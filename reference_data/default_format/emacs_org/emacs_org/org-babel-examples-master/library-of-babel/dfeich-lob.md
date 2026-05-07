# Library of Babel

Derek Feichtinger

\<2017-12-29 Fri\>

# Introduction

I define all source block names with a prefix "lob", so that it will be easy to use expansion/completion
for these functions.

When changing this file, I need to execute the following, to reload the babel functions

``` elisp
(dfeich/lib-babel-reinitialize)
```

(\~/Dropbox/org/examples/library-of-babel/dfeich-lob.org)

# Table related functions

## PostAlignTables - Align and calculate multiple tables of an output block

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

### Test

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

## InsertTableFromFile

``` elisp
  (let* ((klist (cl-remove-if (lambda (x) (equal (cadr x) ""))
              `(("ATTR_LATEX" ,newattr) ("CAPTION" ,newcaption) ("NAME" ,newname))))
     (tbl
      (with-temp-buffer
    (org-mode)
    (insert-file-contents fname)
    (goto-char (point-min))
    (unless (re-search-forward
         (concat "^[ \t]*#\\+\\(tbl\\)?name:[ \t]*"
             (regexp-quote tname) "[ \t]*$")
         nil t)
      (user-error "Can't find table named %s in file" tname fname))
    (forward-line 0)
    (let ((tstart (match-beginning 0))
          tend)
      (while (looking-at "^[ \t]*#\\+\\([^:]+\\): *\\(.*\\)")
        (add-to-list 'klist `(,(upcase (match-string 1)) ,(match-string 2)))
        (delete-region (point) (line-end-position))
        (kill-line))
      (unless (looking-at org-table-line-regexp)
        (looking-at "^.*$")
        (user-error "no table at location of %s, Looking-at: '%s'" tname (match-string 0)))
      (goto-char (org-table-end))
      (while (looking-at-p "^[ \t]*#\\+TBLFM:")
        (forward-line 1))
      (buffer-substring tstart (point))))))
(setq klist (nreverse klist)) ;; reverse for giving priority to new user settings
(dolist (elem '("NAME" "CAPTION" "ATTR_LATEX"))
  (when (assoc elem klist)
    (princ (format "#+%s: %s\n" elem (cadr (assoc elem klist))))))
(princ tbl))
```

### Test setup boilerplate

Creating a file for testing

``` elisp
  (with-temp-file "/tmp/insert-file-test.org"
(goto-char (point-max))
(insert "some text at the start
  #+NAME: test-table1
  | a | b | c |
  |---+---+---|
  | 1 | 2 | 3 |
  | 2 | 4 | 6 |
  |---+---+---|
  |   |   | 9 |
  #+TBLFM: @>$>=vsum(@I..@II)
  some text at the end

  #+NAME: notable
  #+BEGIN_EXAMPLE
  Some Example
  #+END_EXAMPLE

  some other text at the start
  #+NAME: test-table2
  #+caption: original caption of test-table2
  #+ATTR_LATEX: :font \\footnotesize :placement [H]
  | a |  b |  c |
  |---+----+----|
  | 1 | 20 | 10 |
  | 2 | 40 | 20 |
  |---+----+----|
  |   |    | 30 |
  #+TBLFM: @>$>=vsum(@I..@II)
  some other text at the end"))
```

### Test

| a   | b   | c   |
|-----|-----|-----|
| 1   | 20  | 10  |
| 2   | 40  | 20  |
|     |     | 30  |

original caption of test-table2

| a   | b   | c   |
|-----|-----|-----|
| 1   | 20  | 10  |
| 2   | 40  | 20  |
|     |     | 30  |

new caption

## TableFilter

``` elisp
(let ((lst (split-string vals)))
  (concatenate 'list  (loop for row in tbl
                            if (member (let ((field (nth col row)))
                                         (if (numberp field)
                                             (number-to-string field)
                                           field)) lst)
                            collect row into newtbl
                            ;; else do (princ (format "%s: %s\n" (nth col row) lst))
                            finally return newtbl)))
```

### Test

| Name  | A   | B   |
|-------|-----|-----|
| Peter | 1   | 10  |
| Paul  | 2   | 20  |
| Mary  | 3   | 30  |
| Peter | 4   | 40  |
| Mary  | 5   | 50  |
| Peter | 6   | 60  |

| Name  | A   | B   |
|-------|-----|-----|
| Peter | 1   | 10  |
| Paul  | 2   | 20  |
| Peter | 4   | 40  |
| Peter | 6   | 60  |

## lobTableFilterRe

``` elisp
(let ((lst (split-string vals)))
  (concatenate 'list  (loop for row in tbl
                            if (let* ((rawfield (nth col row))
                                      (field (if (numberp rawfield)
                                                 (number-to-string rawfield)
                                               rawfield)))
                                 (loop for regx in lst
                                       when(string-match-p regx field) return 't
                                       finally return nil))
                            collect row into newtbl
                            ;; else do (princ (format "%s: %s\n" (nth col row) lst))
                            finally return newtbl)))
```

### Test

| Name | A                                | B   |
|------|----------------------------------|-----|
| aa   | for mu3e                         | 10  |
| bb   | belongs to MEG.                  | 20  |
| cc   | has its own account              | 30  |
| dd   | another item for mu3e experiment | 40  |
| ee   | for own group                    | 50  |
| ff   | another one for MEG exp          | 60  |

| Name | A                                | B   |
|------|----------------------------------|-----|
| aa   | for mu3e                         | 10  |
| bb   | belongs to MEG.                  | 20  |
| dd   | another item for mu3e experiment | 40  |
| ff   | another one for MEG exp          | 60  |

## GroupTable

``` python
import pandas as pd
import numpy as np
import orgbabelhelper as obh
import sys
import re

