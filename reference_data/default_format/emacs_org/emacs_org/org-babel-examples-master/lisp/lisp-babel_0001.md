### Contents 1 How to use this document

2 Version information

3 using a table as input for a src block  3.1 simple example . . . . . . . . . . . . . . . . . . . . . . . . . .  3.2 passing a sub-range . . . . . . . . . . . . . . . . . . . . . . . .  3.3 Investigating how tables are passed to the src block . . . . . .

4 calling source blocks as a function  4.1 Chaining source block execution . . . . . . . . . . . . . . . . .  4.2 simple call syntax using CALL  4.3 Naming an output table produced by a CALL . . . . . . . . .

5 Inline src calls

6 Dening buer wide variables

7 Using a :post function for post-formatting and executing generated tables 8 Library of babel

1 How to use this document

You should look at this document in its Org mode source form. The PDF rendering is useful to see the results of some of the export options, but the syntax of the source block is only seen in the source text.

## lisp-babel

Derek Feichtinger

January 3, 2018 1

2

2 2 3

3

4

4 . . . . . . . . . . . . . . . . . 4 5 6

for src blocks 6

6

8

---

2 Version information

(princ (concat (format "Emacs version: %s\n" (emacs-version)) (format "org version: %s\n" (org-version))))

Emacs version: GNU Emacs 24.5.1 (x86_64-unknown-linux-gnu, GTK+ Version 3.10.8) of 2015-05-04 on dflt1w

org version: 8.3.2

3 using a table as input for a src block 3.1 simple example

We rst create a table from a lisp a row in the resulting table. I already insert a header row with the names of three columns. A separator line can be obtained by putting the symbol into the resulting list.

