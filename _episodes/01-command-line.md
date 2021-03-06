---
title: "First session with GAP"
teaching: 30
exercises: 10
questions:
- "Working with the GAP command line"
objectives:
- "Time-saving tips and tricks"
- "Using GAP help system"
- "Basic objects and constructions in the GAP language"
keypoints:
- "Remember that GAP is case-sensitive!"
- "Do not panic seeing 'Error, Variable: 'FuncName' must have a value'."
- "Care about names of variables and functions."
- "Use command line editing."
- "Use autocompletion instead of typing names of functions and variables in full."
- "Use `?` and `??` to view help pages."
- "Set default help format to HTML using `SetHelpViewer`."
- "Use `LogTo` function to save all GAP input and output into a text file."
- "If calculation takes too long, press <Control>-C to interrupt it."
- "Read 'A First Session with GAP' from the GAP Tutorial."
---

If GAP is installed correctly you should be able to start it some way that
depends on your operating system. GAP starts with the banner displaying
information about the version of the system and loaded components, and then
displays the command line prompt `gap>`, for example:

~~~
┌───────┐   GAP 4.8.5, 25-Sep-2016, build of 2016-10-04 11:28:21 (BST)
│  GAP  │   http://www.gap-system.org
└───────┘   Architecture: x86_64-apple-darwin15.6.0-gcc-6-default64
Libs used:  gmp, readline
Loading the library and packages ...
Components: trans 1.0, prim 2.1, small* 1.0, id* 1.0
Packages:   AClib 1.2, Alnuth 3.0.0, AtlasRep 1.5.1, AutPGrp 1.6,
            Browse 1.8.6, CRISP 1.4.4, Cryst 4.1.12, CrystCat 1.1.6,
            CTblLib 1.2.2, FactInt 1.5.3, FGA 1.3.1, GAPDoc 1.5.1, IO 4.4.6,
            IRREDSOL 1.3.1, LAGUNA 3.7.0, Polenta 1.3.6, Polycyclic 2.11,
            RadiRoot 2.7, ResClasses 4.5.0, Sophus 1.23, SpinSym 1.5,
            TomLib 1.2.5, Utils 0.40
Try '??help' for help. See also '?copyright', '?cite' and '?authors'
gap>
~~~
{: .output}

To leave GAP, type `quit;` at the GAP prompt. Remember that all GAP commands,
including this one, must be finished with a semicolon! Practice this entering
`quit;` to leave GAP, and then start a new GAP session. Before continuing, you
may wish to enter the following command to display GAP prompts and user inputs
in different colours:

~~~
 ColorPrompt(true);
~~~
{: .source}

Now you can use GAP as a calculator:

~~~
( 1 + 2^32 ) / (1 - 2*3*107 );
~~~
{: .source}

~~~
-6700417
~~~
{: .output}

Now we will turn on logging to save all subsequent interaction with GAP into a
log file. Assuming that you do not have a file named `gap-intro.log` in the GAP
current directory (i.e. the directory where you have started GAP on Unix systems,
and the working directory for GAP on Windows), enter the following:

~~~
LogTo("gap-intro.log");
~~~
{: .source}

Then the file `gap-intro.log` in the GAP current directory will contain all
subsequent input and output that will appear on your terminal. To stop logging,
you will need to call `LogTo` without arguments, as in `LogTo();` (but
don't do this now, as we don't want to stop it), or leave GAP.

It will be useful to leave some comments in the log file in case you will
return to it in the future. A comment in GAP starts with the symbol `#` and
continues to the end of the line. Now, if you enter the following after the
GAP prompt:

~~~
# GAP Software Carpentry Lesson
~~~
{: .source}

then after pressing the Return key, GAP will display new prompt, but the comment
will be written to the log file. To check that this works, open another terminal
window, locate the log file and print it using `cat` to verify this.

The log file records all interaction with GAP that is happening after the call
to `LogTo`, but not before. We can certainly repeat the calculation from above
if we want to record it as well. Instead of retyping it, we will use Up and Down
arrow keys to scroll the *command line history*. Repeat this until you will see
the formula again, then press Return (the location of the cursor in the command
line does not matter):

