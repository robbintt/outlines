

### Notes - K&R - The C Programming Language

1. How to read "statements" in C (k&r: p. 19)
    - One "statement" can be a single statement, like `int c;`, or a group of statements inside braces
    - A control flow keyword also initiates a single statement:
    ```
    /* this is one statement, even though it is two nested control flow keywords */
    while ((c = getchar()) != EOF)
      if (c == '\n')
        ++nl;
    ```
2. Assignments associate from right-to-left
    - The following are equivalent:
        - `nl = nw = nc = 0`
        - `nl = (nw = (nc = 0))`
3. Evaluations with `&&` and `||` are left-to-right
    - `if (c == ' ' || c == '\n' || c == '\t')`
    - Evaluation stops as soon as truth or falsehood is known, "short-circuit" or "minimal" evaluation


### Resources

A list of resources, subdivide as it grows.

1. [The slideshow that got me started here](http://charliethe.ninja/2015/05/29/intro_to_c.html)
    - [Originally found here](https://news.ycombinator.com/item?id=9635230)
2. [comp.lang.c guide](http://www.c-faq.com/)
3. [C Standard Library](http://en.wikipedia.org/wiki/C_standard_library)
4. [C POSIX Library](http://en.wikipedia.org/wiki/C_POSIX_library)
5. [C++ STL - Standard Template Library](http://en.wikipedia.org/wiki/Standard_Template_Library)
6. [gcc docs](https://gcc.gnu.org/onlinedocs/gcc/)
7. [LLVM Sanitizers (Google)](https://github.com/google/sanitizers)
8. [What is the datatype of a pointer in c?](http://stackoverflow.com/questions/3976326/what-is-the-datatype-of-pointer-in-c)
    - henner says: a `long` in any particular system should be able to hold a pointer
9. [Tips on printf (escape sequences)](http://web.mit.edu/10.001/Web/Course_Notes/c_Notes/tips_printf.html)
10. [Wikipedia "Escape sequences in C"](https://en.wikipedia.org/wiki/Escape_sequences_in_C)
11. [a make guide](http://mrbook.org/blog/tutorials/make/)
12. [gnu make guide](https://www.gnu.org/software/make/manual/make.html)
13. Ascii table: `man ascii`
14. [Learn x in y minutes: C](https://learnxinyminutes.com/docs/c/)

#### Definitions

1. `gcc` - gnu compiler collection
2. `gnu binutils` - sister project of gcc
3. `avr-gcc` - version of gcc for the avr class of microcontrollers
    - has 3 available compilers: `c`, `c++`, `ada`
    - compiler does not assemble or link the final code
4. `gas` - gnu assembler 
5. `GNU Libc` - GNU C Standard Library
    - 
6. `AVR Libc` - AVR GCC C Standard Library
7. `GNU Make` - Building software / Makefile stuff
    - Some distributions of the toolchains, and other AVR tools such as MFile, contain a Makefile template written for the AVR toolchain and AVR applications that you can copy and modify for your application.
8. `AVRDUDE` - program your device
9. `avr-gdb`, `avr-insight`, and `ddd`
    - avr versions of common make tools.
10. `AVaRICE` - AVaRICE is a back-end program to AVR GDB and interfaces to the Atmel JTAG In-Circuit Emulator (ICE), to provide emulation capabilities.
11. `SimulAVR` - SimulAVR is an AVR simulator used as a back-end with AVR GDB.
12. `SRecord` is a collection of powerful tools for manipulating EPROM load files. It reads and writes numerous EPROM file formats, and can perform many different manipulations.
13. `MFile` is a simple Makefile generator is meant as an aid to quickly customize a Makefile to use for your AVR application.
 


### Codebases to read and participate in

1. `sqlite3`
2. `python3`



### how 2 be 1337

[Knuth Reward Check](https://en.wikipedia.org/wiki/Knuth_reward_check) - In the preface of each of his books and on his website,[7] Knuth offers a reward of $2.56 (USD) to the first person to find each error in his published books, whether it be technical, typographical, or historical. Knuth explains that $2.56, or 256 cents, corresponds to one hexadecimal dollar.[8] "Valuable suggestions" are worth 32 cents, or about  1⁄8 of the errors in the book (0.001 hexadecimal dollars or 0.1 hexadecimal cents). In his earlier books a smaller reward was offered. For example, the 2nd edition of The Art of Computer Programming, Volume 1, offered $2.00.


### Learn C The Hard Way (Zed Shaw)

Some notes as I read through lcthw.


#### Quickref

1. `: ?` (same category as `&&` `||` `!`) is `logical ternary`. Expression `a:b?c` maps to `if a then b else c`


#### Keywords - Alphabetical

- case: A branch in a switch-statement.
- char: Character data type.
- const: Make a variable unmodifiable.
- continue: Continue to the top of a loop.
- default: Default branch in a switch-statement.
- do: Start a do-while loop.
- double: A double floating point data type.
- else: An else branch of an if-statement.
- enum: Define a set of int constants.
- extern: Declare an identifier is defined externally.
- float: A floating point data type.
- for: Start a for-loop.
- goto: Jump to a label.
- if: Starts an if-statement.
- int: An integer data type.
- long: A long integer data type.
- register: Declare a variable be stored in a CPU register.
- return: Return from a function.
- short: A short integer data type.
- signed: A signed modifier for integer data types.
- sizeof: Determine the size of data.
- static: Preserve variable value after its scope exits.
- struct: Combine variables into a single record.
- switch: Start a switch-statement.
- typedef: Create a new type.
- union: Start a union-statement.
- unsigned: An unsigned modifier for integer data types.
- void: Declare a data type empty.
- volatile: Declare a variable might be modified elsewhere.
- while: Start a while-loop.


#### Keywords - Grouped

Note: keywords in C only fall into two categories: `data management` and `control flow`


##### Data Types & Modifiers

- int: An integer data type.
- long: A long integer data type.
- short: A short integer data type.

- signed: A signed modifier for integer data types.
- unsigned: An unsigned modifier for integer data types.

- char: Character data type.

- float: A floating point data type.
- double: A double floating point data type.

- const: Make a variable unmodifiable.
- volatile: Declare a variable might be modified elsewhere.
- extern: Declare an identifier is defined externally.
- void: Declare a data type empty.
- static: Preserve variable value after its scope exits.
- register: Declare a variable be stored in a CPU register.
- auto: Give a local variable a local lifetime.


##### Compound Data Types

- struct: Combine variables into a single record.

- union: Start a union-statement.
- enum: Define a set of int constants.

- typedef: Create a new type.


##### Data Introspection

- sizeof: Determine the size of data.


##### Control Flow

- if: Starts an if-statement.
- else: An else branch of an if-statement.

- for: Start a for-loop.

- do: Start a do-while loop.
- while: Start a while-loop.

- continue: Continue to the top of a loop.
- break: Exit out of a compound statement.

- switch: Start a switch-statement.
- case: A branch in a switch-statement.
- default: Default branch in a switch-statement.

- goto: Jump to a label.

- return: Return from a function.


#### LCTHW References

- `man 3 printf`
- `gdb quickref` - learn c the hard way page 36-37
    - mentions: run, break, backtrace, print expr, continue, next, step, quit, help, cd, pwd, make, shell, clear, info break, info watch, attach pid, detach, list
- `lldb quickref` - learn c the hard way page 37-38
    - mentions: run [args], breakpint set, thread backtrace, print expr, continue, next, step, quit, help, cd, pwd, make, shell, clear, info break, info watch, attach -p pid, detach, list
- use `gdb` or `lldb` to debug your compiled program
    - type `run` in the debugger command line to run the application
        - a bunch of helpful `gdb` debugging flags from zed
        - `gdb --args ./ex3 myarg1 myarg2 myargetc` pass args to program
    - apple: `lldb` has the same commands available but you have to read the manpages for the llvm names
- `valgrind` - track all your memory and tell you when you messed it up
    - gotta know how to work with the `heap`
    - `valgrind ./ex3`
- apple does not have valgrind:
    - `gdb --batch --ex run --ex bt --ex q --args ./ex3`
    - "a very lame alternative to valgrind, the most useful command for debugging c code"
- `splint` linter
- `address sanitizer` - asan
    - new alternative to `valgrind` that works on osx
    - [github.com/google/sanitizers/wiki/AddressSanitizer](https://github.com/google/sanitizers/wiki/AddressSanitizer)

#### LCTHW Makefile References
- always use tabs in `Makefile`s. Never spaces.
- `-g` generate debug information
- `-Wall` (gnu gcc)
    - From the manpage:   

>This enables all the warnings about constructions that some users consider questionable, and that are easy to avoid (or modify to prevent the warning), even in conjunction with macros.  This also enables some language-specific warnings described in C++ Dialect Options and Objective-C and Objective-C++ Dialect Options.


### Macros [(source)](https://gcc.gnu.org/onlinedocs/cpp/Macros.html)

> A macro is a fragment of code which has been given a name. Whenever the name is used, it is replaced by the contents of the macro. There are two kinds of macros. They differ mostly in what they look like when they are used. Object-like macros resemble data objects when used, function-like macros resemble function calls.

> You may define any valid identifier as a macro, even if it is a C keyword. The preprocessor does not know anything about keywords. This can be useful if you wish to hide a keyword such as const from an older compiler that does not understand it. However, the preprocessor operator defined (see Defined) can never be defined as a macro, and C++'s named operators (see C++ Named Operators) cannot be macros when you are compiling C++.


### Others' Resources

- zv says: `man ld.so` - it's worth your time in my view to at least skim the `ld.so` manpage

#### Mitch says: 

["The C Programming Language by Kernighan and Ritchie"](https://library.noisebridge.net/detail/627/)

#### TheAceOfHearts says: 

["C is a very small and simple language but the tooling and patterns are old and mysterious."](https://news.ycombinator.com/item?id=9635230)

1. make
2. autoconf
3. how the compiler + preprocessors work
    - what do all the flags even mean!?!?!
4. how making `cross platform` stuff works
5. how to pull in and use c "libraries"
6. C-isms
7. how to test
8. etc

1. some platform standards
    - `autotools` in GNU, `msbuild` on win


#### Lizzie says:

`make` - Some people do it strangely but ime 90% of makefiles do the exact same thing: "compile .c files to .o files with CFLAGS. link all the relevant .o files with LDFLAGS"

1. learn to use `asan` and `ubsan` right off the bat. They are `compiler extensions` for `dynamic bounds / overflow checking`.
    1. [asan: Address Sanitizer]()
    2. [ubsan: GCC Undefined Behavior Sanitizer]()
    3. `-fsanitize=address -fsanitize=undefined`

2. learning `gdb` also helps a lot
    1. [gdb]()

3. [klib](https://github.com/attractivechaos/klib) - a fast generic datastructure library for c

4. [c Language Lawyer perspective](http://c-faq.com/)

5. [Programming Lanugages - C  // International Standard 9899:201x Draft April 2011](http://www.open-std.org/jtc1/sc22/wg14/www/docs/n1570.pdf)

6. Check out `struct initializers` - not a common pattern but been around for 20 years. 

    ```c
    struct mystruct mydata = {.b = c, .d = e};
    ```
vs
    ```c
    struct mystruct mydata;
    memset(&mydata, 0, sizeof(mydata));
    mydata.b = c;
    mydata.d = e;
    ```
    - removes potential bugs:
        - passing the wrong size to memset
        - getting the size and value arguments to memset reversed on accident.
        - using mydata before it's initialized
        - memsetting a pointer, which is UB
    - note from henner:
        - > I am always annoyed that the designated initializers ( { .a = 42} ) don't work in C++. Sometimes I just sprinkle in a C file for initializers