df = obh.orgtable_to_dataframe(tbl)
grparr = re.split(r",\s*", grp)
#print re.split(r",\s*", rescols) + [grp]
df = df[re.split(r",\s*", rescols) + grparr]
for elem in grparr:
    assert elem in df.columns, "Error: group column %s not in table columns %s" % (elem, ",".join(df.columns))

if op == "sum":
    res = df.groupby(grparr).sum()
else:
    error("operation %s not implemented" % op)
    sys.exit(1)

print(obh.dataframe_to_orgtable(res))
```

### Test

| Name  | Year | A   | B   |
|-------|------|-----|-----|
| Peter | 2018 | 1   | 10  |
| Paul  | 2018 | 2   | 20  |
| Mary  | 2018 | 3   | 30  |
| Peter | 2019 | 4   | 40  |
| Paul  | 2019 | 5   | 50  |
| Mary  | 2019 | 5   | 60  |
| Peter | 2019 | 6   | 70  |

| Name  | B   |
|-------|-----|
| Mary  | 90  |
| Paul  | 70  |
| Peter | 120 |

| Year | Name  | B   |
|------|-------|-----|
| 2018 | Mary  | 30  |
| 2018 | Paul  | 20  |
| 2018 | Peter | 10  |
| 2019 | Mary  | 60  |
| 2019 | Paul  | 50  |
| 2019 | Peter | 110 |

## ExportOneTableToExcel

Function to write a single table TBL to an Excel file FNAME.

``` python
import pandas as pd
import numpy as np
from pathlib import Path
import orgbabelhelper as obh
import openpyxl

df = obh.orgtable_to_dataframe(tbl)

with pd.ExcelWriter(fname, engine='openpyxl') as writer:
    if Path(fname).exists():
        book = openpyxl.load_workbook(fname)
        writer.book = book
    df.to_excel(writer, sheet, index=False)
    writer.save()
```

## ExportTablesToExcel

Function to write several tables to different sheets in the same
Excel file FNAME. The table names are given as a string TBLNAMES
containing the comma separated list of table names. The sheet name
is given in SHEET.

Here I use a method copied from the `org-sbe` implementation where
a particular source block is called by executing
`org-babel-execute-src-block` on a constructed source block info
structure, where the call is given as part of that source block's
`:var` definition.

``` elisp
(when (file-exists-p fname)
  (if (string=  overwrite "yes")
      (delete-file fname)
    (error "Error: File exists: %s. Refusing to overwrite!" fname)))
(cl-loop
 for tbl in (split-string tblnames "," t "[[:space]]**")
 do (org-babel-execute-src-block
     nil
     (list "emacs-lisp" "myresults"
           `((:var .
                   ,(format "myresults=lobExportOneTableToExcel"
                            tbl fname tbl))))
     '((:results . "silent")))
 (message "wrote table %s to file %s" tbl fname))
```

- TODO: Allow overwriting of Excel sheets.
  - If overwite=yes and a new
    sheet has the same name as an existing sheet, the new sheet is
    added with a new name.

### Test

Test without overwrite option

Test with overwrite option

# File related functions

## Insert file in a suitable block

``` elisp
(cl-labels ((wrap-src
        (lang)
        (list (format "#+BEGIN_SRC %s :eval never :exports source\n" lang)
                   "#+END_SRC\n")))
  (let ((wrappers
    (pcase (file-name-extension filename)
      ("py" (wrap-src "python"))
      (".el" (wrap-src "emacs-lisp"))
      (t '("#+BEGIN_EXAMPLE\n" "#+END_EXAMPLE\n")))))
    (with-temp-buffer
      (goto-char (point-min))
      (insert (format-time-string "# inserted at %Y-%m-%d %H:%M:%S\n"))
      (insert (car wrappers))
      (insert-file-contents filename)
      (goto-char (point-max))
      (insert (car (cdr wrappers)))
      (buffer-string))))
```

# Output cleaning

## Clean control characters from output

``` commonlisp
(replace-regexp-in-string "\x1b\\[[0-9;]*[a-zA-Z]" "" input)
```

# Sysadmin tools

``` bash
if [[ -z "$pid" ]]; then
    echo "Error: no pid given (pid=$pid)?"
    exit 1
fi
sigparse () {
    i=0
    # bits="$(printf "16i 2o %X p" "0x$1" | dc)" # variant for busybox
    bits="$(printf "ibase=16; obase=2; %X\n" "0x$1" | bc)"
    while [ -n "$bits" ] ; do
        i="$(expr "$i" + 1)"
        case "$bits" in
       *1) printf " %s(%s)" "$(kill -l "$i")" "$i" ;;
        esac
        bits="${bits%?}"
    done
}
ps up "$pid" | cat
if [[ $? -ne 0 ]]; then
    echo "Error: Seems there is no such process?"
    exit 1
fi

grep "^Sig...:" "/proc/${pid}/status" | while read a b ; do
    printf "%s%s\n" "$a" "$(sigparse "$b")"
done # | fmt -t  # uncomment for pretty-printing
```

# Local Variables

Local variables:
org-confirm-babel-evaluate: nil
End: