# Scheme Primer

Please note that all Scheme implementations have unique quirks and deviations from the Scheme standard. In general, most of what we'll cover here should just work in whatever Scheme system you're using. I'll be using [CHICKEN Scheme](http://wiki.call-cc.org/) for this primer along with the CHICKEN Scheme Interpreter or `csi`.

You can also check out the Learn X in Y minutes entry for CHICKEN [here](https://learnxinyminutes.com/docs/CHICKEN/).

As someone who uses Python on a daily basis, I found the [Pointless Programming Language Reference](https://plr.sourceforge.net/cgi-bin/plr/display.py?languages=English&languages=Python&languages=Chicken) extremely helpful for how to accomplish things in CHICKEN Scheme much like I would in Python.

# Setup

In this primer, we'll assume you're using CHICKEN Scheme on Ubuntu. To install it run:

```
sudo apt update
sudo apt install chicken-bin
```

# The Basics

Let's head into the interpreter and start evaluating some basic elements of Scheme. To enter the CHICKEN Scheme Interpreter ("csi") run the following command:

```
csi
```

You should see something like this:

```
CHICKEN
(c) 2008-2020, The CHICKEN Team
(c) 2000-2007, Felix L. Winkelmann
Version 5.2.0 (rev 317468e4)
linux-unix-gnu-x86-64 [ 64bit dload ptables ]

Type ,? for help.
#;1> 
```

If you need to quit type `",q"` then `<enter>`.

## Using Functions

In most languages, to evaluate a simple expression like `1 + 2` you simply use `1 + 2` in the intuitive [infix notation](https://en.wikipedia.org/wiki/Infix_notation). However that is not the case in Scheme, which uses the rather odd [prefix or Polish notation](https://en.wikipedia.org/wiki/Polish_notation) `+ 1 2`.

Let's add some numbers together.

### Addition

```scheme
> (+ 1 2)
3

> (+ 1 2 3)
6

> (+ 1)
1

> (+)
0

> (+ 1 2.14)
3.14

> (+ 1 2 3 4 5 6 7 8 9)
45

> + 1 1
<procedure C_plus>
1
1
```

Once you get past the use of Polish notation it's rather elegant that you don't need to repeat the operation you're using (`+`) over and over again. However, we start to see strange things happen when we don't enclose the expression in parenthesis.

In Scheme, parenthesis `(` and `)` are extremely important as they mark the begining and end of a procedure (aka function call) and they also define scope of symbols. When we wrap our addition expression in `()` we're telling Scheme we want to use the addition procedure (`+`) with the specified parameters.

Let's continue with some other basic operations.

### Subtraction

```scheme
> (- 2 1)
1

> (- 2 1 1 1)
-1

> (- 4.14 1)
3.14

> (- 1)
-1

> (-)
Error: too few arguments - received 0 but expected 1

	Call history:

	<syntax>	  (-)
	<eval>	  (-)	<--

> - 1 1
<procedure C_minus>
1
1
```

### Division, Quotient, Remainder, Square Root

```scheme
> (/ 10 5)
2

> (/ 1 2)
1/2

> (/ 10 6)
5/3

> (/ 100 25)    
4

> (/ 100 25 2)
2

> (/ 100 25 2 1 1 1 1 1 1)
2

> (quotient 20 6)
3

> (remainder 20 6)
2

> (sqrt 9)
3

> (sqrt 2)
1.4142135623731

> (sqrt -1)
0.0+1.0i

> (/ 1 0)
Error: (/) division by zero
1
0

	Call history:

	<syntax>	  (/ 1 0)
	<eval>	  (/ 1 0)	<--
```

### Multiplication, Exponential

```scheme
> (* 2 3)
6

> (* 2 3 4)
24

> (* 2 3 4 0)
0

> (* 2 2 2 2 2)
32

> (expt 2 5)
32

> (expt 2 -1)
1/2
```

### Or, And, Not

```scheme
> (or 1 1)
1

> (or 1 0)
1

> (or 0 0)
0

> (and 1 1)
1

> (and 1 0)
0

> (not 1)
#f

> (not 0)
#f 

> (not #t)
#f

> (not #f)
#t
```

### Positive?, Negative?, Zero?, Eq?

```scheme
> (positive? 1)
#t

> (positive? -1)
#f

> (positive? 0)
#f

> (negative? 1)
#f

> (negative? -1)
#t

> (negative? 0)
#f

> (zero? 1)
#f

> (zero? -1)
#f

> (zero? 0)
#t

> (zero? (- 1 1))
#t

> (eq? 0 0)
#t

> (eq? 0 1)
#f
```

## Booleans

Booleans in Scheme are defined as `#t` for true and `#f` for false.

## Lists

Since `(` and `)` are used for procedures in Scheme, when we define a list, we need some way of telling the interpreter we mean a list `()` and not a procedure. This is done by adding a single quote `'` before the list `'()`.

```scheme
> '(1 2 3)
(1 2 3)

> '()
()

> ()
Error: illegal non-atomic object: ()

> (1 2 3)
Error: call of non-procedure: 1

	Call history:

	<syntax>	  (1 2 3)
	<eval>	  (1 2 3)	<--

> (eq? '(1 2 3) '(1 2 3))
#f

> (eq? '() '())
#t
```

## Numbers

As we've seen in previous examples, Scheme supports various number types including real, floating point, and imaginary numbers.

```scheme
> (sqrt -1)
0.0+1.0i

> (expt 0.0+1.0i 2)
-1.0

> (expt i 2)
Error: unbound variable: i

	Call history:

	<syntax>	  (expt i 2)
	<eval>	  (expt i 2)	<--

> (expt 1.0i 2)
Error: unbound variable: 1.0i

	Call history:

	<syntax>	  (expt 1.0i 2)
	<eval>	  (expt 1.0i 2)	<--

> (expt +1i 2)
-1

> (expt +1.0i 2)
-1.0

> (+ 1 1)
2

> (+ 1 1.0)
2.0

> (eq? 2 2)
#t

> (eq? 2 2.0)
#f

; Note this is a comment

> #b1010    ; binary
10

> #o10      ; octal
8

> #xFF      ; hex
255
```

## Strings

Strings in Scheme are just quoted text.

```scheme
> "Hello"
"Hello"

> "*12345^&*(*"
"*12345^&*(*"

> (eq? "Hello" "Hello")
#f

> (eq? "" "")
#f

> (- "Hi" "i")
Error: (-) bad argument type - not a number: "Hi"

	Call history:

	<syntax>	  (- "Hi" "i")
	<eval>	  (- "Hi" "i")	<--

> (substring "Hi" 0 1)
"H"
```

## Variables

Scheme has two ways of declaring variables `define` and `let`. `Define` will declare a variable on "global scope" while `let` will declare a variable in local scope. 

```scheme
> (define x 2)

> x
2

> (+ x 3)
5

> (let y 2)
Error: during expansion of (let ...) - in `let' - not a proper list: (let y 2)

	Call history:

	<syntax>	  (let y 2)	<--

> (let (y 2))
Error: during expansion of (let ...) - in `let' - pair expected: (let (y 2))

	Call history:

	<syntax>	  (let (y 2))	<--

> (let ((y 2)))
Error: during expansion of (let ...) - in `let' - not enough arguments: (let ((y 2)))

	Call history:

	<syntax>	  (let ((y 2)))	<--

> (let ((y 2)) y)
2

> y
Error: unbound variable: y

> (let ((name "John")) (print name))
John
```
