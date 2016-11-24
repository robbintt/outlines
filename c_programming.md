


### Resources

A list of resources, subdivide as it grows.

1. [The slideshow that got me started here](https://news.ycombinator.com/item?id=9635230)
2. [comp.lang.c guide](http://www.c-faq.com/)
3. [C Standard Library](http://en.wikipedia.org/wiki/C_standard_library)
4. [C POSIX Library](http://en.wikipedia.org/wiki/C_POSIX_library)
5. [C++ STL - Standard Template Library](http://en.wikipedia.org/wiki/Standard_Template_Library)
6. [gcc docs](https://gcc.gnu.org/onlinedocs/gcc/)
7. [LLVM Sanitizers (Google)](https://github.com/google/sanitizers)


### Codebases to read and participate in

1. `sqlite3`
2. `python3`



### how 2 be 1337

[Knuth Reward Check](https://en.wikipedia.org/wiki/Knuth_reward_check) - In the preface of each of his books and on his website,[7] Knuth offers a reward of $2.56 (USD) to the first person to find each error in his published books, whether it be technical, typographical, or historical. Knuth explains that $2.56, or 256 cents, corresponds to one hexadecimal dollar.[8] "Valuable suggestions" are worth 32 cents, or about  1⁄8 of the errors in the book (0.001 hexadecimal dollars or 0.1 hexadecimal cents). In his earlier books a smaller reward was offered. For example, the 2nd edition of The Art of Computer Programming, Volume 1, offered $2.00.


### Others' Resources

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
        > I am always annoyed that the designated initializers ( { .a = 42} ) don't work in C++. Sometimes I just sprinkle in a C file for initializers

