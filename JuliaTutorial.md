# Julia Tutorial #

Note that some terminologies may be slightly different from those from
the [Julia Documentation](http://docs.julialang.org/en/latest/).  It
depends on my understanding and my opinions about what is a better
mnemonic.

* [Introduction](#introduction)
* [Installation](#installation)
  + [On Ubuntu](#on-ubuntu)
    - [Additional software](#additional-software)
	  * [IJulia](#ijulia)
  + [On Mac](#on-mac)
  + [On Windows](#on-windows)
* [A quick tour of Julia](#a-quick-tour-of-julia)
  + [Enter and quit Julia interactive session](#enter-and-quit-julia-interactive-session)
  + [Something special to the REPL](#something-special-to-the-repl)
  + [Get help in REPL](#get-help-in-repl)
  + [Play with Julia script file and command line](#play-with-julia-script-file-and-command-line)
  + [Run shell command in Julia](#run-shell-command-in-julia)
  + [Comment code](#comment-code)
  + [Variables](#variables)
    - [Some special internal variables](#some-special-internal-variables)
  + [Built-in numeric primitives](#built-in-numeric-primitives)
  + [Array](#array)
  + [String](#string)
  + [Regular Expressions](#regular-expressions)
  + [Elementary mathematical operations and functions](#elementary-mathematical-operations-and-functions)
  + [Support for complex and rational numbers](#support-for-complex-and-rational-numbers)
  + [Control flow](#control-flow)
    - [if-elseif-else-end](#if-elseif-else-end)
	- [while and for loops](#while-and-for-loops)
  + [Compound expressions](#compound-expressions)
  + [Function](#function)
    - [Return multiple values](#return-multiple-values)
	- [Optional positional and keyword arguments](#optional-positional-and-keyword-arguments)
  + [Special ellipsis "..." symbol](#special-ellipsis--symbol)
  + [Variable scope](#variable-scope)
    - [let...end](#letend)
	- [Special note](#special-note)
  + [Operators](#operators)
	- [Special note for logical operators](#special-note-for-logical-operators)
  + [Types](#types)
    - [Type declaration](#type-declaration)
    - [Abstract types](#abstract-types)
	  * [Type unions](#type-unions)
	- [Concrete types](#concrete-types)
	  * [Composite types](#composite-types)
	- [Parametric types](#parametric-types)
	- [Type aliases](#type-aliases)
	- [Useful functions operate on types](#useful-functions-operate-on-types)
  + [Methods](#methods)
    - [Useful functions operate on methods](#useful-functions-operate-on-methods)
  + [Constructors](#constructors)
  + [Tasks](#tasks)
  + [Exception handling](#exception-handling)
* [Write your own package](#write-your-own-package)
* [Some interesting facts](#some-interesting-facts)
  + [The number of available packages](#the-number-of-available-packages)
* [Useful resources](#useful-resources)

## Introduction ##

[Julia](http://julialang.org/) is a fast dynamic programming language
for technical computing.  With modern language design and compiler
techniques, Julia aims to create an unprecedented combination of
easy-to-use, power, and efficiency in a single language, providing
ease and expressiveness in the same way as languages such as R and
Python, and also good performance like C.

## Installation ##

More specific details can be found at
[Julia Downloads](http://julialang.org/downloads/) and
[Platform Specific Instructions for Installing Julia](http://julialang.org/downloads/platform.html).

### On Ubuntu ###

To install Julia on Ubuntu, one need to use the
[Julia PPA (Personal Package Archives)](https://launchpad.net/~staticfloat).

#### Install stable version ####

To install the current stable version of Julia, one need to use the
[Julia Releases PPA](https://launchpad.net/~staticfloat/+archive/ubuntu/juliareleases)
to sync with the latest stable version of Julia (See
[Julia Downloads](http://julialang.org/downloads/) and
[Installation of Juno, The Julia IDE](http://junolab.org/docs/install.html)
for more details). (**Note**: In this tutorial, we use "**$**" like
below as the prompt for shell.)

```Shell
$ sudo add-apt-repository ppa:staticfloat/juliareleases
$ sudo add-apt-repository ppa:staticfloat/julia-deps
$ sudo apt-get update
$ sudo apt-get install julia
```

#### Install development version ####

Development version means the version of Julia is under heavy
development and one might encounter various problems during usage.
However, it brings new functionlities and features one might want to
try.  To install the development version of Julia, one need to use the
[Julia Nightlies PPA](https://launchpad.net/~staticfloat/+archive/ubuntu/julianightlies).

```Shell
$ sudo apt-add-repository ppa:staticfloat/julianightlies
$ sudo apt-add-repository ppa:staticfloat/julia-deps
$ sudo apt-get update
$ sudo apt-get install julia
```


#### Additional software ####

##### IJulia #####

To use [IJulia](https://github.com/JuliaLang/IJulia.jl), you have to
install [IPython](http://ipython.org/) first (See
[Installing IPython](http://ipython.org/install.html) for more
details.):

```Shell
$ sudo apt-get install ipython-notebook python-matplotlib \
                       python-scipy python-pandas \
                       python-sympy python-nose
```

Thereafter, in shell terminal, enter:

```Shell
$ julia
```

to get into a Julia command line session, within which type:
(**Note**: In this tutorial, we use "**julia>**" like below as the
prompt for Julia)

```Julia
julia> Pkg.update()
julia> Pkg.add("IJulia")
julia> Pkg.add("PyPlot")
```

to install IJulia and related packages, and type **Ctrl-d** to quit
the session.  Finally, you can type in shell terminal:

```Shell
$ ipython notebook --profile julia
```

to run Julia in IJulia notebook.


### On Mac ###

### On Windows ###


## A quick tour of Julia ##

### Enter and quit Julia interactive session ###

In shell terminal, just type:

```Shell
$ julia
```

to get into the interactive session of Julia, within which you type:

```Julia
julia> quit()
```

or **Ctrl-d** to quit back to shell.


### Something special to the REPL ###

1.  Once you have typed a complete expression, pressing **Enter** will
    get the expression be evaluated and the value will be printed out.

2.  A trailing semicolon `;` will suppress the output for the
    evaluated value.

3.  However, you can use the variable `ans`, which is only available
    in REPL, to get the value of the last evaluated expression, no
    matter if it is suppressed or not.

4.  You can type `julia -q` to suppress the display of startup
    banner (like below) when lauch the REPL.

    ```
                   _
       _       _ _(_)_     |  A fresh approach to technical computing
      (_)     | (_) (_)    |  Documentation: http://docs.julialang.org
       _ _   _| |_  __ _   |  Type "help()" to help.
      | | | | | | |/ _` |  |
      | | |_| | | | (_| |  |  Version 0.3.5 (2015-01-08 22:33 UTC)
     _/ |\__'_|_|_|\__'_|  |  Official http://julialang.org release
    |__/                   |  x86_64-linux-gnu
    
    ```

5. For more about command **julia** itself, just type:

   ```Shell
   $ julia --help
   ```

### Get help in REPL ###

With the `help()` function, one can query the documentation for a
specific function, macro, or variable.  For example,

```Julia
julia> help(println)
```

Alternatively, we can use `?` as a short hand for the `help()`
function:

```Julia
julia> ?println
```

If you are not sure how to use `help()`, just type:

```Julia
julia> ?help
```

for more details.

`apropos()` is a more flexible function that can be used to search
documentation for functions related to a specific string.  For
example, if one want to find out what functions there are to do with
"string", one can type:

```Julia
julia> apropos("string")
```

And the blog [Julia Helps](http://www.juliabloggers.com/julia-helps/)
gives a good summary about getting help from Julia itself.


### Play with Julia script file and command line ###

A Julia script file has **.jl** as its extension.

1.  To execute the code in a Julia script file within a Julia
    interactive session, we use function `include()`.  For example,
    if we have a script named **hello.jl** with the following
    contents:

    ```Julia
	# hello.jl
    println("Hello, world!")
    ```

    then in a Julia session, type:

    ```Julia
    julia> include("hello.jl")
    ```

    `Hello, world!` will be printed out.

2.  To execute a Julia script in shell, for example, previous
    **hello.jl**, type:

    ```Shell
    $ julia hello.jl
    ```

3.  To execute a short code within shell command line, we could use
    the option `-e` for command `julia`:

    ```Shell
    $ julia -e 'println("Hello, world!")'
    ```

4.  To execute a Julia script in shell with one or more command line
    arguments, Julia provides `ARGS` for holding the arguments
    passed from command line.  For example, we have a script named
    **hello2.jl**:

    ```Julia
	# hello2.jl
    println("Hello, ", ARGS[1], "!")
    ```

    then in shell, type:

    ```Shell
    $ julia hello2.jl Simon
    ```

    will output `Hello, Simon!`.

5. Or one can also provide command line arguments for short code
   expressions:
   
   ```Shell
   $ julia -e 'println("Hello, ", ARGS[1], "!")' Simon
   ```

   which has the same output as above.

### Run shell command in Julia ###

A shell command should be wrapped in backticks "**`**", and we can use
function `run()` to run the command within them.  For example,

```Julia
julia> run(`echo Hello`)
Hello
```

However, the output will automatically be dumped to the screen.  We
can assign the output to a variable by function `readall()`:

```Julia
julia> a = readall(`echo Hello`)
"Hello\n"

julia> a
"Hello\n"
```


### Comment code ###

1.  In a single Julia script line, everything behind a `#` is
    considered as comment.

2.  `#=` and `=#` are used for multi-line comments.


### Variables ###

Like other languages, variable names in Julia must also begin with a
letter in English alphabet, underscore, or a subset of Unicode code
points greater than 00A0.

As a dynamic programming language, there is no restriction for a
variable in Julia to be of a fixed type after introduced in a scope.
In other words, a variable can be assigned to a value of different
type from its previous one, except that in a local scope we can add a
type annotation to a variable to restrain it from being assigned to a
value of a different type.

**Note**: When in the REPL, we are in a global scope, and a variable
defined in a function is in a local scope.

Examples:

```Julia
x = 1            # introduce a varialbe named x
x += 1           # now x equals to 2
x = "Hello"      # x is re-assigned to a string "Hello"

function foo()
  x::Int32 = 10  # prevent x from being assigned to values of non-Int32
end
```

For expressiveness, one can use Unicode names (in UTF-8 encoding) as
variable names, which, I think, is good for math symbols.  One can
enter these math symbols by typing the backslash LaTeX symbol name
followed by Tab.  For example, δ can be entered by typing "\delta"
and followed by Tab key.

```Julia
julia> δ = 0.125
0.125

julia> δ
0.125
```

#### Some special internal variables ####

|Variable|Description|Example|
|:-------|:----------|:------|
|`WORD_SIZE`|Indicate whether the target system is 32-bit or 64-bit||


### Built-in numeric primitives ###

For basic arithmetic, Julia provides a series of built-in numeric
types, with explicit names telling how many bits they use to represent
a number:

```Julia
# Unsigned integers can be represented by 0x followed by hexadecimal
# digits, or 0b followed by binary digits, or 0o followed by octal
# digits, such as 26 can be represented as 0x1a, 0b11010, or 0o32.
Int8        Uint8
Int16       Uint16
Int32       Uint32
Int64       Uint64
Int128      Uint128

Bool  # false or true with 8 bits

Char # Unicode characters with 32 bits, denoted by enclosing printable
     # characters in single quotes, such as 'x', or escaped '\u' or
     # '\U' hexadecimal input forms, such as '\u78', which is the
     # same as 'x'.

# There is no type named Double as in other programming languages
Float64  # Floating-point numbers are by default of type Float64, such as 25, 2.5e1
Float32  # numbers of type Float32 can be represented by writing an 'f' in place of 'e', such as 2.5f1
Float16
```

A few useful functions that can work with these basic built-in types:

|Function|Description|Example|
|:-------|:----------|:------|
|`typeof(x)`|The exact concrete type of `x`|`typeof(10.04)` returns `Float64`|
|`typemin(x)`|The lowest value representable by the given numeric type|`typemin(Int32)` returns `-2147483648`|
|`typemax(x)`|The highest value representable by the given numeric type|`typemax(Int32)` returns `2147483647`|
|`bits(x)`|A string giving the literal bit representation of a number|`bits(0x7)` returns `"00000111"`|
|`num2hex(x)`|A hexadecimal string of the binary representation of a floating point number|`num2hex(1.0)` returns `"3ff0000000000000"`|
|`bin`|Convert an integer to a binary string|`bin(10)` returns `"1010"`|
|`oct`|Convert an integer to an octal string|`oct(10)` returns `"12"`|
|`hex`|Convert an integer to a hexadecimal string|`hex(10)` returns `"a"`|
|`dec`|Convert an integer to a decimal string|`dec(0xa)` returns `"10"`|
|`eps(x)`|The distance between `x` and the next larger representable floating-point value of the same type as `x`|`eps(Float32)` returns `1.1920929f-7`|

And there are a same number of functions with the same names but in
lower case for converting a value to corresponding numeric types.  For
example, `uint64(x)` converts `x` to `Uint64` data type, `char(120)`
converts the integer value `120` to a `Char`, which turns out to be
`'x'`.

In addition, a set of special floating-point values is provided, such
as `Inf`, `-Inf`, `NaN`.  More details can be found at
[Julia Manual - Integers and Floating-Point Numbers](http://docs.julialang.org/en/latest/manual/integers-and-floating-point-numbers/)


### Array ###

An array in Julia is indexed from 1, not 0.  And the last element can
be accessed by using index `end`.  Range indexing can be done by using
`:`, such as `1:5` (range `[1, 2, 3, 4, 5]`) or `2:2:10` (range
`[2, 4, 6, 8, 10]`)

**Note** the difference between arrays constructed with and without
comma:

```Julia
julia> x = [1, 2, 3]
3-element Array{Int64,1}:
 1
 2
 3

julia> x = [1 2 3]
1x3 Array{Int64,2}:
 1  2  3
```


### String ###

String literals are denoted by being enclosed in double quotes, or
triple double quotes when a string contains double quotes, since
escape the quotes with `\` would be less readable:

```Julia
julia> a = "Hello";

julia> b = """Escape the quotes with "\\" would be less readable""";

julia> c = "Escape the quotes with \"\\\" would be less readable";

julia> b == c
true
```

Strings can be constructed by function `string` or string
interpolation with `$`:

```Julia
julia> "1 + 2 = $(1+2)"
"1 + 2 = 3"

julia> string("1 + 2 = ", 1+2)
"1 + 2 = 3"
```

Here `$` can be followed by any expressions enclosed in parentheses.

Indexing a specific character in a string is like in an array, the
first character is also at index 1.

```Julia
julia> a = "Hello"
"Hello"

julia> a[1]
'H'

julia> a[1:3]
"Hel"
```

However, when the characters in a string aren't in ASCII, the default
encoding of Julia --- UTF-8 --- allows those characters represented
with multiple bytes, so that indexing a string may not get a valid
character.

```Julia
julia> a = "∀x ∃y"
"∀x ∃y"

julia> s = "\u2200x \u2203y"
"∀x ∃y"

julia> a == s
true

julia> s[1]
'∀'

julia> s[2]
ERROR: invalid UTF-8 character index
 in getindex at utf8.jl:63

julia> s[3]
ERROR: invalid UTF-8 character index
 in getindex at utf8.jl:63

julia> s[4]
'x'
```

So the common and effective way to iterate through the characters in a
string is:

```Julia
julia> for c in s
         println(c)
       end
∀
x

∃
y
```

Here are a few useful function related to strings (We can also find
more by typing `apropos("string")` in REPL):

|Function|Description|Example|
|:-------|:----------|:------|
|`length(s)`|The number of characters in string `s`|`length("∀x ∃y")` returns `5`|
|`sizeof(s)`|The number of bytes in string `s`|`sizeof("∀x ∃y")` returns `9`|
|`endof(s)`|The index of the last character of `s`|`endof("∀x ∃")` returns `6`|
|`chr2ind(s, i)`|The index of the `i`-th character of `s`|`chr2ind("∀x ∃y", 4)` returns `6`|
|`nextind(s, i)`|The next valid string index after `i` of the string `s`|`nextind("∀x ∃y", 1)` returns `4` for the very index of character `x`|
|`prevind(s, i)`|The previous valid string index before `i` of the string `s`|`prevind("∀x ∃y", 3)` returns `1`|
|`lowercase(s)`|A string of lowercase of `s`|`lowercase("Hello")` returns `"hello"`|
|`uppercase(s)`|A string of uppercase of `s`|`uppercase("Hello")` returns `"HELLO"`|
|`strip(s)`|A string of `s` but with any leading and trailing whitespace removed|`strip("  Hello  ")` returns `"Hello"`|
|`searchindex(s, sub)`|The start index at which the substring `sub` is found in `s`|`searchindex("Hello", "e")` returns `2`|
|`beginswith(s, prefix)`|Whether string `s` begins with `prefix`|`beginswith("music001", "music")` returns `true`|
|`join(s, d)`|Join an array of strings `s` into a single string, inserting the given delimiter `d` between adjacent strings|`join(["Hello", "world"], ", ")` returns `"Hello, world"`|
|`repeat(s, i)`|Construct a string of `i`-times repeated concatenation of `s` |`repeat("@#", 3)` returns `"@#@#@#"`|
|`replace(s)`|||


### Regular Expressions ###

Julia's regular expression is Perl-compatible.  We can construct a
pattern by prefixing a pattern string with `r`.  We will give a short
example to explain its usage (which is from
[Julia manual - Strings](http://docs.julialang.org/en/latest/manual/strings/#regular-expressions)):

```Julia
julia> m = match(r"(a|b)(c)?(d)", "ad")
RegexMatch("ad", 1="a", 2=nothing, 3="d")

julia> m.match
"ad"

julia> m.captures
3-element Array{Union(Nothing,SubString{UTF8String}),1}:
 "a"
 nothing
 "d"

julia> m.offset
1

julia> m.offsets
3-element Array{Int64,1}:
 1
 0
 2

julia> first, second = m.captures; first
"a"
```




### Elementary mathematical operations and functions ###

The basic arthmetic and bitwise operations are similar to other
programming languages, such as C:

```Julia
+ - */
\ # inverse divide, e.g., x\y is equivalent to y/x
^ # power, e.g., 2^3 equals to 8
% # remainder, e.g., 3%2 equals to 1

! # negation

~ & | $ # bitwise not, and, or, xor

>>> # logical shift right
>>  # arithmetic shift right
<<  # logical/arithmetic shift left

# corresponding updating operators
+=  -=  *=  /= %=  ^=  &=  |=  $=  >>>=  >>=  <<=

# comparisons
==
<
<= ≤  # Can be entered by typing "\le" followed by Tab
>
>= ≥  # Can be entered by typing "\ge" followed by Tab
!= ≠  # Can be entered by typing "\ne" followed by Tab
```

Special note should be taken when comparing `Inf`, `NaN`, see
[Julia Manual - Mathematical Operations and Elementary Functions](http://docs.julialang.org/en/latest/manual/mathematical-operations/#numeric-comparisons)

Julia allows chained comparisons, which can be re-written by `&&`:

```Julia
1 < 2 <= 3 > 0 # equals to: 1 < 2 && 2 <= 3 && 3 > 0
```

A list of useful functions frequently used in mathematics can be found
at
[Julia Manual - Mathematical Operations and Elementary Functions](http://docs.julialang.org/en/latest/manual/mathematical-operations/#elementary-functions)


### Support for complex and rational numbers ###

Complex and rational number are pre-defined types in Julia.

```Julia
-1 + 2im  # a complex number, "im" denotes imaginary part
3//4      # a rational number equals to 0.75
```

Corresponding arithmetic operations are also defined for complex and
rational numbers.

```Julia
(-1 + 2im)*(-1 - 2im) # 5 + 0im
3//4 * 1//3           # 1//4
```


### Control flow ###

#### if-elseif-else-end ####

Conditional evaluation can be obtained by the `if-elseif-else-end`
construct.  For example,

```Julia
x = 1
if x > 0
  y = x * 2
elseif x < 0
  y = -x * 2
else
  y = 1
end
```

Note that `elseif` and `else` are optional, and the conditions
must be expressions that can be evaluated to be boolean values such as
`true` and `false`.


#### while and for loops ####

`while...end` loops are like:

```Julia
i = 1
while i <= 5
  println(i)
  i += 1
end
```

And the `for...end` loop do the same thing is like:

```Julia
for i = 1:5
  println(i)
end
```

which is equivalent to

```Julia
for i in 1:5
  println(i)
end
```

`break` and `continue` are also the same in Julia as the other
programming languages such as C.

The special usage of `for` loops below:

```Julia
for i = 1:3, j in 1:5
  println(i, ", " , j)
end
```

is a syntactic sugar of:

```Julia
for i = 1:3
  for j = 1:5
    println(i, ", " , j)
  end
end
```

However, a `break` will terminate the entire loop that use the
concise nested form.

### Compound expressions ###

In Julia, we can use `begin...end` or `(;)` chains to form a single
compound expression out of several sub-expressions.  In other words,
it can be considered as a small one-time-use function with the value
of the last sub-expression as its return value.

The four ways we can write a compound expression are (The examples
below are borrowed from
[Julia manual - Compound Expressions](http://docs.julialang.org/en/latest/manual/control-flow/#compound-expressions).):

1.  `begin...end` in a single line:

    ```Julia
    z = begin x = 1; y = 2; x + y end
    ```

2.  `begin...end` cross multiple lines:

    ```Julia
	z = begin
	  x = 1
	  y = 2
	  x + y
	end
    ```

3.  `(;)` in a single line:

    ```Julia
	z = (x = 1; y = 2; x + y)
    ```

4.  `(;)` cross multiple lines:

    ```Julia
	z = (
	  x = 1;
	  y = 2;
	  x + y
	)
    ```

Note that when in multiple lines, "`;`" should be kept in `(;)`
chains, while in `begin...end`, it can be droped.  (? I am not
sure whether there is other usage of `(;)`, but here it seems
there is no big difference between `begin...end` and `(;)`,
except that `(;)` saves typing.)


### Function ###

- [ ] maybe need to be more concise like
  [Compound expressions](#compound-expressions)

Functions are defined with `function...end`:

```Julia
function greaterThan(x, y)
  return x > y
end
```

Here we define a function which we can refer it by the name
`greaterThan`.  And the `return` in the function is optional,
which means it can be written as:

```Julia
function greaterThan(x, y)
  x > y
end
```

This is because that in Julia, the value of the last evaluated
expression in the body of a function will be considered as the return
value of that function by default, unless some other value is
explictly indicated as return value by `return` somewhere before the
last expression.

In Julia, function is treated the same as any other object.  That is,
they can be assigned to variables, used as arguments to other
functions, and returned as values, besides called as functions with
the parenthesis form.  All we need is something we can refer to it,
such as a name.

We can call a function with its name followed by the actual arugment
enclosed in parentheses, or by the `apply` function:

```Julia
a = 1
b = 2
if greaterThan(a, b)
  println("a > b")
else
  println("a <= b")
end
```

which is equivalent to:

```Julia
a = 1
b = 2
if apply(greaterThan, a, b)
  println("a > b")
else
  println("a <= b")
end
```

The `apply` function takes another function as its first argument,
and then apply that function to the remain arguments of itself.

If the body of a function consists of only one single expression, the
function can also be defined like:

```Julia
greaterThan(x, y) = return x > y
```

or equivalently:

```Julia
greaterThan(x, y) = x > y
```

or even:

```Julia
greaterThan = (x, y) -> x > y
```

which is defined by assigning an **anonymous function** to the
variable `greaterThan`.

We can also pass an anonymous function to another function that take
functions as its arguments, for example with the previous `apply`
function:

```Julia
apply((x, y) -> begin
        if x > y
		  println(x, " > ", y)
		else
		  println(x, " <= ", y)
		end
      end,
      1,
	  2)
```

which can be written in a more compact way as:

```Julia
apply(1, 2) do x, y
  if x > y
    println(x, " > ", y)
  else
    println(x, " <= ", y)
  end
end
```

The `do...end` is another syntactic sugar that creates an anonymous
function with arguments afterwards (here are `x` and `y`), to be
passed as the first argument to the function before it (here is the
`apply` function), where the rest arguments will be the second, the
third one and so on.


#### Return multiple values ####

In Julia, multiple values are returned by being wrapped in a tuple (A
tuple is an ordered list of values grouped by parentheses with each
value seperated from eath other by comma, ).  However, a syntactic
sugar is provided to allow tuples being created and destructured
without needing parentheses:

```Julia
julia> foo(a, b) = (a+b, a*b);
julia> foo(2, 3)
(5,6)

julia> foo(a, b) = a+b, a*b;
julia> foo(2, 3)
(5,6)

julia> x, y = foo(2, 3)
(5,6)

julia> x
5

julia> y
6
```

#### Optional positional and keyword arguments ####

**Optional** arguments are arguments with default values, so that
functions with optional arguments can be invoked without given
explicit values for those optional arguments if the default values are
appropriate enough.

Optional **posisional** arguments are optional arguments.  The word
"positional" means that in a call, they should be passed in the same
order specified in the function definition.

```Julia
julia> foo(x, y=1, z=1) = x + y + z
foo (generic function with 3 methods)

julia> methods(foo)
# 3 methods for generic function "foo":
foo(x) at none:1
foo(x,y) at none:1
foo(x,y,z) at none:1

julia> foo(1)
3

julia> foo(1, 2)
4

julia> foo(1, 2, 3)
6

julia> foo(1, , 3)
ERROR: syntax: unexpected ,
```

The last results above tells if one specifies a value for a optional
positional argument in a call, the values of all prior optinal
positional arguments must also be explicitly specified.

Therefore, keyword arguments come to rescue.  **Keyword** arguments
are optional arguments too.  Different from positional arguments,
keyword arguments can be referred by the label (keyword) attached to
them.  Thus, in a call, they can be placed in any order, but must be
with explicitly reference by the labels, no matter what order they are
in.  Keyword arguments sequences are defined and seperated from other
type of arguments by using a semicolon in the signature of the
function.

```Julia
julia> foo(x, y=1, z=2; u=3, v=4) = x  - (y + z) + u * v;
julia> foo(1;)
10

julia> foo(1)
10

julia> foo(1, 2, 3; u=5, v=6)
26

julia> foo(1, 2, 3, u=5, v=6)
26

julia> foo(u=5, 1, v=6, 2, 3)
26
```

The last results above tells keyword arguments can be mixed with other
arguments in a call.

Both optional positional and keyword arguments (which are collectively
called optional arguments) should have default values.  Subsequent
optional arguments may refer to prior arguments in defining their
default values.  And all non-optional arguments should be put before
optional arguments in the function definition.

```Julia
julia> foo(x, y=1, z=2; u, v=4) = x  - (y + z) + u * v;
ERROR: syntax: invalid keyword argument u

julia> foo(x, y=1, z=2; u=3, v=u+1) = x  - (y + z) + u * v;
julia> foo(1)
10

julia> foo(x, y=1, z=2, u; v=4) = x  - (y + z) + u * v;
ERROR: syntax: optional positional arguments must occur at end

julia> foo(x, u, y=1, z=2; v=4) = x  - (y + z) + u * v;
julia> foo(1, 3)
10
```

### Special ellipsis "..." symbol ###

Ellipsis "`...`" has special meaning when used with iterable objects
and functions.

1.  Iterable objects followed by an ellipsis "`...`" as an argument to a
    function call.

    ```Julia
	julia> add(x, y) = x + y;
    julia> a = (1, 2); b = [3, 4];
	julia> add(a)
	ERROR: no method add((Int64,Int64),)
	
    julia> add(a...)
    3
	
    julia> add(b...)
    7
	```

    Here the "`...`" in the function call tells Julia that the
    argument `a` should be treated as a collection of arguments.  In
    other words, each element in `a` should be considered as an
    individual argument to the function `add`.

2.  An argument followed by an ellipsis "`...`" as the last argument in
    a function definition.

    ```Julia
	julia> bar(a,b,x...) = (a,b,x);
    julia> bar(1,2)
    (1,2,())
	
    julia> bar(1,2,3)
    (1,2,(3,))
	
    julia> bar(1,2,3,4)
    (1,2,(3,4))
	```

    In this case, the "`...`" tells Julia that the function `bar`
    takes two or more arguments, the first as `a`, the second as
    `b`, and the remains as `x` if any.


### Variable scope ###

In Julia, `for` loops, `try` and `catch` blocks, `function`
bodies, all of these constructs will introduce a new scope for the
variable used within them, where new local variables can be defined
and visible, without worrying about naming conflicts of the same name
variables inside and outside the scope.  However, attention should be
paid to `begin...end` blocks, since they won't introduce any new
scope:

```Julia
julia> for i = 1
         local x = 1
         for j = 1
           local x = 2
           println(x)
         end
		 println(x)
       end
2
1

julia> begin
         local x = 1
         begin
           local x = 2
           println(x)
         end
		 println(x)
       end
ERROR: syntax: local x declared twice
```

#### **let...end** ####

`let...end` is often used for introducing a new scope for local
variables without extra side effects like `for...end` where the code
within it may loop multiple times.  The template for `let...end` is:

```Julia
let var1 = value1, var2, var3 = value3
  code
end
```

where the first line is used for defining local variables that can be
referred to within the "`code`" part.

```Julia
julia> x = 1; y = 2;

julia> let x = 2
         y = 3x
       end
6

julia> y
6

julia> x
1

julia> let x = x, y, z = 2
         y = x + z
         println(y)
       end
3

julia> y
6
```

Note that in the first line of the last `let...end`, the first `x`
is the new defined variable within `let...end`, while the second
`x` is the one defined previously.

One can also leave the first line blank.

```Julia
julia> let
         x = 2
         y = 3x
       end
6

julia> y
6

julia> x
2
```

#### Special note ####

An easily misleading thing I found in the
[Julia Manual about Scope of Variables](http://docs.julialang.org/en/latest/manual/variables-and-scoping/#for-loops-and-comprehensions) is:

```Julia
Fs = cell(2)
for i = 1:2
    Fs[i] = ()->i
	end

julia> Fs[1]()
1

julia> Fs[2]()
2
```

Actually, when there already exists the varialbe `i` before `for` loop:

```Julia
julia> i = 1;

julia> for i = 1:2
         Fs[i] = () -> i
	   end

julia> Fs[1]()
2

julia> Fs[2]()
2
```

the effect is the same as `while` loop:

```Julia
Fs = cell(2)
i = 1
while i <= 2
  Fs[i] = ()->i
    i += 1
	end

julia> Fs[1]()
3

julia> Fs[2]()
3
```

unless one introduces a new scope by `let...end`:

```Julia
Fs = cell(2)
i = 1
while i <= 2
  let i = i
      Fs[i] = ()->i
	    end
		  i += 1
		  end

julia> Fs[1]()
1

julia> Fs[2]()
2
```


### Operators ###

#### Special note for logical operators ####

The last entry (and only it) in a conditional chain formed by the
logical operators `&&` and `||` can be a type of non-boolean
expression, so that the value of the whole chain expression will be
either a boolean value (`false` for `&&`, and `true` for `||`)
or the value of the last entry, depending on whether the last entry
got evaluated or not, which is determined by the short-circuit
property of logical operators.  For example,

```Julia
a = (false || (x = "Hello"))  # a will be "Hello"
a = (true || (x = "Hello"))   # a will be true
```

which can be re-written with one-line `if` statements as:

```Julia
a = (if !false x = "Hello" end)
a = (if false x = "Hello" else true end)
```

And I think no real code would be written this way.  It is only for
illustration.  And the pratical usage of this behaviour of logical
operators are well demonstrated by the factorial routine in the
[Julia manual - Short-Circuit Evaluation](http://docs.julialang.org/en/latest/manual/control-flow/#short-circuit-evaluation)

As mnemonic, one can think:

```Julia
(a || b)
```

as

```Julia
if !a
  b
end
```

and

```Julia
(a && b)
```

as

```Julia
if a
  b
end
```

### Types ###

Though Julia is dynamic programming language, it doesn't mean type is
not important.  It is just the so powerful type system in Julia that
make it expressive, clear and intuitive.

#### Type declaration ####

Usually, one doesn't need to specify a type for a value in Julia.
However, there is some time that it is clearer and more useful to
explicitly declare (or annotate) a type for a value.  **Type
declaration** (or **annotation**) is done by following an expression
or a variable the operator `::` and the desired type:

```Julia
julia> (1+1)::Int
2

julia> (1.0 + 1.0)::Int
ERROR: type: typeassert: expected Int64, got Float64

julia> add(x::Int, y::Int) = x + y
add (generic function with 1 method)

julia> add(1, 2)
3

julia> add(1.0, 2.0)
ERROR: no method add(Float64,Float64)
```

Note that type annotation cannot be used in global scope, such as the
REPL.

```Julia
julia> x::Int8
ERROR: x not defined

julia> x::Int8 = 10
ERROR: x not defined
```


#### Abstract types ####

**Abstract types** are the backbone of Julia type system and form the
conceptual hierachy of it.  They make a piece of code can be applied
to a range of types not just a specific **concrete type**.  In the
whole type hierarchy of Julia, there are two predefined abstract types
`Any` and `None`, which are at the top and the bottom respectively.
In other words, all objects are instances of `Any`, and `Any` is also
the supertype of all types.  On the opposite, no object is an instance
of `None`, and `None` is the subtype of all types.

An abstract type can be defined by `abstract`:

```Julia
abstract Number
```

A hierarchical relationship between two abstract types is defined by
`<:`:

```Julia
abstract Real <: Number
```

where `Real` is below `Number` in the type hierarchy, in other words,
`Real` is a subtype of `Number` and `Number` is a supertype of `Real`.

`<:` can also be used as an operator (or a function) to find out
whether one type is a subtype of the other type:

```Julia
julia> Int <: Number
true
```

##### Type unions #####

A type union is a special abstract type, much like `union` in C, that
can be constructed by the `Union` function:

```Julia
julia> IntOrString = Union(Int,String)
Union(String,Int64)

julia> 1 :: IntOrString
1

julia> "Hello!" :: IntOrString
"Hello!"

julia> 1.0 :: IntOrString
ERROR: type: typeassert: expected Union(String,Int64), got Float64
```


#### Concrete types ####

Unlike **abstract types**, **concrete types** are used to refer to
specific types that can have instances.

##### Composite types #####

Most commonly-used user-defined concrete types are **composite
types**.  Concrete typs is a collection of name fields, more like
`struct` in C, but less like `class` in C++.  They are defined by
`type...end` with field names and optionally annotated types:

```Julia
julia> type Foo
         bar
         baz::Int
         qux::Float64
       end
```

Instances of type `Foo` are created by applying the `Foo` type object
like a function to values of compatible types with the fields:

```Julia
julia> foo = Foo("Hello, world.", 23, 1.5)
Foo("Hello, world.",23,1.5)

julia> foo = Foo("Hello, world.", 23.0, 1.5)
ERROR: no method Foo(ASCIIString,Float64,Float64)
```

The list of field names of a composite type can be obtained by the
`names` function:

```Julia
julia> names(Foo)
3-element Array{Any,1}:
 :bar
 :baz
 :qux

julia> names(foo)
3-element Array{Any,1}:
 :bar
 :baz
 :qux
```

The value of a specific field can be accessed by following an instance
with a `.` and the field name:

```Julia
julia> foo = Foo("Hello, world.", 23, 1.5)
Foo("Hello, world.",23,1.5)

julia> foo.bar
"Hello, world."

julia> foo.bar = 1
1

julia> foo.bar
1
```

#### Parametric types ####

**Parametric types** are types that parameterized in terms of other
types.  In other words, a parametric type is a collection of types
where each specific concrete type is derived from other corresponding
specific types in replace of type paramenters (such as the `T` in
curly braces below of `Point`) of that parametric type, much like a
function, however, it is types here being the substitutes, not values.
Therefore, a parametric type is also an abstract type.

One can define a parametric type by following the type name with a
curly-braces-surrounded list of type paramenters:

```Julia
julia> type Point{T}
         x::T
         y::T
       end

julia> abstract Pointy{T}

julia> type Pointz{A,B}
         x::A
         y::B
       end

julia> Point{Int} <: Point
true

julia> Pointy{Int} <: Pointy
true

julia> Point{Int} <: Point{Number}
false

julia> Pointy{Int} <: Pointy{Number}
false
```

Since a parametric type is an abstract type, instances can only be
created for a specific concrete type derived from that parametric
type.  Except that we need to specify concrete types for the type
paramenters, all are the same as other non-parametric types:

```Julia
julia> Point{Float64}(1.0,2.0)
Point{Float64}(1.0,2.0)

julia> Pointz(1, "a")
Pointz{Int64,ASCIIString}(1,"a")
```

Just as a plain type can have a supertype, so the type parameter can
also have a supertype serves as a range constraint:

```Julia
julia> abstract Pointy{T <: Real}

julia> Pointy{Int64}
Pointy{Int64}

julia> Pointy{String}
ERROR: type: Pointy: in T, expected Real, got Type{String}
```

#### Type aliases ####

Like `typedef` in C, `typealias` is used to give a new name for an
type.

```Julia
julia> typealias IntPt Point{Int64}
Point{Int64} (constructor with 1 method)

julia> IntPt(1, 2)
Point{Int64}(1,2)
```

#### Useful functions related to types ####

|Function|Description|Example|
|:-------|:----------|:------|
|`T1 <: T2`|Subtype operator, determine whether `T1` is a subtype of `T2`.|`Int64 <: Number` returns `true`|
|`isa(x, type)`|Determine whether `x` is of the given `type`.|`isa(1, Float64)` returns `false`|
|`typeof(x)`|Get the concrete type of `x`.|`typeof(1)` returns `Int64` (in 64-bit system)|
|`super(type)`|Return the supertype of DataType `type`|`super(Int64)`, `super(Signed)`, `super(Integer)`, `super(Real)` return `Signed`, `Integer`, `Real`, `Number`, respectively |


### Methods ###

In Julia, a function can have different behaviors for different
combinations of argument types and numbers.  Such definition of one
possible behavior for a fucntion is called a **method**, and it is
just a new definition of the same function but with different
arguments.  Such mechanism of choosing which method to execute when a
function is applied in Julia is known as **multiple dispatch**.

A new method for a specific function can be introduced anywhere at
anytime, as long as it has the same name and different argument types
or numbers.  Argument types can be specified by `::` operator (see
also [Type declaration](#type-declaration)), thus, the method can only
be applied to arguments of the specific types:

```Julia
julia> f(x::Int64, y::Int64) = x + y
f (generic function with 1 method)

julia> f(3, 4)
7

julia> f(3.3, 4.4)
ERROR: no method f(Float64,Float64)

julia> f(x::Float64, y::Float64) = round(x + y)
f (generic function with 2 methods)

julia> f(3.3, 4.4)
8.0
```

Like [parametric types](#parametric-types), methods can also be
parametric.  Type parameters should be declared within curly brackets
after the method name and before the argument tuple:

```Julia
julia> same_type_number{T}(x::T, y::T) = T <: Number;

julia> same_type_number(x, y) = false
same_type_number (generic function with 2 methods)

julia> same_type_number(1, 2.0)
false

julia> same_type_number(1, 2)
true
```

The second method for `same_type_number` above is used as a catch-all
method when the two arguments aren't the same type.


#### Useful functions operates on methods ####

|Function|Description|Example|
|:-------|:----------|:------|
|`methods(f)`|Show all methods of `f` with their argument types.||


### Constructors ###

Constructors are used for creating new objects of a type.  By default,
type objects serve as constructor functions, which means that a new
object of a type can be created by following the type name by a tuple
of field values at the same order of the fields (see
[Composite types](#composite-types)).

There are two ways that a constructor can be defined.

* One way is defining a constructor after the definition of the type.
  These kind of constructors are called **outer constructors**.  It is
  much like defining a new method for a function, except that it must
  use one of the already existed constructors for creating a new
  object.  And generally, the type name followed by a tuple of the
  field names is the automatically provided default one.

* And the other is defining a constructor inside the definition of the
  type.  These kind of constructors are called **inner constructors**.
  Once a inner constructor is defined, the automatically provided
  default constructors mentioned above will not provided.


```Julia
julia> type OrderedPair
         x::Real
		 y::Real

         # a inner constructor that makes sure the first argument
		 # is less than or equal to the second argument
         OrderedPair(a,b,c) = a > b ? error("out of order") : new(a+c,b+c)
       end

julia> a = OrderedPair(1, 2, 3)
OrderedPair(4,5)

julia> a.x = 10  # But one can make x greater than y
10

julia> a
OrderedPair(10,5)

julia> b = OrderedPair(1, 2)  # no default constructor if a inner one exists
ERROR: no method OrderedPair(Int64,Int64)

julia> OrderedPair(a) = OrderedPair(a, a, 2a) # outer constructor
OrderedPair (constructor with 2 methods)

julia> c = OrderedPair(1)
OrderedPair(3,3)
```


### Tasks ###

### Exception handling ###




## Write your own package ##


## Some interesting facts ##

### The number of available packages ###

Julia is still young.  The number of available packages is small
compared to R.  However, they grow rapidly.  Here we list the number
of available packages in the table.  One may have different
interpretations, but the purpose here is for studying the trend of
these two counterparts only by tracking the number of packages newly
comming out.


| Date     |Julia| R  |
|:--------:|----:|---:|
|2014-06-19|  279|5323|
|2014-07-21|  377|5413|
|2014-08-21|  401|5516|
|2014-09-21|  435|5633|
|2014-11-21|  477|5775|
|2015-01-21|  536|5954|
|2015-05-21|  629|6308|
|2015-08-21|  702|6644|
|2015-09-21|  742|6772|
|2015-10-21|  782|6881|
|2015-12-21|  797|7099|
|2016-01-21|  861|7207|
|2016-02-21|  899|7332|


We can get the number of available packages of Julia and R,
respectively by the following Linux shell scripts.

```Shell
# Get the number of available packages of Julia
expr $(curl -s https://github.com/JuliaLang/METADATA.jl | grep \
"js-directory-link" | wc -l) - 5

```

```Shell
# Get the number of available packages of R
expr $(curl -s http://cran.r-project.org/src/contrib/Archive/ | sed -n \
'/Parent Directory/,$ p' | grep -c "</a>") - 1
```

There is also a
[Searchable listing of all registered packages for Julia](http://pkg.julialang.org/),
where you can search for specific package of Julia.

## Useful resources ##

* [The Offical Website for Julia Programming Language](http://julialang.org/)
* [The Latest Manual for Julia Lang](http://docs.julialang.org/en/latest/manual/)
* [Julia Bloggers](http://www.juliabloggers.com/) gathers blogs about
  Julia.  One can also
  [submit their RSS feed](http://www.juliabloggers.com/julia-bloggers-submit-rss-feed/)
  for the specific blogs related to Julia
* [List of Available Julia Packages](http://docs.julialang.org/en/latest/packages/packagelist/)
