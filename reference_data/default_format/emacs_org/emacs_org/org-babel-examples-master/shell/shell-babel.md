# shell-babel

Derek Feichtinger

# Version information

``` numberSource
(princ (concat
        (format "Emacs version: %s\n"
                (emacs-version))
        (format "org version: %s\n"
                (org-version))))
```

    Emacs version: GNU Emacs 26.2 (build 2, x86_64-pc-linux-gnu, GTK+ Version 3.22.30)
     of 2019-04-14
    org version: 9.3.6

``` bash
bash --version
```

    GNU bash, version 4.4.20(1)-release (x86_64-pc-linux-gnu)
    Copyright (C) 2016 Free Software Foundation, Inc.
    License GPLv3+: GNU GPL version 3 or later <http://gnu.org/licenses/gpl.html>

    This is free software; you are free to change and redistribute it.
    There is NO WARRANTY, to the extent permitted by law.

``` bash
dpkg -l dash | tail -n 1
```

    ii  dash           0.5.8-2.10   amd64        POSIX-compliant shell

# Variables for source blocks

Note that you need to use a plus `+` in the definition of
header-args in the document-wide or section properties if you want
the new definition to be added to the old definition, i.e. use
`header-args+`. If you use just `header-args` then the previous
`:var` setting will be replaced by the new setting

``` bash
echo $docwide_var
echo $section_var
echo $block_var
```

    docwide
    section
    block

# Tables as input for source blocks

## Using sh (or dash) as shell

| col1 | col2 | col3 |
|------|------|------|
| 11   | 12   | 13   |
| 21   | 22   | 23   |
| 31   | 32   | 33   |

When using **sh** as language, I get the "old" behavior of obtaining all field values by just
printing the variable.

``` bash
echo $tbl
```

    11 12 13 21 22 23 31 32 33

Internally the variable expansion into the bash script is done by this org function:

``` elisp
(org-babel--variable-assignments:sh-generic 'tbl '((11 12 13) (21 22 23) (31 32 33)) nil nil)
```

    tbl='11    12  13
    21 22  23
    31 32  33'

### TODO `org-babel-expand-src-block` expands sh blocks independent of shell type defined by src block

