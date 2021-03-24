# Basic GDB

## Setup
1. Compile with -ggdb (on GCC compiler at least)
This avoids most (not all) optimized out issues
2. Ensure you disable all compiler optimizations -O3 etc..

## Breakpoints
1. ctrl + c interrupt your program
2. ```b```sets a breakpoint
3. ```c``` continues execution until breakpoint

## More control flow
1. ```c``` Just continues on until the next breakpoint
2. ```n``` Moves to the next line of execution

What about if I'm stepping through and want to finish a loop?

3. ```until XXX``` where xxx is the line number just after the loop, this works like a "one time" breakpoint


## Basic Printing
1. ```p myVariableName``` - Prints a variable name
2. ```p $eax``` - Print the value in any register

3. Pointers can be dereferenced just like in the code itself
```p *pstat``` - shows values in side struct pstat
```someStructPointer->someArray[5]``` - Same idea

4. This gets messy, so try prettyprint
```show print pretty```

## More advanced debugging (with xv6)
1. Debugging user programs (non-trivial)
	a. ```symbol-file _fileName``` - Loads the appropriate userprogram symbol-file. Note this switches your context to exist only in the user-space
	b. For some compilcated reasons, if you set a breakpoint in a user program before xv6 is initalized, you will
	   sporadically hit the break point. Allow XV6 to start completely, then interrupt it to set a break point. Finally, run your userprogram.

2. We can chose whether or not to remain within the parent or child's execution when calling fork()
```set follow-fork-mode (parent|child)```
by default GDB is set to follow parent, change with
```set follow-fork-mode child``` to switch to child's execution instead! (Check the docs for all the different ways to handle this case)

## Resources you should use
1. This is the best resource I have found - contains just about everythig you'd ever want to do.
https://sourceware.org/gdb/current/onlinedocs/gdb/index.html
2. 15 minutes and shows off graphical mode for GDB & some more advanced features
https://www.youtube.com/watch?v=PorfLSr3DDI