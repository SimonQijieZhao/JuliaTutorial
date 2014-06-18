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
  + [Play with Julia script file](#play-with-julia-script-file)
  + [Comment code](#comment-code)
  + [Control flow](#control-flow)
    - [if-elseif-else-end](#if-elseif-else-end)
	- [while and for loops](#while-and-for-loops)
  + [Operators](#operators)
	- [Special note for logical operators](#special-note-for-logical-operators)
  + [Run shell command in Julia](#run-shell-command-in-julia)
  + [Miscellaneous](#miscellaneous)
    - [Compound expressions](#compound-expressions)
* [Write your own package](#write-your-own-package)
* [Useful resources](#useful-resources)

## Introduction ##

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

### Miscellaneous ###

#### Compound expressions ####

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



## Write your own package ##


## Useful resources ##

* [The Offical Website for Julia Programming Language](http://julialang.org/)
* [The Latest Manual for Julia Lang](http://docs.julialang.org/en/latest/manual/)
* [Julia Bloggers](http://www.juliabloggers.com/) gathers blogs about
  Julia.  One can also
  [submit their RSS feed](http://www.juliabloggers.com/julia-bloggers-submit-rss-feed/)
  for the specific blogs related to Julia