Submitted as bug report to [mailing list](http://lists.gnu.org/archive/html/emacs-orgmode/2017-05/msg00082.html)

When using `org-babel-expand-src-block` with a shell src block
one always gets the same code expansion (in my case bash)
independent of the shell that is used while the execution of the
shell block uses the correct expansion.

``` bash
echo $tbl
```

When expanding the sh source block above with `org-babel-expand-src-block` it is wrongly expanded to the
bash expansion and not to the sh expansion that is used when the block is executed. So, instead of the
sh expansion,

    tbl='11    12  13
    21 22  23
    31 32  33'

I see the following expansion in the opened buffer:

    unset tbl
    declare -A tbl
    tbl['11']='12
    13'
    tbl['21']='22
    23'
    tbl['31']='32
    33'
    echo $tbl

Reason:

The case distinction in `org-babel-variable-assignments:shell` is
made based on the shell-file-name which is a standard emacs
variable set by emacs in C code. This is pointing to "/bin/bash"
for my installation.

Looking at the calls stack for the case where we execute the source block and where we just expand it, we see
the following call stack for execution

    org-babel-variable-assignments:shell
    org-babel-execute:shell
    org-babel-execute:sh
    org-babel-execute-src-block

while in the case of just expanding the source block we have

    org-babel-variable-assignments:sh
    org-babel-expand-src-block

Note that `org-babel-variable-assignments:sh` is an alias for
`org-babel-variable-assignments:shell`.

A bit of investigation shows that for all shell languages there
are aliases defined that finally call
`org-babel-execute:shell`. This is set up in the
`org-babel-shell-initialize` function. And it is set up in a way
that `shell-file-name` is overridden by the name of the
particular shell, and this then leads to the correct case
distinction using `shell-file-name` in
`org-babel-variable-assignments:shell`.

The same kind of overriding would have to be in place when
`org-babel-expand-src-block` calls
`org-babel-variable-assignments:shell` in the simple code expansion case. But that
would be a bit hacky since the generic `org-babel-expand-src-block` function should
not override variables needed in just one subclass of backends. It would be
cleaner to have different functions `org-babel-variable-assignments:XXX` for the
different shells.

## Using bash as shell

When using **bash** as language, the expansion uses bash arrays. The
current code (org 9.0.5) makes a case distinction between one-column
tables and tables with multiple columns. This is implemented in
`org-babel--variable-assignments:bash`.

### tables with one column (vectors)

A table with a single column is treated as a vector and translated to an **indexed bash
array**.

| a   |
|-----|
| b   |
| c   |
| d   |
| e   |

A vector table

``` bash
echo ${tbl[*]}
echo ${tbl[0]}   ${tbl[2]}
```

    a b c d e
    a c

The internal expansion of such a vector table is done via
`org-babel--variable-assignments:bash` and then
`org-babel--variable-assignments:bash_array`

``` elisp
(org-babel--variable-assignments:bash 'tbl '((1) (2) (3) (4) (5)) nil nil)
```

    unset tbl
    declare -a tbl=( '1' '2' '3' '4' '5' )

### tables with multiple columns

When using the multi column table from above, the expansion by org
is done using an **associative bash array** where the first column becomes
the index.

``` bash
echo "trying a naive way of printing the table: " $tbl
echo "using the bash syntax for printing all values: " ${tbl[*]}
echo "and finally using a loop over the index"
for idx in ${!tbl[*]}; do
    echo -n "    $idx  "
    while read line; do echo -n "$line  "; done  <<<${tbl[$idx]}
    echo
done
```

    trying a naive way of printing the table: 
    using the bash syntax for printing all values:  22 23 12 13 32 33
    and finally using a loop over the index
        21  22  23  
        11  12  13  
        31  32  33  

So, the first column ends up as the string indexes of the
associative bash array. The current implementation has a major
drawback: The **original order of the rows is not conserved** as
can be seen above and in these examples. The elements belonging
to different columns are separated by newlines (but the echo in
the following code does not show it).

``` bash
 for idx in ${!tbl[*]}; do
echo $idx ${tbl[$idx]}
 done
```

    21 22 23
    11 12 13
    31 32 33

When using `:results value`, org uses the initial table's columns for the new table

``` bash
 for idx in ${!tbl[*]}; do
echo $idx ${tbl[$idx]}
 done
```

| col1 | col2 | col3 |
|------|------|------|
| 21   | 22   | 23   |
| 11   | 12   | 13   |
| 31   | 32   | 33   |

One problem about the current implementation is that it is impossible to
implement a generic solution allowing the use of the column names inside of
the code when using `:colnames no`. Since the sequence of rows is not conserved,
it is impossible to know which was the first row with the names

``` bash
for idx in ${!tbl[*]}; do
    echo -n "    $idx  "
    while read line; do echo -n "$line  "; done  <<<${tbl[$idx]}
    echo
done
```

        21  22  23  
        11  12  13  
        col1  col2  col3  
        31  32  33  

### Working with descriptive column names

| name  | points | multi word comment |
|-------|--------|--------------------|
| Peter | 10     | bad luck           |
| Paul  | 20     | middle ground      |
| Mary  | 30     | the winner         |

We can use use this nice little eval-based setup to work with
descriptive column names. It takes just a minimal boilerplate.

``` bash
colnames="name points comment"
i=0; for cn in $colnames; do c[i]=$cn; i=$((i+1)); done
for idx in ${!tbl[*]}; do
    eval "${c[0]}=$idx"
    i=1; while read line; do eval "${c[$i]}=\"$line\""; i=$((i+1)); done  <<<${tbl[$idx]}
    echo "name:$name points:$points comment:$comment"
done
```

    name:Mary points:30 comment:the winner
    name:Paul points:20 comment:middle ground
    name:Peter points:10 comment:bad luck

### slices

One can use a slice indexing for only importing a subrange of a table

``` bash
echo $slice
```

    11 55 10 50 15 75 14 70 5 25 6 30 7 35

### implementation details of bash table variable assignment

Let's have a look at how the expansion is implemented. The array
is set through `org-babel--variable-assignments:bash` and then
`org-babel--variable-assignments:bash_assoc`.

``` elisp
(org-babel--variable-assignments:bash 'tbl '((11 12 13) (21 22 23) (31 32 33)) nil nil)
```

    unset tbl
    declare -A tbl
    tbl['11']='12
    13'
    tbl['21']='22
    23'
    tbl['31']='32
    33'

I think it would be nicer to treat the first column identical to
the other columns and not make it the index of an associative
array, even though this may be appealing for problems involving
just two columns where the current implementation allows fast
key-value lookups.

A nicer implementation to me would be the use of a simple indexed array
where all values of a row are put into the value part of an array field,
the index number just reflecting the row number.
This allows me to print all fields with an easy
command (`${tbl[*]}`) similar to the older implementations. While this gives me all fields on a
single output line (losing the table structure), I can also retrieve
the whole table structure with the rows in the original order by using a loop construct.

``` bash
 unset tbl
 declare -a tbl
 tbl[0]='11 12 13'
 tbl[1]='21 22 23'
 tbl[2]='31 32 33'

 for idx in ${!tbl[*]}; do
echo ${tbl[$idx]}
 done
```

| 11  | 12  | 13  |
|-----|-----|-----|
| 21  | 22  | 23  |
| 31  | 32  | 33  |

## more examples

We first create a table from a lisp list of lists. Since my final result table
should contain three columns, I already insert a header row with the names for
the three columns.

``` commonlisp
(cons '(col1 col2 col3)
      (loop for i from 5 to 15 collect `(,i ,(* i 5))))
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

