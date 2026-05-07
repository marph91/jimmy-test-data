# lisp-babel

Derek Feichtinger

# How to use this document

You should look at this document in its Org mode source form. The
PDF rendering is useful to see the results of some of the export
options, but the syntax of the source block is only seen in the
source text.

# Version information

``` commonlisp
(princ (concat (format "Emacs version: %s\n" (emacs-version))
               (format "org version: %s\n" (org-version))))
```

    Emacs version: GNU Emacs 24.5.1 (x86_64-unknown-linux-gnu, GTK+ Version 3.10.8)
     of 2015-05-04 on dflt1w
    org version: 8.3.2

# using a table as input for a src block

## simple example

We first create a table from a lisp **list of lists**. Each inner list
will form a row in the resulting table. I already insert a header
row with the names of three columns. A separator line can be obtained
by putting the `hline` symbol into the resulting list.

``` commonlisp
(cons '(col1 col2 col3)
      (cons 'hline
            (loop for i from 5 to 15 collect `(,i ,(* i 5) ""))))
```

| col1 | col2 | col3 |
|------|------|------|
| 5    | 25   |      |
| 6    | 30   |      |
| 7    | 35   |      |
| 8    | 40   |      |
| 9    | 45   |      |
| 10   | 50   |      |
| 11   | 55   |      |
| 12   | 60   |      |
| 13   | 65   |      |
| 14   | 70   |      |
| 15   | 75   |      |

We now can fill the third column by passing the table into the next
source block. We force babel to treat the first row as table header
by using the **:colnames yes** header argument. This also causes the
result table to contain the headers (as long as the new table has the
same number of columns as the original table)

Here I also demonstrate the use of the **-n** option that will export
the code with line numbers.

``` numberSource
(let (result)
  (dolist (row tbl result)
    (setf (nth 2 row) (* 2 (nth 1 row)))
    (setq result (cons row result)))
  (reverse result))
```

| col1 | col2 | col3 |
|------|------|------|
| 5    | 25   | 50   |
| 6    | 30   | 60   |
| 7    | 35   | 70   |
| 8    | 40   | 80   |
| 9    | 45   | 90   |
| 10   | 50   | 100  |
| 11   | 55   | 110  |
| 12   | 60   | 120  |
| 13   | 65   | 130  |
| 14   | 70   | 140  |
| 15   | 75   | 150  |

## passing a sub-range

It is possible to specify a sub-range for the table that is handed over through `:var`. But currently
it does not work well with the `:colnames yes` option, as the following example shows.

``` numberSource
(let (result)
  (dolist (row tbl result)
    (setf (nth 2 row) (* 2 (nth 1 row)))
    (setq result (cons row result)))
  (reverse result))
```

| 7   | 35  |     |
|-----|-----|-----|
| 8   | 40  | 80  |
| 9   | 45  | 90  |
| 10  | 50  | 100 |
| 11  | 55  | 110 |

## Investigating how tables are passed to the src block

| col1 | col2 | col3        |
|------|------|-------------|
| 10   | str  | two strings |
| 20.5 | str2 | 2 strings   |

``` commonlisp
(pp tbl)
```

    ((10 "str" "two strings")
     (20.5 "str2" "2 strings"))

Note that the `raw value` output of the source block does not yield
the same. It loses the string quotes of the single entries!

``` commonlisp
tbl
```

((10 str two strings) (20 str2 2 strings))

# TODO using a list as input for a source block

- item1
- item2
  1.  subitem2.1
  2.  subitem2.2
- item3
  - subitem3.1
- item4

Let's look at the resulting structure that is passed to a source block

``` elisp
(pp lst)
```

    (("item1")
     ("item2"
      (ordered
       ("subitem2.1")
       ("subitem2.2")))
     ("item3"
      (unordered
       ("subitem3.1")))
     ("item4"))

This is different from the current entry in the Manual ([info:org#var](info:org#var)), where it is said that only top
level items are passed along. But this complete passing along of the structure opens nice and
interesting ways of using lists. Need to ask whether this interface will remain stable.

One important point to clarify is, why is the returned structure not exactly the result of
what the Org function `org-list-to-lisp` returns? Comparing with that output we see that the
current handing over of a list by the `:var` argument is losing the outermost layer of information
that describes whether the top level list is of the ordered, unordered, … type.

``` elisp
(pp (save-excursion
  (goto-char (point-min))
  (unless (search-forward-regexp (concat  "#\\\+NAME: .*" lname) nil t)
    (error "No list of this name found: %s" lname))
  (forward-line 1)
  (org-list-to-lisp)))
