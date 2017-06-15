## Unit Testing with Mock

This talk is about unit testing.

Speaker: Brian Weber, SRE at Twitter

Lets execute tests in your code safely

Tests execute your code.

For example, a command line function that deletes hard drives...

### How do we do it? `mock`

### What is a `mock`?  

unitteset.mock is a library for Testing in Python. It allows you to replace parts of your system under test with mock objects... (is this text from the unittest documentation?)

### Why use `mock`?  

1. Stop the state-changing parts so you can actually run tests.  
2. Write better code
3. `_____` (missed it!)

### Patch decorator


### Mocks are plastic

Everything the mock does returns another mock

- `spec` - flexible but not safe
- `spec_set` - safer, somewhat immutable
- `autospec` - match function signatures of class instances


### Mocks have a bunch of introspection features

- called, call_count, call_args, call_args list, method_calls, ... (more)
- assert_called, assert_called_once, ... (more)


### Example: API Requests



### Two options

#### Patch locally defined function

Replace portion of function being tested - side-effect.

#### Patch external library


Which would you pick?  USE BOTH! It's really easy to write, don't worry about it and write both.


#### Another thing: Mock "Factory"

Kind of a factory but not really.


#### DO NOT mock

- The filesystem - too many surfaces and edges. Lots of debate but don't do it
  - use the `temp dir` module or whatever it is called. Very simple
- Acceptance and Integration tests


#### Additional info

- Write mocks as PyTest fixtures. PyTest and mock go hand-in-hand.
- How do you mock a for loop that hits an API a certain number of times?
    - Mock the parent library and setup some sort of a "factory" module
    - One instantiation setup that mocks all the behavior
    - For loop means some expected behavior inside for loop and some expected behavior outside for loop.
- Usually you will patch directly in the namespace you are testing.
    - Direct accuracy over what you are replacing.


