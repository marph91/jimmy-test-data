# Ditaa org babel examples

Derek

\<2015-07-26 Sun\>

# Documentation and links

- [Ditaa on sourceforge](http://ditaa.sourceforge.net)
- Drawin is mostly done in Emacs **Artist mode**
  - when using C-c ' `org-edit-special` the edit buffer is placed in
    artist mode
  - [emacs help page on artist mode](help:artist-mode)
  - [nice screencast by Seong-Kook Shin](http://www.cinsk.org/emacs/emacs-artist.html)
  - when drawing using the keys
    - **polyline**: `return` will begin a line, `C-u return` will end

  the polyline
  - **cut**: `C-c C-a C-k` for entering cut mode. Hit `return` to start

  opening a rectangle. Hit `Return` again for cutting the rectangle.
  - **paste**: `C-c C-a M-w` for entering past mode. Hit `return` for

  pasting.

# Information on local installation

    Emacs variable org-plantuml-jar-path:/home/dfeich/.emacs.d/javalib/ditaa/ditaa.jar


    ditaa version 0.9, Copyright (C) 2004--2009  Efstathios (Stathis) Sideris

    usage: java -jar ditaa.jar <inpfile> [outfile] [-A] [-d] [-E] [-e
           <ENCODING>] [-h] [--help] [-o] [-r] [-s <SCALE>] [-S] [-t <TABS>]
           [-v]
     -A,--no-antialias          Turns anti-aliasing off.
     -d,--debug                 Renders the debug grid over the resulting
                                image.
     -E,--no-separation         Prevents the separation of common edges of
                                shapes.
     -e,--encoding <ENCODING>   The encoding of the input file.
     -h,--html                  In this case the input is an HTML file. The
                                contents of the <pre class="textdiagram"> tags
                                are rendered as diagrams and saved in the
                                images directory and a new HTML file is
                                produced with the appropriate <img> tags.
        --help                  Prints usage help.
     -o,--overwrite             If the filename of the destination image
                                already exists, an alternative name is chosen.
                                If the overwrite option is selected, the image
                                file is instead overwriten.
     -r,--round-corners         Causes all corners to be rendered as round
                                corners.
     -s,--scale <SCALE>         A natural number that determines the size of
                                the rendered image. The units are fractions of
                                the default size (2.5 renders 1.5 times bigger
                                than the default).
     -S,--no-shadows            Turns off the drop-shadow effect.
     -t,--tabs <TABS>           Tabs are normally interpreted as 8 spaces but
                                it is possible to change that using this
                                option. It is not advisable to use tabs in
                                your diagrams.
     -v,--verbose               Makes ditaa more verbose.

# Ditaa tests

``` ditaa

+--------+   +-------+    +-------+
|        | --+ ditaa +--> |       |
|  Text  |   +-------+    |diagram|
|Document|   |!magic!|    |       |
|     {d}|   |       |    |       |
+---+----+   +-------+    +-------+
    :                         ^
    |       Lots of work      |
    +-------------------------+
```

The following graph contains all available default shapes. The available shapes can be
seen in the [source code](https://github.com/stathissideris/ditaa/blob/master/src/org/stathissideris/ascii2image/graphics/Diagram.java).

``` ditaa

+----------------------+         +------------------+----+
| This is a box   |    +---------+  and this is     |    |
|                 |    |         |  another         |    |
|                 |    |         |                  |    |
|                 |    |         |                  |    |            +-------+
+-------+--------------+         +------------------+----+        |       |
        |                                 |       |
        |                                 | {mo}  |
        :           /------------------------------\      |      ^    +-------+
        |           |                              |      |      |
        |           |   and yet another, but       |      |      |
        +---------->+   with round corners         |      |      |    +-------+
                    |   o list item 1              |      |      |    |       |
                    |   o list item 2              |      |      |    |       |
                    \------------------------------/      V      |    | {tr}  |       
                                                                      +-------+       

  +----------+       +--------------+       +---------------+    +-------+    +-------+
  | Storage  |       | Document     |       | Input/Output  |    |       |    |       |
  |          |       |              |       |               |    |       |    |       |
  | cGRE     +-------+ cYEL         +---=---+ cRED          |    | {o}   |    | {c}   |
  |          |       |              |       |               |    +-------+    +-------+
  | {s}      |       | {d}          |       | {io}          |
  +----------+       +--------------+       +---------------+

```

Example from <http://doc.norang.ca/org-mode.html#playingwithditaa>

``` ditaa
    +-----------+        +---------+
    |    PLC    |        |         |
    |  Network  +<------>+   PLC   +<---=---------+
    |    cRED   |        |  c707   |              |
    +-----------+        +----+----+              |
                              ^                   |
                              |                   |
                              |  +----------------|-----------------+
                              |  |                |                 |
                              v  v                v                 v
      +----------+       +----+--+--+      +-------+---+      +-----+-----+       Windows clients
      |          |       |          |      |           |      |           |      +----+      +----+
      | Database +<----->+  Shared  +<---->+ Executive +<-=-->+ Operator  +<---->|cYEL| . . .|cYEL|
      |   c707   |       |  Memory  |      |   c707    |      | Server    |      |    |      |    |
      +--+----+--+       |{d} cGRE  |      +------+----+      |   c707    |      +----+      +----+
         ^    ^          +----------+             ^           +-------+---+
         |    |                                   |
         |    +--------=--------------------------+
         v
+--------+--------+
|                 |
| Millwide System |            -------- Data ---------
| cBLU            |            --=----- Signals ---=--
+-----------------+
```

``` ditaa

+---+    +----+    +---+                                   
|   |    |    |    |   |          +--+  +--+               
|   +----+    +----+   |          |  |  |  |               
|                      |     -----+  +--+  |       +------*
|      some shape      |                   |       |
| cRED                 |           +----*-------*--+
+----------------------+     ------+
```

# Problems

- characters which are used as graphic elements get interpreted within text, e.g "1-100" will
  end up with the "-" being rendered as a line segment.
  - workaround: Use similar looking UTF-8 characters

    | Instead of | UTF-8 char |
    |------------|------------|
    | \-         | EM DASH    |