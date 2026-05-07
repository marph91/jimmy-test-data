# Org-Mode Beamer Example

Subtitle

Derek Feichtinger

9\. 04. 2026

# Introduction

## An alternative title page for a section

## Instructions

Look at the **Org source** file to learn about available options. I also
added many comments explaining the usage, there.

- generating presentation notes.
- inserting a table of contents with the current section highlighted at
  the beginning of each section.
- configuring transparency of yet uncovered overlay elements.

## Debugging

Look at the pdflatex messages in the buffer named `*Org PDF LaTeX Output*`

You may want to run the TeX compilation interactively with something
like

    pdflatex -shell-escape beamer-example.tex

to get the interactive LaTeX shell help

## Org mode version information

    Emacs version:
    GNU Emacs 24.5.1 (x86_64-unknown-linux-gnu, GTK+ Version 3.10.8)
     of 2015-05-04 on dflt1w

    org version: 8.2.10

## Sources and Links

- I started this example based on [the Worg hosted example by Eric S. Fraga](http://orgmode.org/worg/exporters/beamer/tutorial.html)
- Basic LaTeX Beamer links
  - [An introduction to Beamer (German)](http://www2.informatik.hu-berlin.de/~mischulz/beamer.html)
  - great [beamer reference card](https://github.com/fniessen/refcard-org-beamer) by Fabrice Niessen on GitHub.
  - nice link for choosing a theme: [beamer theme matrix](http://www.hartwork.org/beamer-theme-matrix/)
  - [nice example of beamer features (pure Latex)](http://www.mathematik.uni-leipzig.de/~hellmund/LaTeX/beamer2.pdf)
  - [Presentations using Latex - the Beamer Class](http://www.math.utah.edu/~smith/AmberSmith_GSAC_Beamer.pdf) by Amber Smith. Excellent
    introduction showing many beamer features.

1.  Note

    - an example of a note

## A simple slide

This slide consists of some text with a number of bullet points:

- the first, very **important**, point!
- the previous point shows the use of the special markup which
  translates to the Beamer specific *alert* command for highlighting
  text.

The above list could be numbered or any other type of list and may
include sub-lists.

## A more complex slide

This slide illustrates the use of Beamer blocks. The following text,
with its own headline, is displayed in a block:

1.  Org mode increases productivity

    - org mode means not having to remember commands.
    - it is based on ascii text which is inherently portable.
    - Emacs!

    \$\qed\$

## Tables

The size of the table font can be chosen by giving a `#+LATEX: \small`
command (or `\tiny` or `\footnotesize`)

| WNs | Processors          | Cores/node | HS06/node | total cores | total HS06 |
|-----|---------------------|------------|-----------|-------------|------------|
| 20  | 2\*Xeon X5560       | 8          | 118       | 160         | 2360       |
| 11  | 2\*E5-2670 2.60GHz  | 16         | 263       | 176         | 2893       |
| 4   | 2\*AMD 6272 2.40GHz | 32         | 241       | 128         | 964        |
| 35  |                     |            |           | 464         | 6217       |

## This is a notes page

This is a notes page with some information.

## Exporting beamer presentations

Frequently there is a need to convert a beamer presentation
to MS powerpoint for sharing or contributing slides

1.  The best solution known to me as of 2022 is

    1.  open the PDF using `libreoffice --impress`
    2.  Save as pptx
        - may need to adapt slides or copy content to another
          template

# A collection of example pages

## block environments

1.  a block

        \begin{block}{A block}
        ...
        \end{block}

2.  an alert block

        \begin{alertblock}{An alert block}
        ...
        \end{alertblock}

3.  an example block

        \begin{exampleblock}{An alert block}
        ...
        \end{exampleblock}

## colorbox

1.  a block containing a colorbox

    1.  colboxA

        The beamercolorbox text and an Org example block

            \begin{beamercolorbox}[shadow=true, rounded=true]{eecks}
            ...
            \end{beamercolorbox}

2.  a color box test made with inline LaTex code

## fullframe

A `fullframe` is a `frame` with an ignored slide
title. `frametitle` is set to the empty string

## ignoreheading

- A headline with an `ignoreheading` environment will only have its contents
  displayed in the output. The heading text itself is ignored, and no
  heading bar is shown.
  - Contents are not inserted in any `frame` environment. It makes no sense
    to use this as major element for a slide.
- ignoreheading is useful as a structural element in order to again
  place normal text after a previous element (like a block or a
  column environment).

## `structureenv` environment

1.  structureenv

    - For highlighting text.
    - To help the audience see the structure of your presentation.
    - On this slide you should see that the text of the upper items is
      differently typeset from the bottom item in the *structureenv*.

2.  end of structureenv

    - you need to use `ignoreheading` (like here) in order to then
      insert some more normal text after the structureenv.

## `definition` environment

1.  definition

    Contents of the definition

## `proof` environment and revealing line by line

1.  proof

    - \<1-\| alert@1\> Suppose *p* were the largest prime number.
    - \<2-\> Let *q* be the product of the first *p* numbers.
    - \<3-\> Then *q + 1* is not divisible by any of them.
    - \<4-\> But *q + 1* is greater than *1*, thus divisible by some prime number
      not in the first *p* numbers.

## numbered list over two pages (1)

1.  one
2.  two
3.  three
4.  four

## numbered list over two pages (2)

Use the `[@N]` syntax to start a numbered list at a certain value.

1.  block A

    1.  five
    2.  six
    3.  seven

2.  block B

    1.  eight
    2.  nine
    3.  ten

## long source code over two pages

Use the `allowframebreaks` Beamer option.

``` commonlisp
(use-package python
  :config (progn
            ;; load my own python helper functions
            (load-file (concat dfeich/site-lisp "/my-pydoc-helper.el"))

            (defun dfeich/python-keydefs ()
              (define-key python-mode-map (kbd "<M-right>")
                'python-indent-shift-right)
              (define-key python-mode-map (kbd "<M-left>")
                'python-indent-shift-left))
            (add-hook 'python-mode-hook #'dfeich/python-keydefs)

            ;; show line numbers on the left for python
            (add-hook 'python-mode-hook 'linum-mode)

            (when (featurep 'flycheck)
              (add-hook 'python-mode-hook 'flycheck-mode))

            (use-package jedi-core
              :ensure t
              :config (progn
                        (autoload 'jedi:setup "jedi-core" nil t)
                        (add-hook 'python-mode-hook 'jedi:setup)
                        (setq jedi:complete-on-dot t)
                        (setq jedi:server-args '("--log" "/tmp/jedi.log"
                                                 "--log-level" "INFO"))
                        (when (featurep 'company)
                          (defun dfeich/python-mode-hook ()
                            (add-to-list 'company-backends 'company-jedi)
                            )
                          (add-hook 'python-mode-hook 'dfeich/python-mode-hook))))))
```

## placing text at the bottom of a page

This text is on top

This text is on the bottom

## reducing font size in bullet lists

This is a workaround to have the bullet list hierarchy not suddenly
produce bigger font for the lower hierarchy, if you only reset the
main font.

    #+LATEX: \footnotesize \let\small\footnotesize

- example
  - example
    - example
  - example
- example

## Text colors

Examples for colored text (using the xcolor package):

The basic LaTeX colors are: black, blue, brown, cyan, darkgray,
gray, green, lightgray, lime, magenta, olive, orange, pink, purple,
red, teal, violet, white, yellow.

TODO: The Beamer class loads the `xcolor` package by default. By including
the xcolor option `dvipsnames` in the beamer class definition, we should
also be able to use those names:

    #+LaTeX_CLASS_OPTIONS: [t,10pt,xcolor={dvipsnames}]

But this does not seem to work.

# Animations by overlays

## Highlighting text

The double `@@` can be used to enclose active code. Here we use it to specify
beamer code that will highlight text by specifying an overlay.

A **useful** feature

## Lists

For the first list we use an `#+ATTR_BEAMER: :overlay +-` specification.

It acts like `\begin{itemize}[<+->]`. So, it will cause the
list items to appear one after the other.

- item 1
- item 2
- item 3

For the second list we classify each line by angular brackets to
explicitely define the order of revealing each item.

- \<1-\> item 1
- \<3-\> item 2
- \<2-\> item 3

## Basic revealing of blocks using BEAMER\_act

1.  First Block

    - this is visible from the beginning

2.  Second Block

    - and this one is revealed afterwards by using the BEAMER\_act
      keyword in the PROPERTIES section.

## revealing a picture

A picture will be uncovered next

## Explicitely defining the transparancy of covered text

1.  First Block

    - this is visible from the beginning

2.  Second Block

    - this is initially invisible since we used
      `\setbeamercovered{invisible}` for this frame
    - then it is revealed again using the BEAMER\_act
      keyword in the PROPERTIES section.

## different transparency setting and default overlay

1.  First Block

    this is visible from the beginning. Note that we specified another
    transparency compared to the previous slide.

2.  Second Block

    Initial visibility defined by `\setbeamercovered{transparent=30}`.

3.  Third Block

    And a third block

## dynamic transparency setting and default overlay

1.  First Block

    this is visible from the beginning. We defined `\setbeamercovered{highly dynamic}`
    so that other blocks are slowly getting less transparent.

2.  Second Block

    a second block

3.  Third Block

    And a third block

4.  Fourth Block

    And a fourth block

## plain text between two blocks

1.  block 1

    The first block

2.  ign

    behavior by using `#+LATEX: \onslide<2->` in front of the paragraph.

3.  block 2

    The second block

# Multiple Columns

## Blocks in two columns

1.  A left block

    - this slide consists of two columns
    - This is the first column

2.  A right block

    - this is the right column

## A text section and a figure

1.  A text section

    - this slide consists of two columns
    - the first (left) column has no heading and consists of text
    - the second (right) column has an image and is enclosed in an
      **example** block

2.  A screenshot

## A centered text section and a figure

1.  A centered text section

    - a centered text section. I found no good way for
      using `\vfill` or `\minipage` as referenced [here](http://tex.stackexchange.com/questions/15244/why-does-vfill-not-work-inside-a-beamer-column)

2.  A screenshot

## Babel

1.  Octave code

    ``` octave
    A = [1 2 ; 3 4]
    b = [1; 1];
    x = A\b
    ```

2.  The output

        A =

           1   2
           3   4

        x =

          -1
           1

# Conclusions

## Summary

- org is an incredible tool for time management
  - it is also excellent for composing documents
- Beamer is a very powerful package for presentations
- the combination is unbeatable: Org Beamer
  - ease of composing slides fast and being able to use all the other Org features
  - though, it takes a bit of a learning curve and examples to copy from

# Appendix

## Appendix

SOME BACKUP SLIDES. The Appendix will not be listed in the table of contents.

## Backup slide 1

Some backup info

## Backup slide 2

These details are not part of the main talk.