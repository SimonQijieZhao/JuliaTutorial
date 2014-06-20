# Julia Tutorial #

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
  + [Play with Julia script file](#play-with-julia-script-file)
  + [Comment code](#comment-code)
  + [Variables](#variables)
  + [Control flow](#control-flow)
    - [if-elseif-else-end](#if-elseif-else-end)
	- [while and for loops](#while-and-for-loops)
  + [Compound expressions](#compound-expressions)
  + [Function](#function)
    - [Return multiple values](#return-multiple-values)
  + [Operators](#operators)
	- [Special note for logical operators](#special-note-for-logical-operators)
  + [Run shell command in Julia](#run-shell-command-in-julia)
* [Write your own package](#write-your-own-package)
* [Some interesting facts](#some-interesting-facts)
  + [The number of available packages](#the-number-of-available-packages)
* [Useful resources](#useful-resources)

## Introduction ##

[Julia](http://julialang.org/) is a fast dynamic programming language
for technical computing.

## Installation ##

### On Ubuntu ###

To install the current stable version of Julia, just type:

```Shell
sudo apt-get install julia
```

If you are on an older Ubuntu (before Ubuntu 14.04), then you need to
use the
[Julia PPA (Personal Package Archives)](https://launchpad.net/~staticfloat)
to sync with the latest stable version of Julia (See
[Julia Downloads](http://julialang.org/downloads/) for more details).

```Shell
sudo add-apt-repository ppa:staticfloat/juliareleases
sudo add-apt-repository ppa:staticfloat/julia-deps
sudo apt-get update
sudo apt-get install julia
```



#### Additional software ####

##### IJulia #####

To use [IJulia](https://github.com/JuliaLang/IJulia.jl), you have to
install [IPython](http://ipython.org/) first (See
[Installing IPython](http://ipython.org/install.html) for more
details.):

```Shell
sudo apt-get install ipython-notebook python-matplotlib \
                     python-scipy python-pandas \
					 python-sympy python-nose
```

Thereafter, in shell terminal, enter:

```Shell
julia
```

to get into a Julia command line session, within which type:

```Julia
Pkg.update()
Pkg.add("IJulia")
Pkg.add("PyPlot")
```

to install IJulia and related packages, and type **Ctrl-d** to quit
the session.  Finally, you can type in shell terminal:

```Shell
ipython notebook --profile julia
```

to run Julia in IJulia notebook.


### On Mac ###

### On Windows ###


## A quick tour of Julia ##

### Enter and quit Julia interactive session ###

In shell terminal, just type:

```Shell
julia
```

to get into the interactive session of Julia, within which you type:

```Julia
quit()
```

or **Ctrl-d** to quit back to shell.


### Something special to the REPL ###

1.  Once you have typed a complete expression, pressing **Enter** will
    get the expression be evaluated and the value will be printed out.

2.  A trailing semicolon **;** will suppress the output for the
    evaluated value.

3.  However, you can use the variable **ans**, which is only available
    in REPL, to get the value of the last evaluated expression, no
    matter if it is suppressed or not.

4.  You can type "**julia -q**" to suppress the display of startup
    banner when lauch the REPL.


### Get help in REPL ###

With the **help()** function, one can query the documentation for a
specific function, macro, or variable.  For example,

```Julia
help(println)
```

Alternatively, we can use **?** as a short hand for the **help()**
function:

```Julia
?println
```

If you are not sure how to use **help()**, just type:

```Julia
?help
```

for more details.

**apropos()** is a more flexible function that can be used to search
documentation for functions related to a specific string.

And the blog [Julia Helps](http://www.juliabloggers.com/julia-helps/)
gives a good summary about getting help from Julia itself.


### Play with Julia script file ###

A Julia script file has **.jl** as its extension.

1.  To execute the code in a Julia script file within a Julia
    interactive session, we use function **include()**.  For example,
    if we have a script named **hello.jl** with the following
    contents:

    ```Julia
	# hello.jl
    println("Hello, world!")
    ```

    then in a Julia session, type:

    ```Julia
    include("hello.jl")
    ```

    "**Hello, world!**" will be printed out.

2.  To execute a Julia script in shell, for example, previous
    "**hello.jl**", type:

    ```Shell
    julia hello.jl
    ```

3.  To execute a short code within shell command line, we could use
    the option "**-e**" for command "**julia**":

    ```Shell
    julia -e 'println("Hello, world!")'
    ```

4.  To execute a Julia script in shell with one or more command line
    arguments, Julia provides **ARGS** for holding the arguments
    passed from command line.  For example, we have a script named
    "**hello2.jl**":

    ```Julia
	# hello2.jl
    println("Hello, ", ARGS[1], "!")
    ```

    then in shell, type:

    ```Shell
    julia hello2.jl Simon
    ```

    will output "**Hello, Simon!**".


### Comment code ###

1.  In a single Julia script line, everything behind a **#** is
    considered as comment.

2.  **#=** and **=#** are used for multi-line comments.


### Variables ###

Like other languages, variable names in Julia must also begin with a
letter in English alphabet, or underscore.

As a dynamic programming language, there is no restriction for a
variable in Julia to be of a fixed type after introduced in a scope.
In other words, a variable can be assigned to a value of different
type from its previous one, excpet that in a local scope, we can add a
type annotation to a variable to restrain it from being assigned to a
value of a different type.

Note: When in the REPL, we are in a global scope, and a variable
defined in a function is in a local scope.


### Control flow ###

#### if-elseif-else-end ####

Conditional evaluation can be obtained by the **if-elseif-else-end**
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

Note that **elseif** and **else** are optional, and the conditions
must be expressions that can be evaluated to be boolean values such as
**true** and **false**.


#### while and for loops ####

**while...end** loops are like:

```Julia
i = 1
while i <= 5
  println(i)
  i += 1
end
```

And the **for...end** loop do the same thing is like:

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

**break** and **continue** are also the same in Julia as the other
programming languages such as C.

The special usage of **for** loops below:

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

### Compound expressions ###

In Julia, we can use "**begin...end**" or "**(;)**" chains to form a
single compound expression out of several sub-expressions.  In other
words, it can be considered as a small one-time-use function with the
value of the last sub-expression as its return value.

The four ways we can write a compound expression are (The examples
below are borrowed from
[Julia manual - Compound Expressions](http://docs.julialang.org/en/latest/manual/control-flow/#compound-expressions).):

1.  "**begin...end**" in a single line:

    ```Julia
    z = begin x = 1; y = 2; x + y end
    ```

2.  "**begin...end**" cross multiple lines:

    ```Julia
	z = begin
	  x = 1
	  y = 2
	  x + y
	end
    ```

3.  "**(;)**" in a single line:

    ```Julia
	z = (x = 1; y = 2; x + y)
    ```

4.  "**(;)**" cross multiple lines:

    ```Julia
	z = (
	  x = 1;
	  y = 2;
	  x + y
	)
    ```


### Function ###

- [ ] maybe need to be more concise like
  [Compound expressions](#compound-expressions)

Functions are defined with **function...end**:

```Julia
function greaterThan(x, y)
  return x > y
end
```

Here we define a function which we can refer it by the name
**greaterThan**.  And the **return** in the function is optional,
which means it can be written as:

```Julia
function greaterThan(x, y)
  x > y
end
```

This is because that in Julia, the value of the last evaluated
expression in the body of a function will be considered as the return
value of that function by default, unless some other value is
explictly taken as return value by **return** somewhere before the
last expression.

In Julia, function is treated the same as any other object.  That is,
they can be assigned to variables, used as arguments to other
functions, and returned as values, besides called as functions with
the parenthesis form.  All we need is something we can refer to it,
such as a name.

We can call a function with its name followed by the actual arugment
enclosed in parentheses, or by the **apply** function:

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

The **apply** function takes another function as its first argument,
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

which is defined by assigning an anonymous function to the variable
**greaterThan**.

We can also pass an anonymous function to another function that take
functions as its arguments, for example with the previous **apply**
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

The **do...end** is another syntactic sugar that creates an anonymous
function with arguments afterwards (here are **x** and **y**), to be
passed as the first argument to the function before it (here is the
**apply** function), where the rest arguments will be the second, the
third one and so on.


#### Return multiple values ####


### Operators ###

#### Special note for logical operators ####

The last entry in a conditional chain formed by the logical operators
**&&** and **||** can be a type of non-boolean expression, so that the
value of the whole chain expression will be either a boolean value
(**false** for **&&**, and **true** for **||**) or the value of the
last entry, depending on whether the last entry got evaluated or not,
which is determined by the short-circuit property of logical
operators.  For example,

```Julia
a = (false || (x = "Hello"))  # a will be "Hello"
a = (true || (x = "Hello"))   # a will be true
```

which can be re-written with one-line **if** statements as:

```Julia
a = (if !false x = "Hello" end)
a = (if false x = "Hello" else true end)
```

And I think no real code would be written this way.  It is only for
illustration.  And the pratical usage of this behaviour of logical
operators are well demonstrated by the factorial routine in the
[Julia manual - Short-Circuit Evaluation](http://docs.julialang.org/en/latest/manual/control-flow/#short-circuit-evaluation)


### Run shell command in Julia ###

A shell command should be wrapped in backticks "**`**", and we can use
function **run()** to run the command within them.  For example,

```Julia
run(`echo Hello`)
```

However, the output will automatically be dumped to the screen.  We
can assign the output to a variable by function **readall()**:

```Julia
a = readall(`echo Hello`)
```



## Write your own package ##


## Some interesting facts ##

### The number of available packages ###

Julia is still young.  The number of available packages is small
compared to R.  However, they grow rapidly.  Until 2014-06-19, there
are 279 packages available for Julia, and 5323 packages available for
R.

We can get the number of available packages of Julia and R,
respectively by the following Linux shell scripts.

```Shell
# Get the number of available packages of Julia
curl -s https://raw.githubusercontent.com/JuliaLang/julia/master/doc/packages/packagelist.rst \
| grep "Maintainer" | wc -l
```

```Shell
# Get the number of available packages of R
expr $(curl -s http://cran.r-project.org/src/contrib/Archive/ | sed -n \
'/Parent Directory/,$ p' | grep -c "</a>") - 1
```


## Useful resources ##

* [The Offical Website for Julia Programming Language](http://julialang.org/)
* [The Latest Manual for Julia Lang](http://docs.julialang.org/en/latest/manual/)
* [Julia Bloggers](http://www.juliabloggers.com/) gathers blogs about
  Julia.  One can also
  [submit their RSS feed](http://www.juliabloggers.com/julia-bloggers-submit-rss-feed/)
  for the specific blogs related to Julia
* [List of Available Julia Packages](http://docs.julialang.org/en/latest/packages/packagelist/)