```

    (unordered
     ("item1")
     ("item2"
      (ordered
       ("subitem2.1")
       ("subitem2.2")))
     ("item3"
      (unordered
       ("subitem3.1")))
     ("item4"))

# calling source blocks as a function

## Chaining source block execution

I **can have another piece of code implicitly called** by using its
name as an input variable in another code block. So, I could
directly fill the third column of our initial example table without
ever having to print out that table table. We can just pass into the
next function a variable `tbl` and the name of the initial code
block `make-table1`.

``` commonlisp
(let (result)
  (dolist (row tbl result)
    (setf (nth 2 row) (* 2 (nth 1 row)))
    (setq result (cons row result)))
  (reverse result))
```

| col1 | col2 | col3 |
|------|------|------|
| 5    | 25   | 50   |
| 6    | 30   | 60   |
| 7    | 35   | 70   |
| 8    | 40   | 80   |
| 9    | 45   | 90   |
| 10   | 50   | 100  |
| 11   | 55   | 110  |
| 12   | 60   | 120  |
| 13   | 65   | 130  |
| 14   | 70   | 140  |
| 15   | 75   | 150  |

## simple call syntax using CALL

We first define a function in a named code block called `mydouble`. The
variable x will be passed in by defining a header argument `:var x`

``` commonlisp
(* 2 x)
```

Now we can call this babel function by using the code block's name
`mydouble` from any place in the document. For example:

    10

Another example where we pass in two variables x and y.

``` commonlisp
(/ x y)
```

Note that **you can/must pass additional header arguments** to the
call. The ones added at the end influence the final result
(e.g. putting it into a drawer), while the ones added in \[\] are
evaluated in the context of the original definition (e.g whether to
capture the output or return a value).

    4

Another alternative calling syntax

    5

## calling a source block function from elisp

This function is also used for table formulas

``` elisp
(org-sbe mydivide (x 10) (y 3))
```

    3

``` elisp
(princ (concat s1 " " s2))
```

    hello world

``` elisp
(princ (org-sbe srcRepeatStrings (s1 $"hello") (s2 $"world")))
```


    (s1 (quote "hello"))

    (s2 (quote "world"))

    (results (quote "hello world"))
    hello world

``` elisp
(org-babel-execute-src-block nil
                            '("emacs-lisp" "results"
                              ((:var . "results=mydivide")))
                            '((:results . "silent")))
```


    (x (quote 30))

    (y (quote 5))

    (results (quote 6))

``` elisp
(org-babel-execute-src-block nil
                              '("emacs-lisp" "(princ (format \"%s haahahaa\n\"results))"
                                ((:var . "results=mydivide")))
                           '((:results . "silent")))
```

    6 haahahaa

## Naming an output table produced by a CALL

If the called function produces an output table that one wants to
use in subsequent function calls or in table formulas (using the
`remote` keyword) one can give the CALL a name utilizing the syntax
used for other org elements:

| col1 | col2 | col3 |
|------|------|------|
| 5    | 25   |      |
| 6    | 30   |      |
| 7    | 35   |      |
| 8    | 40   |      |
| 9    | 45   |      |
| 10   | 50   |      |
| 11   | 55   |      |
| 12   | 60   |      |
| 13   | 65   |      |
| 14   | 70   |      |
| 15   | 75   |      |

# Inline src calls

Basic inline source calls:

- `(``nth`` ``0`` (``nth`` (``-`` (``length`` tbl) ``1``) tbl))` {{{results(`15`)}}}

- `(org-table-get-remote-range ``"table1"`` ``"@>$1"`` )` {{{results(`15`)}}}

Note, that the result gets wrapped into an ORG MACRO syntax using three curly brackets. This allows
org to replace the results of the evaluation if the inline call is executed multiple times.

If one uses the `:results raw` option, the results are placed "as is" into the buffer, so multiple
executions will lead to multiple insertions of the result.

`(org-table-get-remote-range ``"table1"`` ``"@>$1"`` )` 15

Inline source code is only supposed to create one-line results. If you write code that generates
multiple result lines, an error is raised: *Inline error: multiline result cannot be used*

`(``princ`` ``"hahha``\n``yesyesyes"`` )`

# Defining buffer wide variables for src blocks

One can use a verbatim block like this. I define a named block `myvar` and
I pass it into the variable s of the following code block. This lends itself to some nice
ideas of inserting test in form of templates with some custom variable replacement

    world

``` commonlisp
(concat "hello " s)
```

    hello world

# Using a :post function for post-formatting and executing generated tables

Often I produce multiple tables from a source block (e.g. printing
several pandas data frames). These tables do not get aligned in the
org document after the execution of the code block (even though they
will get aligned upon exporting the document). Also, I may want to have
table calculations using `#+TBLFM` lines executed, instead of manually
having to execute them in the resulting tables.

