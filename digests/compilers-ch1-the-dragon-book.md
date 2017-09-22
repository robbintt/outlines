# Compilers ~ The Dragon Book - 1986


## Chapter 1 - Introduction to Compiling

On the general subject of compiling.

### Contents

- `components` of a compiler 
- `environment` in which a compiler does its job
- `tools` to make it easier to build compilers

### 1.1 Compilers

compiler - a program that reads a program written in the `source language` and translates it into an equivalent `target program` in the `target language`.  The compiler reports errors in the `source program` as `error messages`.

- "basic tasks" all compilers perform "are the same"
- Thousands of source languages
- Target languages include
    - Another programming language
    - Machine language of any computer (microprocessor to supercomputer)
- Some compiler classifications - based on structure or function
    - single-pass
    - multi-pass
    - load-and-go
    - debugging
    - optimizing
    - etc.
- advances in compilers:
    - implementation languages
    - programming environments
    - software tools

#### The `Analysis-Synthesis Model` of Compilation

The 2 parts of compilation are `analysis` and `synthesis`.

1. `Analysis` - Break the `source program` into pieces and create an `intermediate representation` of the `source program`.
1. `Synthesis` - Construct the `target program` from the `intermediate representation` **requires the most specialized techniques*


##### Analysis
- Operations of source program are determined & recorded in a tree, (hierarchical structure).
- Often a `syntax tree`
    - `node` == `operation`
    - `children of node` == `arguments of operation`
    - in the text diagram, operations can be arguments: 
        - `position := initial + rate * 60`
- Many `software tools` that manipulate source programs first perform some kind of `analysis`
    1. `Structure Editors` - text editor + autocomplete + linter + static analysis + etc. 
        - real-time partial analysis
    1. `Pretty Printers` - structure viewer for humans
    1. `Static Checkers` - attempt to discover potential bugs without running the program.  Similar to `optimizing compilers`. 
        - code that cannot be executed in the course of the program 
        - variable used before defined
        - catch logical errors (type checking / use real variable as pointer)
    1. `Interpreters` - Instead of producing `target program`, perform the operations implied by `source program`

##### Compilers aren't just for machine code

The `analysis` portion of compiling shows up in these examples:

1. `Text formatters` - Format text for output in a textual format
1. `Silicon compilers` - Input is a conventional programming `source language`.  Variables represent signals or signal groups in switching circuits. Outputs a `circuit design` in an appropriate `target language`
1. `Query interpreters` - translates a predicate containing relational and boolean operators into commands to search a database for records satisfying the predicate

#### The Context of a Compiler

Other programs may be needed to create the executable target program.

- A `preprocessor` might: 
    - collect parts of the `source program` stored in separate files 
    - expand `macros` into `source language` statements.

See `fig 1.3` page 4.

- A `target program` may require further processing to run.
    - `assembler` - translate assembly to machine code
    - `linker` - link to library routines


### 1.2 Analysis of the `source program`

Introducing `analysis` and illustrate its use in some `text-formatting languages`. Also see chapters 2-4, 6.

##### Three Phases of Analysis

1. `Linear Analysis`
    - AKA: `lexical analysis` or `scanning`
    - read stream of `source program` left-to-right and group into `tokens`, streams of characters, with collective meaning 
1. `Hierarchical Analysis`
    - AKA: `parsing` or `syntax analysis`
    - hierarchically group characters/tokens into meaningful nested collections
1. `Semantic Analysis`
    - check that components of a program fit together meaningfully

#### Lexical Analysis

Linear analysis is called `lexical analysis` or `scanning`.  See example page 5.

Create `tokens` from the `source program` stream. Discard separators, e.g. whitespace.

#### Syntax Analysis

Hierarchical Analsysis is called `parsing` or `syntax analysis`.

Group the `tokens` into `grammatical phrases` for the compiler to synthesize output.  Usually the `grammatical phrases` are represented by a `parse tree` or a `syntax tree`.

1. `parse tree` - `statements`, `expressions`, and `identifers` are all nodes. A precise definition is not given, see fig. 1.4, page 6.
1. `syntax tree` - Compressed representation of a parse tree. Operators appear as interior nodes and operands are the children of that operator's node. See `Section 5.2`.

