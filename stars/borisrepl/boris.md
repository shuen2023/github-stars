---
project: boris
stars: 2153
description: A tiny REPL for PHP
url: https://github.com/borisrepl/boris
---

Boris
=====

A tiny, but robust REPL for PHP.

> **Announcement:** I'm looking to add one or two additional collaborators with commit access. If you are actively involved in open source and have a GitHub profile for review, ping me on Twitter (@d11wtq) to express your interest. Experienced developers with active GitHub projects only.

Python has one. Ruby has one. Clojure has one. Now PHP has one, too. Boris is PHP's missing REPL (read-eval-print loop), allowing developers to experiment with PHP code in the terminal in an interactive manner. If you make a mistake, it doesn't matter, Boris will report the error and stand to attention for further input.

Everything you enter into Boris is evaluated and the result inspected so you can understand what is happening. State is maintained between inputs, allowing you to gradually build up a solution to a problem.

> **Note:** The PCNTL function which is required to run Boris is not available on Windows platforms.

Why?
----

I'm in the process of transitioning away from PHP to Ruby. I have come to find PHP's lack of a real REPL to be frustrating and was not able to find an existing implementation that was complete. Boris weighs in at a few hundred lines of fairly straightforward code.

Usage
-----

Check out our wonderful wiki for usage instructions.

Contributing
------------

We're committed to a loosely-coupled architecture for Boris and would love to get your contributions.

Before jumping in, check out our **Contributing contributing** page on the wiki!

Contributing
------------

We're using PHPUnit for testing. To run all the tests,

```
phpunit --bootstrap tests/autoload.php -c tests.xml
```

Core Team
---------

This module was originally developed by Chris Corbyn, and is now maintained by Tejas Manohar, Dennis Hotson, and other wonderful contributors.

Copyright & Licensing
---------------------

See the LICENSE file for details.