sidenote: the -n flag results in line numbers for the exported source code.

``` numberSource
for idx in ${!tbl[*]}; do
    echo $idx ${tbl[$idx]} $((${tbl[$idx]}*2))
done
```

| col1 | col2 | col3 |
|------|------|------|
| 13   | 65   | 130  |
| 12   | 60   | 120  |
| 11   | 55   | 110  |
| 10   | 50   | 100  |
| 15   | 75   | 150  |
| 14   | 70   | 140  |
| 5    | 25   | 50   |
| 6    | 30   | 60   |
| 7    | 35   | 70   |
| 8    | 40   | 80   |
| 9    | 45   | 90   |

As remarked before, the order of the rows is regrettably lost with the current implementation of bash arrays. In the
present case once could use a sort filter at the end, but this only works because we use some external knowledge
about this particular table. For generic tables the order is lost.

# some useful source block options

## dir

One can use the :dir option to have the shell code executed within
a particular working directory.

``` bash
pwd
```

    /home

Since the directory can also be a TRAMP URL, `:dir` allows easy
**execution of commands on remote servers**, which to me is the most
powerful application of this option. Combine this option with
the SSH configuration options **ControlMaster and ProxyCommand**
and all remote hosts become one hop away, and you only need to
authenticate once. This allows very nice documenting of remote
work and writing template documents collecting information from
remote servers.

``` bash
hostname
pwd
```

dftest2
/etc

## line numbering for exported code: -n

Using the flag `-n` results in the exported code lines being printed with line numbers.

# noweb example - including code blocks in other code blocks

Redefine the standard **noweb markers**, since `<<` and `>>` are valid shell code redirectors and this messes
up the syntax highlighting for source blocks. This can be
done by defining the variables `org-babel-noweb-wrap-start` and `org-babel-noweb-wrap-end`. I do this
in the footer of this document in the emacs "Local Variables" section choosing a markup as in "`<<<bla>>>`".

``` bash
echo "I am from A"
```

Now we include the code from the upper source block in the following block

``` bash
echo "This is B"

<<<srcCodeA>>>

echo "This is B again"

cat <<EOF
this way we do not mess with "here"-documents
EOF

echo "the end"
```

    This is B
    I am from A
    This is B again
    this way we do not mess with "here"-documents
    the end

# Changes in regard to earlier versions of this document

## org-babel-sh-command no longer used for selecting shell

In earlier implementations of org one needed to select the
particular shell that was run by setting the `org-babel-sh-command`
to the shell executable, e.g. "/bin/bash". This was either done
globally or in the usual local variable section of a document. The
newer org versions (certainly org\>9.x) allow specifying the shell
type as one usually specifies any language of a source block,
i.e. by writing a header like `#+BEGIN_SRC bash`.