The following function can be used in a :post argument for getting
all tables in the output aligned and their TBLFM instructions executed, as shown further below

``` commonlisp
(with-temp-buffer
  (erase-buffer)
  (cl-assert text nil "PostAlignTables received nil instead of text ")
  (insert text)
  (beginning-of-buffer)
  (org-mode)
  (while
      (search-forward-regexp org-table-any-line-regexp nil t)
    (org-table-align)
    (org-table-recalculate 'iterate)
    (goto-char (org-table-end)))
  (buffer-string))
```

    |  5 | 22222 |
    |  0 |       |
    | 12 |    45 |
    |----+-------|
    | 17 |       |
    #+TBLFM:@>$1=vsum(@1..@-1)

    |  1 | 22222 |
    |  0 |       |
    | 12 |    45 |

Example without using the `:post` function:

``` commonlisp
(princ
 (concat
  "#+CAPTION: Test1\n"
  "|A|B|C|\n"
  "|---\n"
  "|1|20|300|\n"
  "|200|30|4|\n"
  "|---\n"
  "||||\n"
  "#+TBLFM: @>$1..@>$3=vsum(@I..@II)\n"
  "\n#+CAPTION: Test2\n"
  "|A|B|C|\n"
  "|---\n"
  "|1|20|300|\n"
  "|200|30|4|\n"
  ))
```

| A   | B   | C   |
|-----|-----|-----|
| 1   | 20  | 300 |
| 200 | 30  | 4   |
|     |     |     |

Test1

| A   | B   | C   |
|-----|-----|-----|
| 1   | 20  | 300 |
| 200 | 30  | 4   |

Test2

The same example with the `:post` function:

``` commonlisp
(princ
 (concat
  "#+CAPTION: Test1\n"
  "|A|B|C|\n"
  "|---\n"
  "|1|20|300|\n"
  "|200|30|4|\n"
  "|---\n"
  "||||\n"
  "#+TBLFM: @>$1..@>$3=vsum(@I..@II)\n"
  "\n#+CAPTION: Test2\n"
  "|A|B|C|\n"
  "|---\n"
  "|1|20|300|\n"
  "|200|30|4|\n"
  ))
```

| A   | B   | C   |
|-----|-----|-----|
| 1   | 20  | 300 |
| 200 | 30  | 4   |
| 201 | 50  | 304 |

Test1

| A   | B   | C   |
|-----|-----|-----|
| 1   | 20  | 300 |
| 200 | 30  | 4   |

Test2

# Library of babel

The "Library of Babel" feature provides a kind of primitive function
library system for org files. It allows running source blocks that
have been added to it in every org file. The library is implemented
as an association list with the source block names as the keys. It
is stored in the `org-babel-library-of-babel` variable.

Execute the following source block to load the source code blocks of the
test file `lib-of-babel-test.org` into the library of babel.

    1

For example, the post table alignment function of the last section is a useful generic function. I renamed it in the
`lib-of-babel-test.org` file to `srcPostAlignTablesLIB` to demonstrate that it indeed is the definition from that file.

I can call the function like any normally defined named source code block which produces:

    |  5 | 22222 |
    |  0 |       |
    | 12 |    45 |
    |----+-------|
    | 17 |       |
    #+TBLFM:@>$1=vsum(@1..@-1)

    |  1 | 22222 |
    |  0 |       |
    | 12 |    45 |

But more interesting for this example, I can also use it in the `:post` block:

``` elisp
(princ text)
```

| A   | 22222 |
|-----|-------|
| B   |       |
| C   | 45    |
|     | 22267 |

| X   | 3   |
|-----|-----|
| Y   | 4   |
| Z   | 5   |
|     | 12  |

Note: Originally, I thought I could have the babel library as a
local variable by executing the `org-babel-lob-ingest` on a file
local variable in the local variable section of the file (using
first make-local-variable and the using the ingest). But it turns
out that during the ingest the buffer associated with the sourced
file is active, so the local variable in this buffer remains
unset. This is regrettable, because this means that the library of
babel is always global. One could set the
`org-babel-library-of-babel` variable directly to the final value
instead of using the ingest function, but this would break the
abstraction.