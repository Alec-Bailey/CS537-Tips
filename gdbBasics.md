# Basic GDB

## Setup
1. Compile with -ggdb (on GCC compiler at least)
This avoids most (not all) optimized out issues
2. Ensure you disable all compiler optimizations -O3 etc..

## Breakpoints
1. ctrl + c interrupt your program
2. ```b``` sets a breakpoint
    1. Break on a function name ```b doSomething```
    2. Or a line number in any valid file in the context file.c:lineNum ```b proc.c:420```

## More control flow
1. ```c``` Just continues on until the next breakpoint
2. ```n``` Moves to the next line of execution

What about if I'm stepping through and want to finish a loop?

3. ```until XXX``` where xxx is the line number just after the loop, this works like a "one time" breakpoint

4. This should get you through, breakpoints and until, with the ability to step line by line are very powerful. Check the reference for even more powerful tools, including conditional break points etc.

## Basic Printing
1. ```p myVariableName``` - Prints a variable name
2. ```p $eax``` - Print the value in any register

3. Pointers can be dereferenced just like in the code itself
    1. ```p *pstat``` - shows values inside struct pstat
    2. ```someStructPointer->someArray[5]``` - Same idea

4. This gets messy with large structures or arrays, so try prettyprint
```set print pretty on```

## More advanced debugging (with xv6)
1. Debugging user programs (non-trivial)
    1. ```symbol-file _fileName``` - Loads the appropriate userprogram symbol-file. Note this switches your context to exist only in the user-space
    2. For some compilcated reasons, if you set a breakpoint in a user program before xv6 is initalized, you will sporadically hit the break point. Allow XV6 to start completely, then interrupt it to set a break point. Finally, run your userprogram.

2. We can chose whether or not to remain within the parent or child's execution when calling fork()
```set follow-fork-mode (parent|child)```
by default GDB is set to follow parent, change with
```set follow-fork-mode child``` to switch to child's execution instead! (Check the docs for all the different ways to handle this case)

## Resources you should use
1. This is the best resource I have found - contains just about everythig you'd ever want to do.
[GDB Master Resource](https://sourceware.org/gdb/current/onlinedocs/gdb/index.html)
2. 15 minutes and shows off graphical mode for GDB & some more advanced features
[15 Minutes to change your view of GDB](https://www.youtube.com/watch?v=PorfLSr3DDI)
