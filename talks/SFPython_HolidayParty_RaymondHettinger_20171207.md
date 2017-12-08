# Raymond Hettinger Holiday Party Talk

Raymond says: I will tweet out a link to this presentation later. It is in sphinx.

- Mission: Train thousands of Python Developers
- Mutable Minds, Inc.
- raymond.hettinger@gmail.com
- Training Videos: Free to users of Safari Online: "Modern Python: Big Ideas, Little Code"
    - Raymond says about a $100 on-ramp to using Safari Online
- @raymondh on twitter

I use sphinx to prepare my talks / slide decks. Never intend to go back to Powerpoint.

I am a manufacturer of Python Programmers. I take someone good at something and make them good at something plus Python programming.


## Python 3.7

- How to hold these 3 numbers:   33, 1.00, 0.5 (HSL Colors)


## Class Generators: dataclasses and namedtuples



### Problems to be Solved

I want to pass around a bunch of instances of colors: HSL system.

Dark Orange: 33 degrees on the color wheel at 100% saturation and 50% lightness.

```
from bunch import Bunch
from types import SimpleNamespace
? import record # for recordtype
? import dataclass

# tuple
dark_orange = (33, 1.00, 0.5)
print(dark_orange)

# dict
dark_orange = {'hue': 33, 'saturation': 1.0, 'lightness': 0.5}
print(dark_orange)

# simple class
class Color:
    ''' there are 6 basic dunder methods, __init__, __hash__, something else, __lt__ etc, 
    '''
    def __init__(self, hue, saturation, lightness=0.5):
        self.hue = hue
        self.saturation = saturation
        self.lightness = lightness

dark_orange = Color(33, 1.00, 0.5)
print(dark_orange)


# bunch recipe ########### Bunch can be written in three lines (not in std library)
dark_orange = Bunch(hue=33, saturation=1.00, lightness=0.5)
print(dark_orange)

# simple namespace ######### Bunch, but in the standard library, written in c
# good, because it's in the standard library... ha but it's just bunch
# this way is pretty good, repr but can't compare it, can't sort, can't hash...
# takes a bunch of space... has an object with a reference to a dictionary, 300 bytes
dark_orange = SimpleNamespace(hue=33, saturation=1.00, lightness=0.5)


# named tuples ######### i stole it, i'm an aggregator... i found it reinvented dozens of times
# i brought them all together in a massive chart, took the best ideas from each, aggregated
# published the recipe, got lots of people to use it, took it to python dev, we put it in
# internally same name tuple as before, but now written in a class format... before what?
class Color(NamedTuple):
    ''' 
    benefits from before
    one from each line
    see the datatype, use default
    '''
    hue: int
    saturation: floor
    lightness: float = 0.5

# calling the NamedTuple... 72 bytes, 4 times smaller than SimpleNamespace
# make one namedtuple then you can make another one based on it, just change an attribute and clone
# named tuples are hashable so they are useable as dictionary keys
# immutable! - whaa - you just have to use the replace() method to make another... too hard
dark_orange = Color(hue=33, saturation=1.00)
print(dark_orange)

''' Python 2.7 so it's commented
# record by george sakkis ####
# python 2.7 recipe and not changed for Python3
# we had mutable nametuples for a very long time, 8 years, no typing, needs typing
# but it didn't have a cool name#127.0.0.1 dev.hackersinresidence.c so no one knew!
Color = record.recordtype('Color', ['hue', 'saturation', 'lightness'])
# mutability is fun!
# 64 bytes, smaller than a tuple... tuples store the length, instances don't unless you add the field
# so this can't tell you its length... but it's smaller
dark_orange = Color(hue=, saturation=1.00, lightness=0.5)
'''

# dataclass ##################
# half the people see it as a data container, half the people see it as a class
# rorscach test
# you can start using it in Python3.6 with raymonds code, or wait for python3.7
# in python2, you can import recordtype as dataclass - ha!
# biggest way of all at 296 bytes, bigger than a dict
@dataclass
class Color:
    ''' it writes classes for you and holds data
    '''
    hue: int
    saturation: float
    lightness: float = 0.5

dark_orange = Color(hue=33, saturation=1.00)
print(dark_orange)

# dataclass with slots but no defaults ########
@dataclass
class Color:
    ''' 64 bytes but you can't have any default values, or use george's recipe
    '''
    slots = ['hue', 'saturation', 'lightness']
    hue: int
    saturation: float
    lightness: float

dark_orange = Color(hue=33, saturation=1.00, lightness=0.5)
print(dark_orange)
  
# you learned the history of how to store 3 numbers
# this gives some output
```


# Details about each data container option

Have to see the notes for this... it's really fast


## Bunch and SimpleNamespace

### Recipe

```
class Bunch(object):
    def __init__(self, **kwds):
        self.__dict__.update(kwds)
```

### Optimization

```
class Bunch(object):
    ''' much faster, replace the dict with kwds
    dict is guaranteed to be ordered
    ''' 
    def __init__(self, **kwds):
        self.__dict__ = kwds
```

### C version built into Python

```
from types import SimpleNamespace
```


## Named Tuples - same size as regular tuple

- Replaces tons of stuff with NamedTuples when doing code review
- raymond loves fstrings - brought by eric smith
- who did dataclass - eric smith
- are you going to remember his name?

You can let the code generator build it then modify it yourself... how? what?
I think it's written in python so you need to paste it in or something... no idea


## Data Classes - PEP 557 has landed

- Validates that NamedTuple was doing the right thing but we need mutable. And a cool name.
- Immutable if you want (possible to freeze the data)
- PEP says - mutable namedtuples with defaults
    - main design goal is to support static type checkers
    - highly opinionated about typing, no way to use it without typing
    - static typing was optional, not here... you can put a type of `None` or `any` and it will be ignored.
    - have to explicitly opt out of typing with `None` or `any`
    - raymond is working on a workaround
- boilerplate for class, attribute based dataholder
- is it a code generator? is it a data holder? two different ways of looking at it
- generates code for you, generates class docstring, __init__, __repr__, __eq__ with strong typechecking, rich comparisons, hashing, read-only enforced by __setattr__, __delattr__

```from dataclasses import make_dataclass```
- this thing is huge unless there are slots... but with slots you lose defaults
- the language has a built in constraint against slots and defaults at the same time

Do you always know if something is going to be integer float? No. 12.5 timezones off in india!

When you import types it actually executes code... so there is debate about whether they will stringify types in `make_dataclass`

- if you read python-dev you will get all of the drama

- emulate a namedtuple (see slides) with `from operator import itemgetter` and `dataclasses`


# Summary

I have been studying dataclasses since the first draft of PEP 557.

I really like the new dataclasses!

If you need mutable named tuples today, try George Sakkis's Record class or use the attached dataclass code that runs fine on Python3.6 but not prior. (code in raymond's slides)

See the 4 tuple code generator table: Namedtuple, Record, Dataclasses, Dataclasses w/ slots

## Gains and losses

(see the slides)


## Some Nice Improvements

(see the slides)


## Some things that aren't as nice

- higher complexity and learning curve, 700 ish lines of code, couple hundred lines of tests, lots of specs.
- dataclasses is its own miniature ORM for python stuff, declare, fields() function, hashable, etc.

(see the slides)


# Inside the sphinx slides this talk is from, you can cut and paste raymond's code and use it now.