~~~
( 1 + 2^32 ) / (1 - 2*3*107 );
~~~
{: .source}

~~~
-6700417
~~~
{: .output}

Now restore the previous command, use Left and Right arrow keys, Delete or
Backspace to edit it and replace 32 by 64 (another useful shortcuts are
Ctrl-A and Ctrl-E to move the cursor to the beginning or to the end of the
line, respectively). Now press the Return key (at any position of the
cursor in the command line):

~~~
( 1 + 2^64 ) / (1 - 2*3*107 );
~~~
{: .source}

~~~
-18446744073709551617/641
~~~
{: .output}

It is useful to know that if the command line history is long, one could
perform a partial search by typing the initial part of the command and using
Up and Down arrow keys after that, to scroll only the lines that begin with
the same string (but be careful about whitespaces!).

Whitespace characters (i.e. Spaces, Tabs and Returns) are insignificant for
the meaning of GAP input in most places. For example, the previous input
could be typed without spaces:

~~~
(1+2^64)/(1-2*3*107);
~~~
{: .source}

~~~
-18446744073709551617/641
~~~
{: .output}

Whitespace symbols are often used to format more complicated commands for
better readability. For example, the following input which creates a 3x3 matrix

~~~
m:=[[1,2,3],[4,5,6],[7,8,9]];
~~~
{: .source}

~~~
[ [ 1, 2, 3 ], [ 4, 5, 6 ], [ 7, 8, 9 ] ]
~~~
{: .output}

may be spread over three lines. In this case, instead of the full prompt
`gap>`, a partial prompt `>` will be displayed until the user will finish
the input by a semicolon:

~~~
gap> m:=[[ 1, 2, 3 ],
>        [ 4, 5, 6 ],
>        [ 7, 8, 9 ]];
~~~
{: .source}

~~~
[ [ 1, 2, 3 ], [ 4, 5, 6 ], [ 7, 8, 9 ] ]
~~~
{: .output}

Note that you may use `Display` to pretty-print the matrix:

~~~
Display(m);
~~~
{: .source}

~~~
[ [  1,  2,  3 ],
  [  4,  5,  6 ],
  [  7,  8,  9 ] ]
~~~
{: .output}

You have met by now some GAP functions, e.g. `LogTo` and `Display`, and observed
that to call them, one needs to use brackets with no or some arguments in them.

> ## Functions are also GAP objects
>
> Check what happens if you forget to add brackets,
> e.g. type `LogTo;` and `Factorial;`
> We will explain the differences in these outputs later.
{: .callout}

Here there are examples of calling some other GAP functions:

~~~
Factorial(100);
~~~
{: .source}

~~~
93326215443944152681699238856266700490715968264381621468\
59296389521759999322991560894146397615651828625369792082\
7223758251185210916864000000000000000000000000
~~~
{: .output}

(this also displays multi-line output; the exact width may depend
on the terminal settings),

~~~
Determinant(m);
~~~
{: .source}

~~~
0
~~~
{: .output}

and

~~~
Factors(2^64-1);
~~~
{: .source}

~~~
[ 3, 5, 17, 257, 641, 65537, 6700417 ]
~~~
{: .output}

Functions may be combined in various ways, and may be
used as arguments of other functions, for example:

~~~
Filtered( Partitions(10), x -> 5 in x);
~~~
{: .source}

~~~
[ [ 5, 1, 1, 1, 1, 1 ], [ 5, 2, 1, 1, 1 ], [ 5, 2, 2, 1 ],
  [ 5, 3, 1, 1 ], [ 5, 3, 2 ], [ 5, 4, 1 ], [ 5, 5 ] ]
~~~
{: .output}

> ## What does the last command calculate?
> The command `Filtered( Partitions(10), x -> 5 in x);` calculates the list of all partitions of 10 that contain 5.
{: .challenge}
> ## Also, how many functions can you see in the input?
> The input uses 4 function calls, namely:
>
> * `Filtered`
>
> * `Partitions`
>
> * `function(x) return 5 in x; end`
>
> * `in` (the _membership test_)
{: .challenge}

A very time-saving feature of the GAP command-line interfaces is completion
of identifiers when the Tab key is pressed. For example, type `Fib` and then
press the Tab key to complete the input to `Fibonacci`:

