# A Plan to Learn Rust

I was planning on learning C but it's tough to get up to speed and people seem to have wildly varying practices. It would be better to learn low level things in a modern context with less baggage.


## The Plan


### Todo

- Go through the book (2nd edition) and check out the community maintained git repo.
- Skip the git project of examples for now, I've checked them out before and should learn the rust book before checking them out again.
- How do I get a .gitignore to be generated when I do `cargo new --bin variables` or similar?
- What's the deal with shadowing? Sure it's fine, but you could end up with a bunch of values that never get garbage collected, what other tradeoffs are there? Perhaps the same type management issues that Python is attempting to solve with type annotation. Why use shadowing?


### Done

- Learn about `rustup` and how to maintain your `rust` toolchain. Hopefully build an analogy to `python-virtualenv`.


## Ingesting Anthologies and Aggregators of Rust Information


## More Resource Compilations to Ingest

- [Rust Anthology](https://github.com/brson/rust-anthology/blob/master/master-list.md)
- [readrust.net interesting post aggregator](https://readrust.net/)
- [rust community blog](http://blog.community.rs/en-US/)
- [project euler in rust](https://github.com/gifnksm/ProjectEulerRust)
- [hackr.io tutorials learn-rust tutorials and courses](https://hackr.io/tutorials/learn-rust)
- [rust design patterns](https://github.com/rust-unofficial/patterns)

## Already Ingested Here & Date

- [rust-learning](https://github.com/ctjhoa/rust-learning) - 2018.08.13


## Tools

Tools for Rust.

### Places to get help

> there are a number of places you can get help. The easiest is the #rust IRC channel on irc.mozilla.org, which you can access through Mibbit. At that address you can chat with other Rustaceans (a silly nickname we call ourselves) who can help you out. Other great resources include the Users forum and Stack Overflow.

### Local Documentation

try: `rustup doc`

### rustup


#### Switch between `stable` and `nightly`

you will need some or all of these: 

- `rustup update`
- `rustup install nightly`
- switch with: `rustup default nightly` or `rustup default stable`



> rustup installs The Rust Programming Language from the official release channels, enabling you to easily switch between __stable, beta, and nightly compilers__ and __keep them updated__. It makes cross-compiling simpler with binary builds of the standard library for common platforms. And it runs on all platforms Rust supports, including Windows. (emphasis mine)

> rustup is a toolchain multiplexer. It installs and manages many Rust toolchains and presents them all through a single set of tools installed to ~/.cargo/bin. The rustc and cargo installed to ~/.cargo/bin are proxies that delegate to the real toolchain. rustup then provides mechanisms to easily change the active toolchain by reconfiguring the behavior of the proxies.


### Clippy

Linter - `nightly` only. Use it!



### Playpen

You can put your rust in a gist and put it in `Playpen` and then share it with others who can see it run. Good tool for collaboration.


### Crater

I don't think this is useful until I'm trying to switch between `stable` and `nightly` with tons of dependencies.

- detect regressions in rust compiler against a bunch of `crates`
- [github project](https://github.com/rust-lang-nursery/crater)
- Check the differences between `stable` and `target` 
    - only for sandboxed environments, it's very destructive... so I guess only on vms.



### Cargo

- [howto: specify cargo dependencies](https://doc.rust-lang.org/cargo/reference/specifying-dependencies.html)
    - This is manual... but I prefer cargo-edit so far for add/rm/upgrade
- Make sure to `cargo install cargo-edit`
    - This gives you the ability to use `cargo add/rm/upgrade <crate>` for example `cargo add num_bigint`


- [Rust cargo guide](https://doc.rust-lang.org/cargo/guide/)

> Cargo is a tool that allows Rust projects to declare their various dependencies and ensure that you’ll always get a repeatable build.  To accomplish this goal, Cargo does four things:

> 1. Introduces two metadata files with various bits of project information.
> 1. Fetches and builds your project’s dependencies.
> 1. Invokes rustc or another build tool with the correct parameters to build your project.
> 1. Introduces conventions to make working with Rust projects easier.

### GDB

- [GDB supports Rust](https://sourceware.org/gdb/onlinedocs/gdb/Rust.html)
    - Lizzie says no one uses it


## "The Book 2nd Ed." aka "The Rust Programming Language"

>  When you finish this you will be an intermediate rust programmer.

> In general, this book assumes that you’re reading it in sequence from front to back. Later chapters build on concepts in earlier chapters, and earlier chapters might not delve into details on a topic; we typically revisit the topic in a later chapter.

> You’ll find two kinds of chapters in this book: concept chapters and project chapters. In concept chapters, you’ll learn about an aspect of Rust. In project chapters, we’ll build small programs together, applying what you’ve learned so far. Chapters 2, 12, and 20 are project chapters; the rest are concept chapters.


### Rust 101 Youtube (20 Jan 2017)

- Speaker: E. Dunham; @qedunham
- [source](https://www.youtube.com/watch?v=FMqydRampuo)
- [slides](http://talks.edunham.net/lca2017/rust101.pdf)


#### Exercises

- [Rustlings repo](https://github.com/rustlings/rustlings)
- Rust By Example book


#### Macros

Macros are syntactic sugar for functions that take a variable number of arguments...

Need more content, see rust book v2.


#### Inclusive and Exclusive Ranges

- `..` is an exclusive range, `..=` is an inclusive range
    - This is true for both matches and expressions
    - The old match-only inclusive range syntax `...` is still acceptable in match-only but not recommended and does not work in expressions
    - See `rust book v2 appendix 6`
    




### Notes

- Rust is an `expression` based language 
    - `Statements` are instructions that perform some action and do not return a value. 
        - `let y = 6;` is a statement, it does not return a value
    - `Expressions` evaluate to a resulting value.
        - Expressions can be parts of statements: in `let y = 6`, the `6` is an expression that evaluates to `6`.
        - calling a `function` or calling a `macro` is an expression
        - calling the block to create new scopes, `{}`, is an expression
        - a function can have an expression and it will be returned by the function
    - other languages don't have the same distinctions
- blocks of code inside `if` expressions or `match` expressions are sometimes called `arms`
- Remember that blocks of code evaluate to the last expression in them


#### Chapter 2

> Switching from an `expect` call to a `match` expression is how you generally move from crashing on an error to handling the error. Remember that `parse` returns a `Result` type and Result is an enum that has the variants `Ok` or `Err`. We’re using a `match` expression here, as we did with the `Ordering` result of the `cmp` method.

> --- snip ---

> If `parse` is not able to turn the string into a number, it will return an `Err` value that contains more information about the error. The `Err` value does not match the `Ok(num)` pattern in the first `match` arm, but it does match the `Err(_)` pattern in the second arm. The underscore, `_`, is a catchall value; in this example, we’re saying we want to match all `Err` values, no matter what information they have inside them. So the program will execute the second arm’s code, `continue`, which tells the program to go to the next iteration of the `loop` and ask for another guess. So effectively, the program ignores all errors that `parse` might encounter!


#### Chapter 3

> Function bodies are made up of a series of statements optionally ending in an expression. So far, we’ve only covered functions without an ending expression, but you have seen an expression as part of a statement. Because Rust is an expression-based language, this is an important distinction to understand. Other languages don’t have the same distinctions, so let’s look at what statements and expressions are and how their differences affect the bodies of functions.  

> We’ve actually already used statements and expressions. Statements are instructions that perform some action and do not return a value. Expressions evaluate to a resulting value. Let’s look at some examples.

> So how do you know which type of integer to use? If you’re unsure, Rust’s defaults are generally good choices, and integer types default to i32: this type is generally the fastest, even on 64-bit systems. The primary situation in which you’d use isize or usize is when indexing some sort of collection.

> Floating-point numbers are represented according to the IEEE-754 standard. The f32 type is a single-precision float, and f64 has double precision.

> Rust’s char type represents a Unicode Scalar Value, which means it can represent a lot more than just ASCII. Accented letters; Chinese, Japanese, and Korean characters; emoji; and zero-width spaces are all valid char values in Rust. Unicode Scalar Values range from U+0000 to U+D7FF and U+E000 to U+10FFFF inclusive. However, a “character” isn’t really a concept in Unicode, so your human intuition for what a “character” is may not match up with what a char is in Rust. We’ll discuss this topic in detail in “Strings” in Chapter 8.


## Resources

Resources from main rust site.


### "Are we _ yet?"

- [web app stuff](http://www.arewewebyet.org/)
- [game stuff](http://arewegameyet.com/)
- also check out "things that are [not awesome yet in rust](https://github.com/not-yet-awesome-rust/not-yet-awesome-rust)"





### Articles

Summaries go below.

- A list of ['fearless rust bloggers'](https://users.rust-lang.org/t/fearless-rust-bloggers/16770)
- [Tutorials & Workshop Materials](https://github.com/ctjhoa/rust-learning#tutorials--workshop-materials)
- [hackr.io tutorials](https://hackr.io/tutorials/learn-rust)


#### ["Rust for Python Developers" by Armin Ronacher](http://lucumr.pocoo.org/2015/5/27/rust-for-pythonistas/)


##### Mutability, Borrows, and Owners

> Functions that operate on immutable borrows are marked as &self and functions that need a mutable borrow are marked as &mut self. You can only loan out references if you are the owner. If you want to move the value out of the function (for instance by returning it) you cannot have any outstanding loans and you cannot loan out values after having moved ownership away from yourself.

> This is a big change in how you think about programs but you will get used to it.


##### [Three rust things Armin wishes he learned earlier](http://lucumr.pocoo.org/2018/3/31/you-cant-rust-that/)


##### [RUST'S OWNERSHIP MODEL FOR JAVASCRIPT DEVELOPERS](https://blog.thoughtram.io/rust/2015/05/11/rusts-ownership-model-for-javascript-developers.html)


##### [github py2rs](https://github.com/rochacbruno/py2rs)


##### [rust for node developers](https://github.com/Mercateo/rust-for-node-developers)

##### [rust for c developers / "I used to use pointers - now what?"](https://github.com/diwic/reffers-rs/blob/master/docs/Pointers.md)


##### [rust for clojurists](https://gist.github.com/oakes/4af1023b6c5162c6f8f0)

### Intro

- [Rust Docs](https://www.rust-lang.org/en-US/documentation.html)
- ["The Book (Second Edition)" aka "The Rust Programming Language"](https://doc.rust-lang.org/book/second-edition/index.html)
- [Self Contained Rust Examples](https://doc.rust-lang.org/rust-by-example/)
- [Community Maintained Git Repo of Rust Resources](https://github.com/ctjhoa/rust-learning)
- [Rust Performance Pitfalls](https://llogiq.github.io/2017/06/01/perf-pitfalls.html)


### Detailed

- [The Rust Reference](https://doc.rust-lang.org/stable/reference/)
- [Rust Grammar](https://doc.rust-lang.org/stable/grammar.html)
- [Standard Library API Reference](https://doc.rust-lang.org/std/)
- [Rust API Guidelines](https://rust-lang-nursery.github.io/api-guidelines/)
    - [Rust API Guidelines Quick Checklist](https://rust-lang-nursery.github.io/api-guidelines/checklist.html)
- [Advanced: How to write unsafe Rust code aka "The Rustonomicon"](https://doc.rust-lang.org/nomicon/)
- [Unstable Book](https://doc.rust-lang.org/nightly/unstable-book/)
- [Rust release notes](https://github.com/rust-lang/rust/blob/master/RELEASES.md)
- [Rust platform support](https://forge.rust-lang.org/platform-support.html)
- [Rust Compiler Error Index](https://doc.rust-lang.org/error-index.html)
- [Segfaults in Rust](https://jvns.ca/blog/2017/12/23/segfault-debugging/)
- [Profiling Rust Applications on Linux](https://llogiq.github.io/2015/07/15/profiling.html)
- [Writing an OS in rust](https://os.phil-opp.com/)
- [Pretty state machine patterns in rust](https://hoverbear.org/2016/10/12/rust-state-machine-pattern/)


