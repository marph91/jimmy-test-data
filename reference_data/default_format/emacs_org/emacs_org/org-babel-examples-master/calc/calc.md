# calc examples

Derek Feichtinger

# Version information

``` commonlisp
(princ (concat (format "Emacs version: %s\n" (emacs-version))
               (format "org version: %s\n" (org-version))))
```

    Emacs version: GNU Emacs 26.2 (build 2, x86_64-pc-linux-gnu, GTK+ Version 3.22.30)
     of 2019-04-14
    org version: 9.3.7

# General

- refer to the [Calc info pages](info:calc#Top)
- Note that, unlike in usual computer notation, multiplication binds
  more strongly than division: \`a\*b/c\*d' is equivalent to
  \`(a\*b)/(c\*d)'
- [Nice reference sheet](https://github.com/SueDNymme/emacs-calc-qref) on calc maintained by Sue D. Nymme

# babel Calc

Not too useful, yet. Embedded calc certainly is better for
inlining math in documents. Using Elisp to directly interacting with
calc also is more powerful.

``` calc
24
3
'/
```

    8

- solving an equation

  ``` calc
  fsolve(x*2+x=4,x)
  ```

      x = 1.33333333333

- solving a linear system of equations

  ``` calc
  fsolve([x + y = a, x - y = b],[x,y])
  ```

      [x = a + (b - a) / 2, y = (a - b) / 2]

# embedded calc

We can assing variables using the ":=" syntax. Each formula can be
evaluated using `C-x * u` (calc-embedded-update-formula). When
opening a buffer with such formulas, using `C-x * a`
(calc-embedded-activate) will activate all formulas found in the
buffer (it may be preferrable to even place a local variable
definition with `eval:(calc-embedded-activate)` at the end of the
file).

$varA := 5$
$varB := 2$
$varA + varB => 7$

A formula on a line surrounded by new lines is recognized without specific
opening and closing characters. Evaluating it moves it into the first column
for some reason (loss of indentation)

varC := 35

$varA + varB + varC => 42$

varC + varA =\> 40

$[1, 0, 1] + [2, 2, 2] => [3, 2, 3]$

Solving a system of equations
$solve([x + y = 10, x - y = 8], [x, y]) => [x = 9, y = 1]$

$solve([x + y = 6, x - y = 10], [x, y]) => [x = 8, y = -2]$

# Calc from lisp

- [Emacs Info Manual: Calling Calc from your programs](info:calc#Calling%20Calc%20from%20Your%20Programs)
- nice blog post on [RSA cryptography using emacs Calc](http://nullprogram.com/blog/2015/10/30/) by Chris
  Wellons on his [nullprogram](http://nullprogram.com/) blog. Contains examples on `calc-eval`
  usage.

## basic use of calc-eval

The variables in formulas are replaced by the additional arguments. Arguments can be given as string or number.

``` commonlisp
(print (calc-eval "2^$1 - 1 + $2" nil 3 5))
(print (calc-eval "2^$1 - 1" nil 128))

(print (calc-eval "$1 < $2" 'pred "4000" "5000"))
(print (calc-eval "$1 > $2" 'pred "4000" "5000"))
(print (calc-eval "$1 < $2" nil "4000" "5000"))
(print (calc-eval "$1 > $2" nil "4000" "5000"))
(print (calc-eval "nextprime($1)" nil "100000000000000000"))

;; radix can be chosen by separating radix by # from number
(print (calc-eval "16#deadbeef"))
(print (calc-eval "2#1111"))
```


    "12"

    "340282366920938463463374607431768211455"

    t

    nil

    "1"

    "0"

    "100000000000000003"

    "3735928559"

    "15"

The second argument serves as a separator if the result is a list of expressions. By default the list
is printed comma-separated.

``` commonlisp
(print (calc-eval "10+5, 7*3, 5/2"))
(print (calc-eval "10+5, 7*3, 5/2" ";"))
(print (calc-eval "10+5, 7*3, 5/2" "___"))
```


    "15, 21, 2.5"

    "15;21;2.5"

    "15___21___2.5"

## using calc-eval to supply raw calc objects as input to calc internal functions

calc internal functions deal with *raw* calc objects. These can also be obtained through `calc-eval` by
passing the `raw` as the second argument.

``` commonlisp
(calc-eval (math-convert-units (calc-eval "10 m" 'raw)
                               (calc-eval "ft" 'raw)))
```

    32.8083989501 ft

``` commonlisp
(calc-eval (math-simplify-units (calc-eval "10 m + 1 mm" 'raw)))
```

    10.001 m

Todo: I do not know how the second arg to math-to-standard-units is used. Nil
works as well as any other list, it seems.

``` commonlisp
(calc-eval
 (math-to-standard-units
  (calc-eval "5 J" 'raw) nil))
```

    5000 g m^2 / s^2

## math-read-exprs returns the AST of an expression

To understand the lisp expressions that will get executed to obtain
a result, one can use the `math-read-exprs` function. It returns an
AST of the expression.

``` commonlisp
(math-read-exprs "5 * 6 - 20")
```

    ((- (* 5 6) 20))

``` commonlisp
(math-read-exprs "x=vsum(1, 2, 3)")
```

    ((calcFunc-eq (var x var-x) (calcFunc-vsum 1 2 3)))

Lets try executing the lisp (note that the result is enclosed by an
extra parentheses).

``` elisp
(calcFunc-eq '(var x var-x) (calcFunc-vsum 1 2 3))
```

    (calcFunc-eq (var x var-x) 6)

``` elisp
(calc-eval (calcFunc-eq '(var x var-x) (calcFunc-vsum 1 2 3)))
```

    "x = 6"

## Stack operations: push, pop and top

- `push` pushes the element onto the stack
- `pop` deletes as many elements from the stack as the preceding integer argument indicates
  - `0 pop` is convenient for finding out the size of the stack
- `top` retrieves the value at the indicated position of the stack

``` commonlisp
(princ (format "Size of the stack: %s\n" (calc-eval 0 'pop)))
(calc-eval "10 ft" 'push)
(calc-eval "20 ft" 'push)
(calc-eval "30 ft" 'push)
(princ (format "After 3*push: Size of the stack: %s (top element: %s)\n"
               (calc-eval 0 'pop)
               (calc-eval 1 'top)))
(princ (format "element on second level of stack: %s\n" (calc-eval 2 'top)))
(calc-eval 2 'pop)
(princ (format "After 3*push: Size of the stack: %s (top element: %s)\n"
               (calc-eval 0 'pop)
               (calc-eval 1 'top)))
(calc-eval 1 'pop)
```

    Size of the stack: 5
    After 3*push: Size of the stack: 8 (top element: 30 ft)
    element on second level of stack: 20 ft
    After 3*push: Size of the stack: 6 (top element: 10 ft)

## executing functions on the stack

``` commonlisp
(calc-eval "10 ft" 'push)
(calc-base-units)
;; retrieve the value from the stack as a string. Note that it still stays on the stack!
(print (calc-eval 1 'top))
;; clean the value from the stack
(calc-eval 1 'pop)
```


    "3.048 m"

It is also possible to execute Calc keyboard macros, i.e. the string is interpreted as
interactive keyboard strokes in calc mode.

``` commonlisp
(calc-eval "10 ft" 'push)
;; calc keys for base unit conversion
(calc-eval "ub" 'macro)
(print (calc-eval 1 'top))
;; pop one item from stack
(calc-eval "\C-d" 'macro)
```


    "3.048 m"

## Some other examples of using calc in lisp

``` commonlisp
(princ
 (format "%s  %s"
    (calc-eval "deg(37@ 26' 36.42)")
    ;; now using pure lisp
    (math-format-number
     (calcFunc-deg '(hms 37 26 (float 3642 -2))))))
```

    37.44345  37.44345

# Org configurations for Calc

- <https://emacs.stackexchange.com/questions/59179/specify-precision-using-calc-in-org-mode-spreadsheets/59181#59181>
  The variable org-calc-default-modes is used to customize Calc for org usage

  ``` elisp
  (defcustom org-calc-default-modes
    '(calc-internal-prec 12
               calc-float-format  (float 8)
               calc-angle-mode    deg
               calc-prefer-frac   nil
               calc-symbolic-mode nil
               calc-date-format (YYYY "-" MM "-" DD " " Www (" " hh ":" mm))
               calc-display-working-message t)
    "List with Calc mode settings for use in `calc-eval' for table formulas.
  The list must contain alternating symbols (Calc modes variables and values).
  Don't remove any of the default settings, just change the values.  Org mode
  relies on the variables to be present in the list."
    :group 'org-table-calculation
    :type 'plist)
  ```

# Calc usage in tables

## Unit conversions by defining new functions with defmath

- from <http://article.gmane.org/gmane.emacs.orgmode/93489>

Displaying all calc units in a buffer can be obtained by executing

Calc preserves units and variables in table operations.

| distance | time   | speed       |     |
|----------|--------|-------------|-----|
| 3 km     | 2.5 hr | 1.2 km / hr |     |

| speed        | simplified speed |
|--------------|------------------|
| 40km / 2.5hr | 16\. km / hr     |

We can also decide to use calc via its elisp api. To understand
the following lisp formula that involves calc internal functions
q.v. the *Calc from lisp* section.

| km    | ft      |
|-------|---------|
| 2.5km | 8202.10 |

Defining a new calc function for unit conversion with defmath

``` commonlisp
(defmath uconv (expr target-units &optional pure)
  (math-convert-units expr target-units pure))
```

    calcFunc-uconv

| km     | ft           |
|--------|--------------|
| 2.5 km | 8202.0997 ft |

Using the units from the table header (if the 3rd arg is given to
uconv, the output is stripped of the unit):

| km  | ft        |
|-----|-----------|
| 2.5 | 8202.0997 |

The standard calc function usimplify also works for this use
case:

| km  | ft        |
|-----|-----------|
| 2.5 | 8202.0997 |

A lisp equivalent of the above

``` elisp
(calc-eval "usimplify(2.5 km / ft)")
```

    8202.09973753

Let's define a function that converts to base units

``` elisp
(defmath ustd (expr) (math-simplify-units (math-to-standard-units expr nil)))
```

    calcFunc-ustd

| distance | time   | speed       | std unit speed   | speed in ft/s    |
|----------|--------|-------------|------------------|------------------|
| 3 km     | 2.5 hr | 1.2 km / hr | 0.33333333 m / s | 1.0936133 ft / s |

# Some standard Calc functions that can be used in formulas

- <info:calc#Formulas>
- factorial: \$6! =\> 720 \$ also fact(6) can be used in writing
- find: \$ find(\[5, 6, 7, 8\], 6) =\> 2 \$
- power: \$pow(2, 3) =\> 8 \$ \$2^3^ =\> 8 \$
- modulo: $mod(10, 3) => 1$ \$10 % 3 =\> 1 \$
- binomial coefficient: $choose(3, 2) => 3$
- random numbers: $random(10) => 7$
- binomial distribution: the result (\`utpb(x,n,p)') is the
  probability that an event will occur X or more times out of N
  trials, if its probability of occurring in any given trial is P:
  $utpb(2, 6, 1/6) => 0.263224451304$
- gaussian distribution with mean m and stdev s. Probability that a normal
  distributed random variable will exceed x: uttn(x,m,s):
  $utpn(0.2b, 0, 0.5) => 0.34457825839$
  - <http://www-zeuthen.desy.de/~kolanosk/smd_ss02/skripte/>
- prime factorisation \$ prfac(9370) =\> \[2, 5, 937\] \$

## Time calculations

q.v. [info:calc#Date Arithmetic](info:calc#Date%20Arithmetic)

- $now(0) => <11:03:18pm Sun Aug 11, 2013>$
- \$now() =\> \<10:48:31pm Wed Jun 28, 2017\> \$
- Using calc HMS forms
  - \$ 11@ 41' 15.561" - 11@ 40' 58.096" =\> 0@ 0' 17.465" \$
- The date function with a date form as argument returns a number of days since Jan 1, 1 AD.
  The date function with an INT argument yields back a date form.
  - \$date() =\> 735091 \$
  - \$date(735091) =\> \$
  - \$date(\<10:00am Sun Aug 11, 2013\>) =\> 735091.416667 \$
  - \$date() - date() =\> 10 \$
  - \$ - =\> 10 \$
  - \$date(\<10:00am Sun Aug 11, 2013\>) - date(\<9:00am Thu Aug 1, 2013\>) =\> 10.041667 \$
- The date function with a comma separated list builds a date or a date/time form
  - \$date(2017, 6, 26) =\> \$
  - \$date(2017, 6, 26, 11@ 41' 15.561") =\> \<11:41:16am Mon Jun 26, 2017\> \$
  - \$date(2017, 6, 26, 11, 41, 15) =\> \<11:41:15am Mon Jun 26, 2017\> \$
  - Not quite clear whether the angular bracket format is any good for more exact calculations
    - \$ \<11:03:18pm Sun Aug 11, 2013\> - \<11:03:18pm Sun Aug 11, 2013\> =\> 0. \$
    - \$ \<11:03:18pm Sun Aug 11, 2013\> - \<11:02:18pm Sun Aug 11, 2013\> =\> 6.94e-4 \$
    - \$ \<11:03:18pm Sun Aug 11, 2013\> - \<11:03:17pm Sun Aug 11, 2013\> =\> 1.2e-5 \$
    - \$ \<11:03:18pm Sun Aug 11, 2013\> - \<6:03:18pm Sun Aug 11, 2013\> =\> 0.208333 \$
- Unix time
  - \$unixtime(\<9:00am Wed Jun 28, 2017\>) =\> 1498640400 \$
  - \$unixtime(1498640400) =\> \<9:00am Wed Jun 28, 2017\> \$
  - $unixtime(now(0)) => 1376262280$
- Julian date
  - \$julian(date(2017, 6, 26)) =\> 2457929 \$
  - \$julian(2457929) =\> \$
- Using a calc variable
  - \$ testdate := \<11:41:15am Mon Jun 26, 2017\> \$

  - \$ year(testdate) =\> 2017 \$

    \$ date(date() - 10) =\> \$