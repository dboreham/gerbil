= Gerbil Scheme =

Gerbil is a new dialect of scheme, designed around a multiresolution
macro-system.

The macro system is based on quote-syntax, and provides full the
meta-syntactic tower with a native implementation of syntax-case.
It also provides a full-blown module system, similar to plt scheme's
(sorry, racket) modules. The main difference from plt's modules is that
Gerbil modules are single instantiation, supporting high performance ahead
of time compilation.

== History of Gerbil ==
Gerbil has been my private Scheme for many years, evolved out of a set
of common macros that i used across different implementations. As such
i have multiple backends that work with the Gerbil macro system, but I
have elected to base the primary version of Gerbil on Gambit.

At the prompting of fare and mikael (they know who they are), who
had seen private versions of Gerbil, I decided to release it in public
with a clean bootstrap version that bootstraps on gambit with a precompiled
version of the macro system and a compiler for Gambit.
That means that the macro system and Gambit compiler is entirely
self-hosted.

= License and Copyright =

The source code is distributed under the Gambit license; that means
that Gerbil on Gambit is dual licensed under LGPLv2.1 and Apache 2.0.

Gerbil's primary author and maintainer is vyzo-at-hackzen.org, aka in
the Net as Dimitris Vyzovitis. The obligatory copyright notice, had I
bothered polluted everything with more than a (C) vyzo at hackzen.org,
would read like this:

(C) 2007-2016 Dimitris Vyzovitis <vyzo -at- hackzen.org>
Gerbil is Free Software, distributed under the GNU LGPLv2.1 or later
and the Apache 2.0 license.

= Installation =
== Source Code ==
The source code for Gerbil is hosted on [Github](https://github.com/vyzo/gerbil).
You can obtain the source tree directly in the command line by checking
out the sources:
$ git clone https://github.com/vyzo/gerbil.git

== Dependencies ==
I have tested the bootstrap with Gambit v4.8.4, but older versions
starting with v4.6.0 should works as well.

The :std/xml library in std requires libxml2 to build; comment it out
xml stuffs in src/std/build.ss if you don't have it.
The initial std library is an initial packaging of libraries that worked
with the Gambit bootstrap out of the box. I am continuously porting
more libraries from the various private versions of Gerbils, so you should
expect more libraries to be continously merged.

== Build Instructions ==
After checking out the source code from Github, let GERBIL_HOME be the
top directory of Gerbil.
Then:
$ cd $GERBIL_HOME/src
$ ./build.sh

this will execute a full bootstrap build in place, starging from the
pre-compiled Scheme sources in $GERBIL_HOME/src/bootstrap.

= Using Gerbil =
The Gerbil interpreter is $GERBIL_HOME/bin/gxi, and the compiler is
in $GERBIL_HOME/bin/gxc.

If you want an interactive Gerbil shell just execute the interpreter
directly by running gxi.

If you want to write a runnable Gerbil script, add $GERBIL_HOME/bin
to your PATH and use the following for your magic:
```
\#!/usr/bin/env gxi-script
```

You can define a main procedure in your script that will receive
the command line arguments.

For an example script, put the following in hello.ss
```
\#!/usr/bin/env gxi-script

(def (main . args)
 (displayln "Hello world! My arguments are " args))
```

Running the script with
```
chmod +x hello.ss
./hello.ss 1 2 3
```

should produce the following output:
```
Hello world! My arguments are (1 2 3)
```

= Documentation =

This README is intended to seasoned scheme hackers anyway, which
assumes that you can find your way around the source code; the code
should be self-documenting, except for the really hairy parts.

There is no further documentation at this point, because I haven't
had the time to prepare some nice and coherent documentation that
can help scheme neophytes (or people who like neat documentation
before using a new scheme system; I hope to write some real
documentation in the not-so-distant future. Check the Github
repository, as I intend to host documentation directly on Github
with github-pages.

Patches (even for typos in the comments) are always welcome.
No copyright assignment ever, you keep what you contribute.