~~~
Fibonacci(100);
~~~
{: .source}

~~~
354224848179261915075
~~~
{: .output}

In case when the unique completion is not possible, GAP will try to perform
partial completion, and pressing the Tab key second time will display all possible
completions of the identifier. Try, for example, to enter `GroupHomomorphismByImages`
or `NaturalHomomorphismByNormalSubgroup` using completion.

The way functions are named in GAP might help to memorize or even guess names
of library functions. If a variable name consists of several words then the
first letter of each word is capitalized (remember that GAP is case-sensitive!).
Further details on naming conventions used in GAP are documented in the GAP
manual [here](http://www.gap-system.org/Manuals/doc/ref/chap5.html#X81F732457F7BC851).

It is important to remember that GAP is case-sensitive. For example, the following
input causes an error

~~~
factorial(100);
~~~
{: .source}

~~~
Error, Variable: 'factorial' must have a value
not in any function at line 14 of *stdin*
~~~
{: .error}

because the name of the GAP library function is `Factorial`. Using lowercase
instead of uppercase or vice versa also affects name completion.

Now let's consider the following problem: for a finite group _G_, calculate the
average order of its element (that is, the sum of orders of its elements divided
by the order of the group). Where to start?

Enter `?Group`, and you will see all help entries, starting with `Group`:

~~~
┌──────────────────────────────────────────────────────────────────────────────┐
│   Choose an entry to view, 'q' for none (or use ?<nr> later):                │
│[1]    AutoDoc (not loaded): @Group                                           │
│[2]    loops (not loaded): group                                              │
│[3]    polycyclic: Group                                                      │
│[4]    RCWA (not loaded): Group                                               │
│[5]    Tutorial: Groups and Homomorphisms                                     │
│[6]    Tutorial: Group Homomorphisms by Images                                │
│[7]    Tutorial: group general mapping                                        │
│[8]    Tutorial: GroupHomomorphismByImages vs. GroupGeneralMappingByImages    │
│[9]    Tutorial: group general mapping single-valued                          │
│[10]   Tutorial: group general mapping total                                  │
│[11]   Reference: Groups                                                      │
│[12]   Reference: Group Elements                                              │
│[13]   Reference: Group Properties                                            │
│[14]   Reference: Group Homomorphisms                                         │
│[15]   Reference: GroupHomomorphismByFunction                                 │
│[16]   Reference: Group Automorphisms                                         │
│[17]   Reference: Groups of Automorphisms                                     │
│[18]   Reference: Group Actions                                               │
│[19]   Reference: Group Products                                              │
│[20]   Reference: Group Libraries                                             │
│ > > >                                                                        │
└─────────────── [ <Up>/<Down> select, <Return> show, q quit ] ────────────────┘
~~~
{: .output}

You may use arrow keys to move up and down the list, and open help pages by
pressing Return key. For this exercise, open `Tutorial: Groups and Homomorphisms`
first. Note navigation instructions at the bottom of the screen. Look at
first two pages, then press `q` to return to the selection menu. Next, navigate to
`Reference: Groups` and open it. Within two first pages you will find the
function `Group` and mentioning of `Order`.

GAP manual comes in several formats: text is good to view in a terminal,
PDF is good for printing and HTML (especially with MathJax support) is
very efficient for exploring with a browser. We will use the following to
set the help viewer to the default browser (for this session, see
`?WriteGapIniFile` on how to make this setting permanent):

~~~
SetHelpViewer("browser");
~~~
{: .source}

After that, invoke the help again, and see the difference!

Let's now copy the following input from the first example of the GAP Reference
manual Chapter on groups. It shows how to create permutations, and assign values
to variables; also it is finished by a double semicolon to suppress output:

~~~
a:=(1,2,3);;b:=(2,3,4);;
~~~
{: .source}

Next, let `G` be a group generated by `a` and `b`:

~~~
G:=Group(a,b);
~~~
{: .source}

~~~
Group([ (1,2,3), (2,3,4) ])
~~~
{: .output}

We may explore some properties of `G` and its generators:

~~~
Size(G); IsAbelian(G); StructureDescription(G); Order(a);
~~~
{: .source}

~~~
12
false
"A4"
3
~~~
{: .output}

Our next task is to find out how to obtain a list of element and their orders.
Enter `?elements` and explore the list of help topics. After its inspection,
the entry from the Tutorial does not seem relevant, but the entry from the
Reference manual is. It also tells the difference between using `AsSSortedList`
and `AsList`. So, this is the list of elements of `G`:

~~~
AsList(G);
~~~
{: .source}

~~~
[ (), (2,3,4), (2,4,3), (1,2)(3,4), (1,2,3), (1,2,4), (1,3,2), (1,3,4),
  (1,3)(2,4), (1,4,2), (1,4,3), (1,4)(2,3) ]
~~~
{: .output}

The returned object is a _list_. We would like to assign it to a variable
to explore and reuse. We forgot to do it when we were calculating it. Of
course, we may use the command line history to restore the last command, edit
it and call again. But instead, we will use `last` which is a special variable
holding the last result returned by GAP:

~~~
elts:=last;
~~~
{: .source}

~~~
[ (), (2,3,4), (2,4,3), (1,2)(3,4), (1,2,3), (1,2,4), (1,3,2), (1,3,4),
  (1,3)(2,4), (1,4,2), (1,4,3), (1,4)(2,3) ]
~~~
{: .output}

This is a list. The following commands are self-explanatory:

~~~
gap> elts[1]; elts[3]; Length(elts);
~~~
{: .source}

~~~
()
(2,4,3)
12
~~~
{: .output}

> ## Lists are more than arrays
>
> * May contain holes or be empty
>
> * May dynamically change their length (with `Add`, `Append` or direct assigment)
>
> * Not required to contain objects of the same type
>
> * There are also sets (ordered lists without holes and repetitions)
>
> * See more in [GAP Tutorial: Lists and Records](http://www.gap-system.org/Manuals/doc/tut/chap3.html)
{: .callout}

We are almost ready calculate the average order of elements of `G`. All three
examples below compute it in different ways, exposing concepts like ranges,
for-loops, iterators, and functional notation:

~~~
s:=0;;
for i in [ 1 .. Length(elts) ] do
  s := s + Order( elts[i] );
od;
s/Length(elts);
~~~
{: .source}

~~~
31/12
~~~
{: .output}

~~~
s:=0;;
for g in elts do
  s := s + Order(g);
od;
s/Length(elts);
~~~
{: .source}

~~~
31/12
~~~
{: .output}

~~~
Sum( List( elts, Order ) ) / Length( elts );
~~~
{: .source}

~~~
31/12
~~~
{: .output}

> ## Which approach is better?
>
> Compare these approaches. Which one would you prefer to use?
{: .callout}

GAP has very helpful list manipulation tools. Just to show some more examples:

* finding elements of `G` having no fixed points:

~~~
Filtered( elts, g -> NrMovedPoints(g) = 4 );
~~~
{: .source}

~~~
[ (1,2)(3,4), (1,3)(2,4), (1,4)(2,3) ]
~~~
{: .output}

* funding a permutation `g` such that conjugates (1,2) to (2,3)

~~~
First( elts, g -> (1,2)^g = (2,3) );
~~~
{: .source}

~~~
(1,2,3)
~~~
{: .output}

Let's check this (remember that in GAP permutations are multiplied from left to right!):

~~~
(1,2,3)^-1*(1,2)*(1,2,3)=(2,3);
~~~
{: .source}

~~~
true
~~~
{: .output}

* checking whether no elements of `G` move the point 1 to 2:

~~~
ForAll( elts, g -> 1^g <> 2 );
~~~
{: .source}

~~~
false
~~~
{: .output}

* checking whether there is an element in `G` which moves exactly two points:

~~~
ForAny( elts, g -> NrMovedPoints(g) = 2 );
~~~
{: .source}

~~~
false
~~~
{: .output}

> ## Use list operations to select from `elts` the stabiliser of the point 2 and the centraliser of the permutation (1,2)
>
> * `Filtered( elts, g -> 2^g = 2 );`
>
> * `Filtered( elts, g -> (1,2)^g = (1,2) );`
{: .challenge}