There is a good example here, page 6.

`expressions`, `recursive rules`, `(nonrecursive) basis rules`, and `definition rules`, and `statements` are described in the example but not introduced as formal terms.

> The division between lexical and syntactic analysis is somewhat arbitrary.
> We usually choose a division that simplifies the overall task of analysis.

##### Factors for division between `lexical` and `syntactic` analysis:

1. Is the source language construct recursive or not?
    - `Lexical constructs` - **do not require recursion**.
        - `identifiers` - strings of `letters+digits` beginning with a letter
        - recursion not necessary to recognize `identifiers`, typically scan until `non-(letter+number)` and group back to beginning
        - the grouped characters are recorded in a `symbol table` and removed from the input (so the pointer is back at the beginning)
        - the next token is then processed.
    - `Syntactic constructs` often **require recursion**.
        - linear scan cannot analyze expressions or statements
        - cannot match `parentheses` in expressions
        - cannot match `begin` and `end` in statements
        - unless there is a `hierarchical` or nesting `structure` ON the input
2. `Context-free grammars` - formalization of recursive rule that can be used to guide `syntactic analysis`
    - See chapter 2 for introduction, chapter 4 for extensive treatment.

##### Syntax-directed translation

The `compiler` uses the `hierarchical structure` on the `input` to **help generate** the `output`.

See: Chapters 2, 5.


#### Semantic Analysis

- check `source program` for `semantic errors`
- gather `type information` for subsequent `code-generation phase`
- use `hierarchical structure` determined by `syntax-analysis phase` to identify `operators` and `operands` of `expressions` and `statements`


1. `type checking`: `compiler` checks that each `operator` has permitted `operands` based on `source language` specification. Must also check for operator coercions.
    - Part of `semantic analysis`, see ch. 6.
    - example: binary arithmetic operator applied to integer & real, converts integer to real, see example 1.1 and fig. 1.5 inttoreal


#### Analysis in Text Formatters

TEX uses hierarchical arrangement in boxes as part of the `syntax analysis` to describe the relative position of groups of vertical and horizontal characters.  See p.8-9 for fig 1.6-1.7.


### 1.3 The Phases of a Compiler



#### Symbol-Table Management




#### Error Detection and Reporting



#### The Analysis Phase



#### Intermediate Code Generation



#### Code Optimization



#### Code Generation




### 1.4 Cousins of the Compiler


### 1.5 The Grouping of Phases


### 1.6 Compiler-Construction Tools


Chapter eleven discusses `software tools` for implementing a compiler.

There are `specialized tools` for implementing various phases of a compiler

These tools are called variously: 

- `compiler-compilers`
- `compiler-generators`
- `translator-writing systems`

`Specialized tools` are typically oriented around a model of languages and are suitable for languages following that model.

Tools exist for automatic design of specific `compiler components`, they use `specialized languages` for specifying and implementing the component.  The most successful hide details of generation algorithm and make components that are easily integrated into the remainder of the compiler.

##### A list of compiler construction tools

1. `Parser generators`: produce `syntax analyzers` normally from in put based on `context-free grammar`. Syntax analysis used to be very time consuming but now is "one of the easiest phases to implement".  Often `parser generators` use `parsing algorithms` too complex to do by hand.
1. `Scanner generators`: automatically generate `lexical analyzers`, normally from a specification based on `regular expressions`.   The `lexical analyzer` is effectively a `finite automaton`. See `chapter 3`, implementations in `section 3.5, section 3.8`.
1. `Syntax-directed translation engines`: produce collections of routines that walk the parse tree, generating `intermediate code`. One or more translations are associated with each node of the parse tree, each translation defined in terms of its neighbor nodes in the tree. See chapter 5.
1. `Automatic code generators`: take a collection of rules defining `intermediate language`->`target language` and replace the intermediate rules with templates that represent sequences of machine instructions. Something about tiling intermediate code without a combinatorial explosion in compiler running time.  See chapter 9.
1. `Data-flow engines`: `data flow analysis` is used in optimization. How are values transmitted from one part of a program to each other part? Especially as the user defines relationships between intermediate code statements and the information being gathered. See Section 10.11.

### Bibliographic Notes

Lots of parallel discovery, hard to attribute credit. Page 23-24 have references.