(cons ’(col1 col2 col3)

(cons ’hline (loop for i from 5 to 15 collect `(,i ,(* i 5) ""))))

col1  5  6  7  8  9 10  11  12

13

14

15

We now can ll the third column by passing the table into the next source block. We force babel to treat the rst row as table header by using the :colnames yes header argument. This also causes the result table to contain the headers (as long as the new table has the same number of columns as the original table) Here I also demonstrate the use of the code with line numbers.

list of lists . Each inner list will form

hline

col2 col3 25 30 35 40 45 50 55 60 65 70

75

-n option that will export the

---

1 (let (result) 2 (dolist (row tbl result) 3

(setf (nth 2 row) (* 2 (nth 1 row))) 4

(setq result (cons row result))) 5 (reverse result))

col1 col2 col3 5 25 50 6 30 60 7 35 70 8 40 80

9 45 90 10 50 100 11 55 110 12 60 120 13 65 130 14 70 140

15 75 150

3.2 passing a sub-range

It is possible to specify a sub-range for the table that is handed over :var. But currently it does not work well with the as the following example shows.

1 (let (result) 2 (dolist (row tbl result) 3

(setf (nth 2 row) (* 2 (nth 1 row))) 4

(setq result (cons row result))) 5 (reverse result)) 7 35 8 40 80

through :colnames yes option,

9 45 90 10 50 100

11 55 110

3.3 Investigating how tables are passed to the src block

col1 col2 col3 10 str two strings 20.5 str2 2 strings

---

(pp tbl)

((10 "str" "two strings") (20.5 "str2" "2 strings"))

Note that the raw value same. It loses the string quotes of the single entries!

tbl

((10 str two strings) (20 str2 2 strings))

4 calling source blocks as a function

4.1 Chaining source block execution

I can have another piece of code implicitly called as an input variable in another code block. So, I could directly ll the third column of our initial example table without ever having to print out that table table. We can just pass into the next function a variable name of the initial code block

(let (result) (dolist (row tbl result) (setf (nth 2 row) (* 2 (nth 1 row))) (setq result (cons row result))) (reverse result))

4.2 simple call syntax using CALL

We rst dene a function in a named code block called variable x will be passed in by dening a header argument

output of the source block does not yield the

make-table1

by using its name

tbl and the

mydouble The :var x (* 2 x)

Now we can call this babel function by using the code block’s name mydouble from any place in the document. For 10

Another example where we pass in two (/ x y)

example:

variables x and y.

---

Note that you can/must pass additional header arguments call. The ones added at the end inuence the nal result (e.g. putting it into a drawer), while the ones added in [] are evaluated original denition (e.g whether to capture the output or return a value).

4

Another alternative calling syntax

to the

in the context of the 5

4.3 Naming an output table produced by a CALL

If the called function produces an output table that one wants subsequent function calls or in table formulas (using the can give the CALL a name utilizing the syntax used for other org elements:

5  6  7  8  9  10  11  12  13  14  15

5  6  7  8  9  10  11  12  13  14  15

to use in remote keyword) one

25 30 35 40 45 50 55 60 65 70 75

25 30 35 40 45 50 55 60 65 70 75

---

5 Inline src calls

This is the result of an inline src call in lisp: 15 and this is another: 15

15

6 Dening buer wide variables

One can use a verbatim block like this. I dene a named block pass it into the variable s of the following code block.

world

### for src blocks

myvar and I (concat "hello " s)

hello world

7 Using a :post function for post-formatting and

### executing generated tables

Often I produce multiple tables from a source block (e.g. printing several pandas data frames). These tables do not get aligned in the org document after the execution of the code block (even though they will get aligned upon exporting the document). Also, I may want #+TBLFM lines executed, instead of manually having to execute them in the resulting tables. The following function can be used in a :post argument for getting all tables in the output aligned and their TBLFM instructions executed, as shown further below

(with-temp-buffer (erase-buffer) (cl-assert text nil "PostAlignTables received nil instead of text ") (insert text) (beginning-of-buffer) (org-mode) (while (search-forward-regexp org-table-any-line-regexp nil t)

to have table calculations using

---

(org-table-align) (org-table-recalculate ’iterate) (goto-char (org-table-end))) (buffer-string)) 5 | 22222 |

0 |  | 12 | 45 | |----+-------|

\| 17 |  #+TBLFM:@>$1=vsum(@1..@-1) 1 | 22222 | 0 |

\| 12 | 45 |

Example without using the :post function:

(princ (concat "#+CAPTION: Test1\n" "|A|B|C|\n"

"|---\n" "|1|20|300|\n" "|200|30|4|\n" "|---\n"

"||||\n" "#+TBLFM: @>$1..@>$3=vsum(@I..@II)\n" "\n#+CAPTION: Test2\n" "|A|B|C|\n"

"|---\n" "|1|20|300|\n" "|200|30|4|\n"

The same example with the :post function:

(princ (concat "#+CAPTION: Test1\n" "|A|B|C|\n"

---

"|---\n" "|1|20|300|\n" "|200|30|4|\n" "|---\n"

"||||\n" "#+TBLFM: @>$1..@>$3=vsum(@I..@II)\n" "\n#+CAPTION: Test2\n" "|A|B|C|\n"

"|---\n" "|1|20|300|\n" "|200|30|4|\n"

8 Library of babel

The "Library of Babel" feature provides a kind of primitive function li-brary system for org les. It allows running source blocks that have added to it in every org le.  ation list with the source block names as the keys.  org-babel-library-of-babel

Table 1: Test1 A B C 1 20 300 200 30 4

Table 2: Test2 A B C 1 20 300 200 30 4

Table 3: Test1 A B C 1 20 300 200 30 4 201 50 304

been The library is implemented as an associ-It is stored in the variable.

---

Execute the following source block to load the source code blocks of the test le lib-of-babel-test.org

(org-babel-lob-ingest "./lib-of-babel-test.org")

For example, the post table alignment function of the last section is a useful generic function. I renamed it in the srcPostAlignTablesLIB to demonstrate that it indeed is the denition from that le. I can call the function like any normally dened named source code block which produces: 5 | 22222 |

0 |  | 12 | 45 | |----+-------|

\| 17 |  #+TBLFM:@>$1=vsum(@1..@-1) 1 | 22222 |

0 |

\| 12 | 45 |

But more interesting for this example, I can also use it in the block: (princ text)

Table 4: Test2 A B C 1 20 300 200 30 4

into the library of babel.

lib-of-babel-test.org le to

:post

A 22222 B C 45 22267

X 3 Y 4 Z 5 12

---

Note: Originally, I thought I could have the babel library as a local variable by executing the org-babel-lob-ingest on a le local variable in the local variable section of the le (using rst make-local-variable and the using the ingest). But it turns out that during the ingest the buer associated with the sourced le is active, so the local variable in this buer remains unset. This is regrettable, because this means that the library of babel is always global. One could set the org-babel-library-of-babel variable directly to the nal value instead of using the ingest function, but this would break the abstraction. Emacs 25.3.1 (Org mode 9.1.5)
