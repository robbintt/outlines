# A Plan to Learn Rust

I was planning on learning C but it's tough to get up to speed and people seem to have wildly varying practices. It would be better to learn low level things in a modern context with less baggage.


## The Plan

Go through the book (2nd edition) and check out the community maintained git repo.

Skip the examples for now because I've already run them once.

Learn about `rustup` and how to maintain your `rust` toolchain. Hopefully build an analogy to `python-virtualenv`.


## Tools

Tools for Rust.

### rustup

> rustup installs The Rust Programming Language from the official release channels, enabling you to easily switch between __stable, beta, and nightly compilers__ and __keep them updated__. It makes cross-compiling simpler with binary builds of the standard library for common platforms. And it runs on all platforms Rust supports, including Windows. (emphasis mine)

> rustup is a toolchain multiplexer. It installs and manages many Rust toolchains and presents them all through a single set of tools installed to ~/.cargo/bin. The rustc and cargo installed to ~/.cargo/bin are proxies that delegate to the real toolchain. rustup then provides mechanisms to easily change the active toolchain by reconfiguring the behavior of the proxies.


### GDB

- [GDB support Rust](https://sourceware.org/gdb/onlinedocs/gdb/Rust.html)
    - Lizzie says no one uses it


## Resources

Resources from main rust site.


### Articles

- ["Rust for Python Developers" by Armin Ronacher](http://lucumr.pocoo.org/2015/5/27/rust-for-pythonistas/)
- [Three things Armin wishes he learned earlier](http://lucumr.pocoo.org/2018/3/31/you-cant-rust-that/)

### Intro

- [Rust Docs](https://www.rust-lang.org/en-US/documentation.html)
- ["The Book (Second Edition)" aka "The Rust Programming Language"](https://doc.rust-lang.org/book/second-edition/index.html)
- [Self Contained Rust Examples](https://doc.rust-lang.org/rust-by-example/)
- [Community Maintained Git Repo of Rust Resources](https://github.com/ctjhoa/rust-learning)


### Detailed

- [The Rust Reference](https://doc.rust-lang.org/stable/reference/)
- [Rust Grammar](https://doc.rust-lang.org/stable/grammar.html)
- [Standard Library API Reference](https://doc.rust-lang.org/std/)
- [Advanced: How to write unsafe Rust code aka "The Rustonomicon"](https://doc.rust-lang.org/nomicon/)
- [Unstable Book](https://doc.rust-lang.org/nightly/unstable-book/)


