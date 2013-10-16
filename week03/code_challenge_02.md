*Portland Code School*
#Ruby Code Challenge 2


## Overview

[HQ9+](http://esolangs.org/wiki/HQ9_Plus) - see [this blog post](http://cliffle.com/esoterica/hq9plus.html) - is a programming joke. Not a shameful example of programming, but a thing that makes programmers laugh (or at least shake their head and smile whimiscally). It has a bunch of code that sounds impressive but (IMHO) doesn't really provide anything of value to a customer. It also is a way to try some simple and some difficult programming challenges.

Work in pairs. One person can create the repo and make sure the other person can push to it. Then, both participants just clone it. Make sure both people get a copy of the repo at the end. Switch drivers when it makes sense. Play to your strengths, but change it up and challenge yourself.

Be prepared to demonstrate your code as a pair Monday night.

Note that there are other repos on github that purport to solve this code challenge. Use them in your learning process if you want (it would be better to problem-solve with your classmates at a hack session), but frankly, some of their code is ugly. If you steal their code, people will notice when you do a code walkthrough and think less of you. Also, you won't learn anything. 


**Note: Whatever code you write must adhere to [this style guide](https://github.com/bbatsov/ruby-style-guide) so use [the checker that goes with it](https://github.com/bbatsov/rubocop) as you code.**


Everybody should do the "easy" homework. Then, try the "medium" tasks and, if you can, do the "hard" ones. Get as far as you can.

## Deadline
Your deadline for the code challenge is next Monday at 6pm. We will start the code walkthroughs right after warmup. You can send me email and I'll look at your github repo if you need advice, or come to the hack sessions and we can talk about it.


## Easy homework
Topics: Classes, variables, and methods

0. Create an HQ9F class (http://esolangs.org/wiki/HQ9_Plus)
0. Create a github repo to hold your work.
0. Inside this class create 3 methods: H, _99, and +
	* "H" should simply print out "Hello World!" and quit
	* "_99" should take 1 variable: the number of bottles of beer on the wall. It should output the lyrics to the hugely popular "99 Bottles Of Beer On The Wall" song, including a sad lament when there is no more beer.
	* "+" increments the accumulator (I personally find this the funniest part)


This class should respond to:
~~~~ruby
h              # (this is a *global function*)
HQ9F._99(99)   # (this is a *class method*)
win = HQ9F.new # (this is the initializer)
win.+          # (this is an *instance method*)
~~~~

## Medium homework

Topic: Modules and over-riding methods (with a hint of blocks and Procs thrown in)

0. Add an 'each' method to your HQ9F class and `include Enumerable`. The class should use an array internally as storage, and 'each' just needs to iterate over that array.
0. Once 'each' works, try using 'reject' or 'map' to look at the internal state of the array
0. Write a unit test that verifies the 'each' method


## Hard homework

Topic: Really esoteric stuff. :-) And test coverage.

0. Add a 'q' method to HQ9F which prints out the source code of the file. This is called a "quine".
0. See if you can do this without using IO.read to just read the source file. :)
0. Write unit tests that verify all methods. How do you know you have tested everything?


<hr />
Copyright © 2013 Alan Zimmerman <br />
Used by permission by Portland Code School