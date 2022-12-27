# The Little Schemer

This repo conatins my notes and code from [The Little Schemer](https://mitpress.mit.edu/9780262560993/the-little-schemer/) 4th edition. 

This repo will evolve as I learn more about Scheme and work my way through [The Little Schemer](https://mitpress.mit.edu/9780262560993/the-little-schemer/),  [The Little Prover](https://mitpress.mit.edu/9780262527958/the-little-prover/), and perhaps [The Little Typer](https://mitpress.mit.edu/9780262536431/the-little-typer/). 

I've selected these books because I hit a pretty major roadblock while trying to read [PROGRAM = PROOF](https://www.lix.polytechnique.fr/Labo/Samuel.Mimram/teaching/INF551/course.pdf) and [Principles of Abstract Interpretation](https://mitpress.mit.edu/9780262044905/principles-of-abstract-interpretation/) which humbled me enough to return to the basics. I've selected *"The Little X"* series of books as a gentle introduction to LISP/Scheme and to work my way into lambda calculus, functional programming, and proof assistants like [Coq](https://en.wikipedia.org/wiki/Coq) and [Agda](https://en.wikipedia.org/wiki/Agda_(programming_language)) through the books listed above and other resources.

## The Book

[The Little Schemer](https://mitpress.mit.edu/9780262560993/the-little-schemer/) has one of the most intertesting formats of any non-fiction book I've ever read. It's presented in a question and answer conversation between the authors and a student of Scheme. Through reading this dialog you start to pick up on details of Scheme and learn as you progress through the increasingly more difficult conversation.

## Getting Started with Scheme

Scheme is an interesting language. Unlike say Python, you don't just install "the interpreter" - instead you install a Scheme implementation, of which there are *many*.

After researching and trying a few I was split between [Gambit Scheme](http://www.gambitscheme.org/) and [CHICKEN Scheme](http://wiki.call-cc.org/). Both have some very appealing features, like Gambit's ability to compile to multiple languages including C and Python. But ultimately I decided to go with CHICKEN Scheme for some minor reasons mainly related to documentation and the fact that "The Little Schemer" uses food as a basis for a lot of its examples (sorry vegans).

### Installing CHICKEN Scheme

Both Gambit and CHICKEN are included in major package managers. But for me, I'll be installing CHICKEN Scheme on a Ubuntu 22.04 LTS system with `apt`.

```
sudo apt install chicken-bin
```

### Verifying Installation

Once installation is complete check to make sure the interpreter and compiler and ready to use:

```
# CHICKEN interpreter (csi)
user@devbox:~/$ csi -version
CHICKEN
(c) 2008-2020, The CHICKEN Team
(c) 2000-2007, Felix L. Winkelmann
Version 5.2.0 (rev 317468e4)
linux-unix-gnu-x86-64 [ 64bit dload ptables ]

# CHICKEN compiler (csc)
user@devbox:~/$ csc -version
CHICKEN
(c) 2008-2020, The CHICKEN Team
(c) 2000-2007, Felix L. Winkelmann
Version 5.2.0 (rev 317468e4)
linux-unix-gnu-x86-64 [ 64bit dload ptables ]
```

Now we can run our first Scheme file `tests/smoketest.scm` through the interpreter (csi). First, let's take a look at the contents:

```scheme
user@devbox:~/$ cat tests/smoketest.scm
(display "Looks like we're cooking with fire!") (newline) (exit)
```

This just prints a string to the screen with a newline and exits. We can run it with the `-q` or `--quiet` switch to suppress the banner

```
user@devbox:~/$ csi -q tests/smoketest.scm
Looks like we're cooking with fire!
```

At this point we're about as ready to dive into The Little Schemer as we'll ever be.

### Getting Help

If you need help, check out the man pages:

```
user@devbox:~/$ man csi
user@devbox:~/$ man csc
```

The official [CHICKEN Scheme documentation](http://wiki.call-cc.org/man/5/The%20User%27s%20Manual).

Learn X in Y minutes has [a nice document on CHICKEN](https://learnxinyminutes.com/docs/CHICKEN/).

## The Scheme Files & Notes

My Scheme files and notes are broken down by chapter in the `/chapters` directory. See the `README.md` in each chapter's folder for notes and Scheme files.

