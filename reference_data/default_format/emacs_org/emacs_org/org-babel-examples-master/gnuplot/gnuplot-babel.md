# gnuplot-babel

Derek Feichtinger

\<2014-01-03 Fri\>

# Version information

``` numberSource
(princ (concat
        (format "Emacs version: %s\n"
                (emacs-version))
        (format "org version: %s\n"
                (org-version))))        
```

    Emacs version: GNU Emacs 24.3.1 (i686-pc-linux-gnu, GTK+ Version 3.4.2)
     of 2013-10-03 on hamsa, modified by Debian
    org version: 8.2.4

# Links and Documentation

- <http://orgmode.org/worg/org-contrib/babel/languages/ob-doc-gnuplot.html>

# Simple graphs

From an example by Eric Schulte

``` gnuplot
reset

set title "a simple graph"

set xrange [0:1]
set autoscale y
set xlabel "frequency of A"

plot x * x title 'AA', (1-x) * (1-x) title 'aa', 2 * x * (1-x) title 'Aa'  
```

``` gnuplot
reset

set title "Putting it All Together"

set xlabel "X"
set xrange [-8:8]
set xtics -8,2,8


set ylabel "Y"
set yrange [-20:70]
set ytics -20,10,70

f(x) = x**2
g(x) = x**3
h(x) = 10*sqrt(abs(x))

plot f(x) w lp lw 1, g(x) w p lw 2, h(x) w l lw 3
```

# stackoverflow

A method for getting an `#+INCLUDE` of a result SVG file instead of
having it appear as a standard org link. This was my answer to the
stack exchange problem: [How to embed svg output of org-mode src block as inline svg in html export?](http://emacs.stackexchange.com/questions/29871/how-to-embed-svg-output-of-org-mode-src-block-as-inline-svg-in-html-export)

First I define a filter function in this source block

``` elisp
(with-temp-buffer
  (erase-buffer)
  (cl-assert text nil "PostAlignTables received nil instead of text ")
  (insert text)
  (beginning-of-buffer)
  (if (re-search-forward org-any-link-re nil t)
(progn (let ((fname (match-string 2)))
     (replace-match
      (format "#+INCLUDE: \"%s\" export html" fname))
     ))
    (error "PostFileToInclude: Was not able to find link in output"))
  (buffer-string)
  )
;; #+INCLUDE: "example-plot.svg" export html
```

And here we use the filter function in the `:post` option.

``` gnuplot
plot sin(x)
```

Naturally, one could make the filter much more intelligent, e.g. only doing it for SVG files, etc.