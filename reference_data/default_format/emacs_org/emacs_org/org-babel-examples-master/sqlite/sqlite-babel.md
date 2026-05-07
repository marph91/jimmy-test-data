# sqlite-babel

Derek Feichtinger

# Version information

``` commonlisp
(princ (concat (format "Emacs version: %s\n" (emacs-version))
               (format "org version: %s\n" (org-version))))
```

    Emacs version: GNU Emacs 27.2 (build 1, x86_64-pc-linux-gnu, GTK+ Version 3.22.30)
     of 2021-08-29
    org version: 9.5.2

# using a table as input

Note: Do not use colons in the table fields, since they are used as field delimiters in the table import

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

It is necessary to create the explicit table definition. The table can be
read in via the **.import** function.

``` sql
drop table if exists t1;
create table t1 (col1 INTEGER, col2 INTEGER, col3 INTEGER);
.import "$tbl" t1
select count(*) from t1;
```

    11

# SQLite table UPDATEs, column names

The **:colnames yes** option selects in the next block that the output
table should contain a header row with the column names.

``` sql
UPDATE t1 SET col3 = 2 * col2;
SELECT * FROM t1;
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

# SELECTs and using babel blocks as functions via CALL

``` sql
SELECT * FROM t1 WHERE col1>=$val;
```

| col1 | col2 | col3 |
|------|------|------|
| 13   | 65   | 130  |
| 14   | 70   | 140  |
| 15   | 75   | 150  |

Now the filter can be called as a function using the org babel CALL syntax

| col1 | col2 | col3 |
|------|------|------|
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