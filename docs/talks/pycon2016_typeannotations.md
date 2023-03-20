### Why use static typing? (Dropbox talk)

Date: 2016-05-29
Talk: PyCon 2016
Who: Guido van Rossum et al, Dropbox Inc.
Spreadsheet URL: 

At dropbox, 40% of time was used on reading/understanding code (2015 survey)

Static typing helps understanding of code.


#### Problem: 

Finding a type of an input can be impossible. Worst case: recursively hunt backwards in the codebase until you enumerate everything constructing your input. Massive search tree required.

More complex problem: type can even vary, maybe a method is overloaded (eek). Computer science says this is undecidable.


#### Another problem:

Over time, expectations for the code change and comments that were true become lies.

Now we have to go back to the original problem.

"Explicit is better than implicit." -> "Checked is better than unchecked."

Lets make our types explicit have a computer check our types.


#### New Strategy: Make types explicit and checked.

1. Write types at def and where not obvious.
2. Run `mypy` to check types, routinely like your tests
3. Read code, learning types i easy.


#### A definition for "static typing"

Static Typing - The expectation the author had for the piece of code when they were writing it.


##### Using Type Hints in Python 2 (Static Typing)

Simply use a comment.

```
def function(a, b):
    # a: int, b: int => int
```

#### Using Type Hints in Python 3 (Static Typing)

Use mypy as a checker for type hints in python 3.


#### History of static typing (Guido)

Guido has been considering this over a decade. The technology really has come around in the last six months.

##### 2004-2005 - Artima blog posts:
1. https://www.artima.com/weblogs/viewpost.jsp?thread=85551
2. 


##### 2006 - PEP 3107 Compromise, 'function annotations'
1. https://www.python.org/dev/peps/pep-3107/
2. Type annotations do nothing but are introspectable.


##### 2012 - Jukka also started working with this, stsarted `mypy` as an "experimental python variant" - statically typed python.
Used angular brackets because other languages do it in this way.

Guido convinced him to use pep3107 and square brackets so mypy is completely compatible with Python


##### 2014 - Bob Ippolito - EuroPython Talk (see youtube) - "What Can Python Learn from Haskell"

His 3rd idea was to use mypy b/c static typing.

https://www.youtube.com/watch?v=pJOmlFf5Je4

Discussion about PEP484 started right after PyCon 2014.
https://www.python.org/dev/peps/pep-0484/

PyCharm and Google's pytype project started adopting this standard.


##### Everything is optional and gradual.

You can have annotations in one place and none elsewhere.

Python ignores annotations.  Except when you set __annotations__


