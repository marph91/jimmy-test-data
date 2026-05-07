# c-babel

Derek

\<2014-10-20 Mon\>

# Links

- <http://orgmode.org/worg/org-contrib/babel/languages/ob-doc-C.html>

# Compiler version

``` bash
gcc --version
```

    gcc (Ubuntu 4.8.2-19ubuntu1) 4.8.2
    Copyright (C) 2013 Free Software Foundation, Inc.
    This is free software; see the source for copying conditions.  There is NO
    warranty; not even for MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.

# test

Both C and C++ get activated by adding `C` to the `org-babel-load-languages`.

If there is no main function present, babel will wrap one around the code. It also
will add some of the standard include files needed to compile the code.

``` c
printf("Hello World");
```

    Hello World

The equivalent example with explicitely writing the include and the main function.

``` c
#include "stdlib.h"
int main(int argc,char **argv) {
  printf("Hello World");
  exit(0);
}
```

    Hello World

# Passing variables by header arguments

## passing simple types

``` c
printf ("mystring %s\n", mystring);
printf ("myint    %d\n", myint);
printf ("mydouble %g\n", mydouble);
```

    mystring Sunday
    myint    145
    mydouble 3.14

Using CALL to call the source block as a function

    mystring Monday
    myint    20
    mydouble 1.5

An example with C++ and including a header file using the `:includes` header argument. Note
that one can look at the resulting code before compilation by using `org-babel-expand-src-block`
(by default assigned to `C-c C-v v`)

    std::cout << "Hello World!\n";

    Hello World!

## passing a table

| nb    | sqr | noise |
|-------|-----|-------|
| zero  | 0   | 0.23  |
| one   | 1   | 1.31  |
| two   | 4   | 4.61  |
| three | 9   | 9.05  |
| four  | 16  | 16.55 |

The following code only works if the `string.h` header is included via the header. Even
though the src block does not require a function from that library by itself, the boiler
plate code inserted by babel to parse the table uses `strncmp`. The boiler plate code
gets inserted before the source block, so includes defined within the source block
are read in too late. But the includes defined through the header arguments are inserted
before the boiler plate.

This I consider a bug which I should report to the developers.

    int main()
     {
       for(int j=0; j<somedata_cols; j++) { printf("%s  ", somedata_header[j]); };
       printf("\n");
       for (int i=0; i<somedata_rows; i++) {
         printf ("%2d %7s ", i, somedata_h(i,"nb"));
         for (int j=1; j<somedata_cols; j++) {
           const char* cell = somedata[i][j];
           printf ("%5s %5g ", cell, 1000*atof(cell));
         }
         printf("\n");
       }
       return 0;
     }

    nb  sqr  noise  
     0    zero     0     0  0.23   230 
     1     one     1  1000  1.31  1310 
     2     two     4  4000  4.61  4610 
     3   three     9  9000  9.05  9050 
     4    four    16 16000 16.55 16550

# noweb syntax

First we define named code blocks

``` c
void myfunc() {
  printf("print from function\n");
}
```

``` c
int main(int argc,char **argv) {
  printf("Hello World\n");
  myfunc();
  exit(0);
}
```

Now we define a block which includes the other code blocks (needs
the :noweb yes option). We could tangle this block, but we can also
execute it directly.

``` c
#include "stdlib.h"
#include "stdio.h"

<<srcMyfunc>>
<<srcMain>>
```

    Hello World
    print from function

# C++11 examples

Passing multiple `includes` requires defining them within a list.
ERROR: Why can I not use the `:results output` syntax?

    std::vector<std::complex<double>> v{{0,0}, {1,0}, {0,1}};
    for (auto &iter: v) {
      std::cout << iter << ' ';
     }

    (0,0) (1,0) (0,1)

An example with lambda functions

    using namespace std;

    float vf0[5] = {1.2, 3.4, 5.1, 8.4, 9.9};
    function<void(float&)> out =  {cout << f << ' '; };
    // function<void(float&)> mult = [&fac](float &f) {f* = fac; };

    for_each(vf0, vf0+5, out);
    cout << " (vf0)\n";

Local Variables:
org-confirm-babel-evaluate: nil
End: