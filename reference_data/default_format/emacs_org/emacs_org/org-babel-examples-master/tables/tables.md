# Org mode tables

Derek Feichtinger

\<2020-08-01 Sat\>

# Org mode and Emacs version information

``` commonlisp
(princ (concat (format "Emacs version: %s\n" (emacs-version))
               (format "org version: %s\n" (org-version))))
```

    Emacs version: GNU Emacs 26.2 (build 2, x86_64-pc-linux-gnu, GTK+ Version 3.22.30)
     of 2019-04-14
    org version: 9.3.7

# Basic table examples

## Basic syntax

Having used Org mode for a few years now, I notice that most of my tables
look like the following

| Name  | number | cost per item | sum      | incl VAT |
|-------|--------|---------------|----------|----------|
| name1 | 3      | 1500.00       | 4500.00  | 4860.00  |
| name2 | 9      | 4000.00       | 36000.00 | 38880.00 |
| name3 | 4      | 2800.00       | 11200.00 | 12096.00 |
| Total |        |               | 51700.00 | 55836.00 |

Note:

- The syntax `@I..@II` for defining the vertical range between the horizontal rulers is extremely
  useful. One does not need to provide row numbers. Regrettably this syntax can only be
  used on the right side of an equation (So this is forbidden: @I\$2..@II\$2=5).
- The use of `>` to indicate the last row or column is useful, since one does not need to use
  explicit row and column numbers.
- Unsurprisingly, `vsum` is the most frequent calc function used in my tables.
- The number format is controlled by the `%.2f` specifiers at the end of the formulas. The
  syntax is similar to the one used in C format specifiers, e.g. %f for float.

Moving rows and columns in a table

- When inserting rows or deleting rows always try to use `M-up` /
  `M-down` (org-table-move-row). It will adapt the formulas.
- When moving columns around, always do it with `M-right` and `M-left`. It will
  adapt the formulas to match the changed structure.

## Advanced table syntax

The same table using named columns, an advanced table feature. The column
names get defined in the row containing `!` in the first column.

|     | Name  | number | cost per item | sum      | incl VAT |
|-----|-------|--------|---------------|----------|----------|
| !   | name  | num    | peritem       | sum      |          |
|     | name1 | 3      | 1500.00       | 4500\.   | 4860.00  |
|     | name2 | 9      | 4000.00       | 36000\.  | 38880.00 |
|     | name3 | 4      | 2800.00       | 11200\.  | 12096.00 |
|     | Total |        |               | 51700.00 | 55836.00 |

Using a column formula instead of the range formula for column 5. In
order to use the other advanced features like the naming of fields,
it is necessary to mark the rows to be affected by the column
formula with a "\*" in the first column. All other rows will
be unaffected.

|     | Name    | number | cost per item | sum      | incl VAT |
|-----|---------|--------|---------------|----------|----------|
| !   | name    | num    | peritem       | sum      |          |
| \*  | name1   | 3      | 1500.00       | 4500\.   | 4860.00  |
| \^  | varname |        |               |          |          |
| \*  | name2   | 9      | 4000.00       | 36000\.  | 38880.00 |
| \*  | name3   | 4      | 2800.00       | 11200\.  | 12096.00 |
|     | Total   |        |               | 51700.00 | 55836.00 |

# Table formulas

## using lisp functions in table formulas

### basic usage

Referenced fields in a lisp formula are read as strings, except if the modifiers `;N` for
numeric or `;L` for using literal values are given at the end of the formula.

