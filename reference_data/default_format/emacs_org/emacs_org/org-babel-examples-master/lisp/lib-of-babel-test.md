# Example of an org-babel library

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