Tip: try using the table debugger (C-c {) if something goes wrong.

|     | Row | c2  | c3  | Add | Add2 |
|-----|-----|-----|-----|-----|------|
| !   |     | c2  | c3  |     |      |
| \#  | A   | 1   | 2   | 3   | 3    |
| \#  | B   | 4   | 7   | 11  | 11   |
| \#  | C   | 4   | str | 4   | 4    |

For the next example, this lisp function must be defined in the present emacs session (do `C-x C-e` with the cursor at the end of the expression or use `C-c C-c` on the source block.)

``` commonlisp
  (defun my-colsum-if (keylist vallist keymatch)
  "sum values in vallist if the corresponding key matches the keymatch argument"
(cl-loop for key in keylist
     for val in vallist
     when (equal key keymatch)
     sum (string-to-number val)))
```

The values in the following table are random generated. In the lower section of the table we use
the above function to only add values with the class matching the specification.

|     | Class      | value       |
|-----|------------|-------------|
| !   | class      | value       |
| \#  | A          | 3           |
| \#  | B          | 8           |
| \#  | C          | 2           |
| \#  | A          | 3           |
| \#  | B          | 5           |
| \#  | C          | 9           |
| \#  | all values | 3 8 2 3 5 9 |
| \#  | sum        | 30          |
| \#  | sum if A   | 6           |
| \#  | sum if B   | 13          |

### reading input fields as literal lisp values

Using the `;L` modifier, one can have the references be interpreted as literal
lisp values. In this example I am using this feature for displaying the lisp
types of various arguments in the first column.

| expression                | lisp type |
|---------------------------|-----------|
| 'mapconcat                | symbol    |
| #'mapconcat               | symbol    |
| "text"                    | string    |
| (concat "hello" " world") | string    |
| 1                         | integer   |
| (+ 3 4)                   | integer   |
| ?a                        | integer   |
| 1.0                       | float     |
| '(1 2 3)                  | cons      |
| \[1 2 3 4\]               | vector    |
| nil                       | symbol    |

## Using src block functions in table formulas

### calling a source block from a lisp formula with `org-sbe`

The **org-sbe** macro (warning: it was called **sbe** in earlier org
versions) allows calling the previously defined src blocks from
within table formulas and feeding them then named arguments.

I first define two example source block functions *mydouble* and *mydivide*.

``` commonlisp
(* 2 x)
```

``` commonlisp
(/ x y)
```

|     | A    | calc double | lisp double | lisp divide |
|-----|------|-------------|-------------|-------------|
| !   | colA | colB        | colC        | colD        |
| \#  | 1    | 2           | 2           | 2           |
| \#  | 3    | 6           | 6           | 2           |
| \#  | 9    | 18          | 18          | 2           |

### specifying whether referred to fields are to be read as numbers or strings

**If the field references should be read as strings**, one needs to
add an additional dollar sign, e.q. `$$1, $$colname`, a single
dollar sign `$1` reads the field value as a number. Here is an
example reading in date strings, and using calc functions for doing
some time arithmetic.

``` commonlisp
  (let ((calc-date-format
     '(YYYY "-" MM "-" DD)))
(math-format-date (calcFunc-bsub (calcFunc-incmonth (math-parse-date argdate) (string-to-number argmonths)) 1))
)
```

|     | WP     |                     | WP duration | WP start   | WP end     |
|-----|--------|---------------------|-------------|------------|------------|
|     | number | subject             | months      | date       | date       |
| !   | wpid   | wpname              | wpmonths    | sdate      | edate      |
| \#  | WP0    | Project Management  | 24          | 2015-01-01 | 2016-12-31 |
| \#  | WP1    | IT Infrastructure   | 24          | 2015-01-01 | 2016-12-31 |
| \#  | WP2    | IdM Mngm + Rem Acc  | 12          | 2015-01-01 | 2015-12-31 |
| \#  | WP3    | Data Catalog        | 9           | 2015-01-01 | 2015-09-30 |
| \#  | WP4    | provide existing SW | 24          | 2015-01-01 | 2016-12-31 |
| \#  | WP5    | SW development      | 24          | 2015-01-01 | 2016-12-31 |
| \#  |        | TOTAL               |             |            |            |

A function which sums up the values in a column of table tbl if col1
matches match1 and col2 matches match2

``` commonlisp
;; add vcol column values if col1 matches match1 and col2 matchtes match2
(let ((c1list (org-table-get-remote-range tbl (format "@I$%s..@>$%s" col1 col1)))
      (c2list (org-table-get-remote-range tbl (format "@I$%s..@>$%s" col2 col2)))
      (vallist (org-table-get-remote-range tbl (format "@I$%s..@>$%s" vcol vcol))))
  (cl-loop for c1tst in c1list
           for c2tst in c2list
           for val in vallist
           when (and (equal c1tst match1) (equal c2tst match2))
           sum (string-to-number val))
  )
```

    5

|     | name    | group | use | value |
|-----|---------|-------|-----|-------|
| !   | name    | group | use | value |
|     | john    | B     | 1   | 1     |
|     | beth    | B     | 0   | 3     |
|     | mike    | C     | 1   | 5     |
|     | leslie  | A     | 0   | 7     |
|     | barbara | A     | 1   | 4     |
|     | ken     | C     | 0   | 2     |
|     | thomas  | A     | 1   | 8     |

To demonstrate the above code, we use it to fill the sum column in
the table below. We sum up all values in the above table where the
`group` matches the given target group column, and where the `use`
column matches "1".

|     | target group | sum |
|-----|--------------|-----|
| !   | grp          |     |
| \#  | A            | 12  |
| \#  | B            | 1   |
| \#  | C            | 5   |

### an analytic look at the involved lisp functions

1.  org-sbe

        #+TBLFM: @I$6..@II$6='(org-sbe addmonths (argdate $$sdate) (argmonths $$wpmonths))

    The double dollar ends up in passing this kind of code line where
    the resulting string arguments are headed by a dollar sign:

    ``` commonlisp
    (org-sbe addmonths (argdate $"2015-01-01") (argmonths $"24"))
    ```

        2016-12-30

2.  org-table-get-remote-range

    There seems to be a bug in the org-table-get-remote-range
    function. When I reference the remote range by a field name
    (defined in a special row marked by "\^" in the first column), the
    result is a string that contains the field value wrapped in
    parentheses:

    ``` commonlisp
    (pp (org-no-properties (org-table-get-remote-range "remtable1" "$ref_number"))) (princ "\n")
    (pp (org-no-properties (org-table-get-remote-range "remtable1" "@2$3"))) (princ "\n")
    (pp (org-no-properties (org-table-get-remote-range "remtable1" "$ref_date"))) (princ "\n")
    (pp (org-no-properties (org-table-get-remote-range "remtable1" "@4$3"))) (princ "\n")
    ```

        "(24)"
        "24"
        "(2014-01-02)"
        "2014-01-02"

    Exploring the usage of `remote` inside of a table.

    - The date is read as an equation ("-" is minus) and I get the
      result of a substraction

    Table for remote table test

    |     | Entry    | Value       |
    |-----|----------|-------------|
    |     | a number | 24          |
    | \^  |          | ref~number~ |
    |     | a date   | 2014-01-02  |
    | \^  |          | ref~date~   |

    global model parameters

    Here we try different ways of referencing the fields of the table above using the `remote` keyword:

    | Entry         | field name ref | num ref | lisp + field name |
    |---------------|----------------|---------|-------------------|
    | remote number | 24             | 24      | \(24\)            |
    | remote date   | 2011           | 2011    | (2014-01-02)      |

## some other calc functions used in table formulas

Calc offers a big number of functions. Have a look in [info:calc#Function Index](info:calc#Function%20Index).
Here I present just a few examples in these subsections

### conditions using if

| number | class | even |
|--------|-------|------|
| 1      | A     | odd  |
| 2      | A     | even |
| 3      | B     | odd  |
| 4      | B     | even |

### locate position of element in a column: find

In the following table we use `find` to determine the location of
the "1" in each column. Note that we use the qualifier `;E` in
order to have the vector retain the empty fields.

| Pos    | AA  | BB  | CC  | DD  | EE  | FF  | GG  | HH  | II  | JJ  | KK  | LL  | MM  |
|--------|-----|-----|-----|-----|-----|-----|-----|-----|-----|-----|-----|-----|-----|
| 1      |     |     |     |     | 1   |     |     | 1   |     |     |     | 1   |     |
| 2      |     |     |     | 1   |     |     |     |     |     |     |     |     |     |
| 3      |     |     |     |     |     |     |     |     |     |     |     |     |     |
| 4      |     |     |     |     |     | 1   |     |     |     |     |     |     |     |
| 5      |     |     |     |     |     |     | 1   |     |     |     |     |     |     |
| 6      | 8   |     |     |     |     |     |     |     |     | 1   |     |     |     |
| 7      |     |     |     |     |     |     |     |     |     |     |     |     |     |
| 8      |     |     |     |     |     |     |     |     |     |     |     |     |     |
| 9      |     |     |     |     |     |     |     |     | 1   |     |     |     |     |
| 10     |     |     | 1   |     |     |     |     | 2   |     |     | 1   |     |     |
| 11     | 1   |     |     |     |     |     |     |     |     |     |     |     |     |
| 12     |     |     |     |     |     |     |     |     |     |     |     |     | 1   |
| 13     |     |     |     |     |     |     |     | 1   |     |     |     | 1   |     |
| 14     |     | 1   |     |     |     |     |     |     |     |     |     |     |     |
| 15     | 5   |     |     |     |     |     |     |     |     |     |     |     |     |
| 16     |     |     |     | 1   |     |     |     |     |     |     |     |     |     |
| 17     |     |     |     |     |     |     |     |     | 1   |     |     |     |     |
| 18     |     |     |     |     |     |     | 1   |     |     |     |     |     |     |
| 19     |     |     |     |     |     |     |     |     |     |     |     |     |     |
| Result | 11  | 14  | 10  | 2   | 1   | 4   | 5   | 1   | 9   | 6   | 10  | 1   | 12  |

### mapping over elements of a vector

From a mail by Eric S Fraga to the Emacs-orgmode@gnu.org list

| a       | b       | result       |
|---------|---------|--------------|
| \[2,3\] | \[4,6\] | \[0.5, 0.5\] |

## time calculations

### basic usage

Time calculations can be done using the `T` modifier, which
will expect input in HH:MM\[:SS\] format and deliver output
in HH:MM\[:SS\] format.

For the last column I use the `t` modifier, which delivers
the result as a float according to the setting of the
variable `org-table-duration-custom-format` ('hours by default).

| Item                          | duration | starting | total |
|-------------------------------|----------|----------|-------|
|                               | (min)    | time AM  | hours |
| Presentation by the candidate | 00:20    | 8:30     | 8.50  |
| Presentation Questions        | 00:10    | 08:50:00 | 8.83  |
| Break                         | 00:15    | 09:00:00 | 9.00  |
| Main interview                | 00:90    | 09:15:00 | 9.25  |
| Break                         | 00:15    | 10:45:00 | 10.75 |
| HR Interview                  | 00:60    | 11:00:00 | 11.00 |
| optional Lunch / Coffee       | 00:60    | 12:00:00 | 12.00 |
| optional interview            | 00:30    | 13:00:00 | 13.00 |

### a nicer function for adding up time values

Here another function to add up a time interval and a clock value.

``` commonlisp
(let ((date (org-parse-time-string
             (concat "2015-06-01 "
                     (substring-no-properties inputtime)))))
  (setf (nth 1 date) (+ (nth 1 date) (string-to-number delta)))
  (format-time-string "%H:%M" (apply 'encode-time date)))
```

    09:30

And we use it for calculating the clock value for an interview schedule in
the following table.

| Item                          | duration | starting |
|-------------------------------|----------|----------|
|                               | (min)    | time AM  |
| Presentation by the candidate | 20       | 8:30     |
| Presentation Questions        | 10       | 08:50    |
| Break                         | 15       | 09:00    |
| Main interview                | 90       | 09:15    |
| Break                         | 15       | 10:45    |
| HR Interview                  | 60       | 11:00    |
| optional Lunch / Coffee       | 60       | 12:00    |
| optional interview            | 30       | 13:00    |

## table lookup functions

Interesting advanced possibilities are opened up when using the org table lookup
functions

<http://orgmode.org/worg/org-tutorials/org-lookups.html>

We define a mapping table. Note that we have two mappings for the string "two".

| one   | 1   |
|-------|-----|
| two   | 2   |
| three | 3   |
| four  | 4   |
| two   | 100 |

We fill the second column of the table below according to the
associative array defined by the table above. Values which cannot
be mapped yield nil (it was #ERROR in older
versions). `org-lookup-first` will find the first matching row and
give back the associated mapped value. An `#ERROR` will be returned
for missing key values.

| three | 3   |
|-------|-----|
| five  | nil |
| two   | 2   |
| six   | nil |
| one   | 1   |
| four  | 4   |

`org-lookup-last` accordingly takes the values from the last row that matched.

| three | 3   |
|-------|-----|
| five  | nil |
| two   | 100 |
| six   | nil |
| one   | 1   |
| four  | 4   |

## A note on the choice of column names and remote references

- One must be careful and **not use a remote column name that also is used in the current table**.
  Seems that the substitution of the value in the current scope takes precedence over the one
  in the remote scope.
- Underscores in column names should be avoided. As seen in the Value4 column of the second
  table below, the "\$value~a4~" reference seem to be interpreted just as "\$value"

|     | Entry    | Value | Value2 | Value3  | Value4    |
|-----|----------|-------|--------|---------|-----------|
| !   | entry    | value | value2 | value3a | value~a4~ |
| \#  | example1 | 101   | 102    | 103     | 104       |
|     |          |       |        |         |           |

|     | Entry | Value | Value2 | Value3 | Value4 |
|-----|-------|-------|--------|--------|--------|
| !   |       |       |        |        |        |
| \#  |       | 101   | 102    | 103    | 101    |

## Indirection in remote table references

Org supports indirection for the tablename argument of the `remote`
function in table formulas. So you can refer to tables based on the contents of a current table's fields:

| Tablename         |      |           |
|-------------------|------|-----------|
| remtableIdColName | 4    | 4         |
| table1            | USA  | 50        |
| remtable1         | 2011 | ref~date~ |

# Some examples using tables from babel blocks

## referencing table ranges from lisp code blocks

The lisp function to use for retrieving table values is
`org-table-get-remote-range`.
**Notes**

- the retrieval from tables using advanced naming syntax (e.g `^` in
  the initial column to name the element above as "first") returns
  the value in parentheses (a bug?).
- the advanced naming also creates problems in the ranges, since
  the row containing "first" and the empty value are not filtered out

Here an example for multiple cases.

|     | key   | value |
|-----|-------|-------|
| !   | key   | value |
|     | A     | 1     |
| \^  | first |       |
|     | B     | 2     |
|     | C     | 3     |
|     | D     | 4     |
|     | SUM   | 10    |

``` commonlisp
(mapc (lambda (x) (princ (format "%s => %s\n" (car x) (cdr x))))
      (cl-loop for ref in '("@3$3" "@3$key" "$first" "@I$3..@II$3" "@I$2..@II$3")
       for tblget = (org-table-get-remote-range "tblRefsFromLisp" ref)
       collect (cons ref (pp-to-string
                  (cl-case (type-of tblget)
                    ('cons (mapcar #'substring-no-properties tblget))
                    ('string (substring-no-properties tblget))
                    (t "failed to match")))) into result
       finally return result))
```

    @3$3 => "1"
    @3$key => "A"
    $first => "(A)"
    @I$3..@II$3 => ("1" "" "2" "3" "4")

    @I$2..@II$3 => ("A" "1" "first" "" "B" "2" "C" "3" "D" "4")

## filtering a table

I posted this in reply to [this stackexchange question](http://emacs.stackexchange.com/questions/20129/how-can-i-filter-table-in-org-mode).

We produce an example table to work upon

``` elisp
(let ((countries
       (mapcar #'symbol-name '(CH D USA CN JP PL USA D PL CN CH))))
  (cl-loop for country1 in countries
   for country2 in (reverse countries)
   with counter = 0
   collect (list (format "row%d" counter)
                         (* 2 counter)
                         country1
                         country2
                         (* 5 counter)) into mylst
                         count t into counter
                         finally return (append
                                         '((col1 col2 col3 col4 col5)
                   hline)
                                         mylst)))
```

| col1  | col2 | col3 | col4 | col5 |
|-------|------|------|------|------|
| row0  | 0    | CH   | CH   | 0    |
| row1  | 2    | D    | CN   | 5    |
| row2  | 4    | USA  | PL   | 10   |
| row3  | 6    | CN   | D    | 15   |
| row4  | 8    | JP   | USA  | 20   |
| row5  | 10   | PL   | PL   | 25   |
| row6  | 12   | USA  | JP   | 30   |
| row7  | 14   | D    | CN   | 35   |
| row8  | 16   | PL   | USA  | 40   |
| row9  | 18   | CN   | D    | 45   |
| row10 | 20   | CH   | CH   | 50   |

Now we define a filter function which produces a new
table with the required values. Notice that I am
using the **colnames** argument in the BEGIN line
in order to preserve the column headings.

``` elisp
(loop for row in tbl
      if (equal (nth 3 row) val)
      collect row into newtbl
      finally return newtbl)
```

| col1 | col2 | col3 | col4 | col5 |
|------|------|------|------|------|
| row4 | 8    | JP   | USA  | 20   |
| row8 | 16   | PL   | USA  | 40   |

Note that in the previous source block the input is actually coming from the re-evaluation
of the `table1` source block and not from the resulting table.

I can also use this function with the org-mode CALL syntax

| col1 | col2 | col3 | col4 | col5 |
|------|------|------|------|------|
| row1 | 2    | D    | CN   | 5    |
| row7 | 14   | D    | CN   | 35   |

I also demonstrate here the SQLite approach where I use your
original requirement of filtering all the rows which contain the
string either in columns 3 or 4. A minor drawback of the sqlite
approach is that we have some boilerplate code to read in the table
and create a SQLite DB.

``` sql
drop table if exists table1;
create table table1 (col1 VARCHAR, col2 INTEGER, col3 VARCHAR,
col4 VARCHAR, col5 INTEGER);
.import "$tbl" table1
select * from table1 where col3='$val' or col4='$val';
```

| col1 | col2 | col3 | col4 | col5 |
|------|------|------|------|------|
| row2 | 4    | USA  | PL   | 10   |
| row4 | 8    | JP   | USA  | 20   |
| row6 | 12   | USA  | JP   | 30   |
| row8 | 16   | PL   | USA  | 40   |

| col1 | col2 | col3 | col4 | col5 |
|------|------|------|------|------|
| row1 | 2    | D    | CN   | 5    |
| row3 | 6    | CN   | D    | 15   |
| row7 | 14   | D    | CN   | 35   |
| row9 | 18   | CN   | D    | 45   |

# Exporting tables with some columns hidden

It is desirable to be able and hide columns in exported output. This is often the
case in tables where a lot of computations are done, and where intermediate
results end up in columns that one does not want to end up in the exported document.

This functionality is currently not available by standard org, but since this is Emacs, a simple function
implementing this functionality was published by [Michael Brand](https://github.com/brandm) within this [emacs-orgmode thread](http://lists.gnu.org/archive/html/emacs-orgmode/2016-05/msg00027.html).

The exported table will have col2 removed.

|     | col1 | col2  | col3 |
|-----|------|-------|------|
| /   |      | \<#\> |      |
|     | a1   | a2    | a3   |
|     | b1   | b2    | b3   |

# Information on internals

Nicolas Goaziou [wrote](http://article.gmane.org/gmane.emacs.orgmode/105130) in a reply about the mechanism how formulas are evaluated:

> Field formulas bind stronger than column formulas.
>
> First, all cells with an associated field formula are marked as
> read-only. Then column formulas are evaluated. Eventually, fields
> formulas are evaluated.
>
> This was introduced in Org 5.01, AFAICT. Before, the "read-only" part
> would not happens, i.e, fields formulas would overwrite column formulas.
>
> I think the idea behind this is that formulas are applied to the current
> state of the table, not some intermediate one, with some formulas
> applied and others not.

# Bugs I found \[1/2\]

## FIXED table names like p2~somename~

**do not use table names like p2~somename~ or
somename~p2~\_someother.** The p2 is interpretet as column P, field 2
when you go back from the table editor (C-'), and it will be
substituted by the numeric location @2\$16. This happens when you
use a remote(p2~somename~,somefield) reference in a formula. It
clearly is a bug.
**This seems to be fixed in org-version 8.2.7c**

| one | two |
|-----|-----|
| 1   | 2   |

| col1 | col2 |
|------|------|
| 2    |      |
|      |      |

## OPEN table referenced by remote calls must not contain same column names

|     | one | two |
|-----|-----|-----|
| !   | one | two |
| \#  | 1   | 2   |
| \#  | 3   | 4   |

in the following remote call, the \$one variable is replaced by the
local table's column number for column "one" (which is 2) instead
of the column number of the referred table (where "one" marks the
first column)

|     | one | two |
|-----|-----|-----|
| !   | two | one |
| \#  | 2   |     |
|     |     |     |