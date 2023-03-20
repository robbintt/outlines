

### Python Generators from Principles

Outline notes come from [here](https://wiki.python.org/moin/Generators). The code has been slightly modified to sum to the first n inclusive.


##### Future:
1. Include information about converting list comprehensions into generator comprehensions.


#### A simple use case for a generator, described without any generators

``` python

def firstn(n):
    """
    The code works. 
    Problem: the function sends the entire list at once (using memory).
    Memory constrained applications need a different way.
    """
    num = 0
    nums = []

    while num <= n:
        nums.append(num)
        num += 1

    return nums

for i in range(10):
    print(i, sum(firstn(i)))

```

#### Constructing a generator from scratch

``` python

class firstn(object):
    """
    The generator pattern (an iterable)

    From: https://wiki.python.org/moin/Generators

    Notes: This pattern is compacted into the Python `generator function` and
    can be accessed by using the `yield` keyword in a function.
    """

    def __init__(self, n):
        self.n = n
        self.num = 0
        self.nums = []

    def __iter__(self):
        return self

    # Python 3 compatibility
    def __next__(self):
        return self.next()


    def next(self):
        if self.num <= self.n:
            cur = self.num
            self.num += 1
            return cur
        else:
            raise StopIteration()

for i in range(10):
    print(i, sum(firstn(i)))

```

####  Using the generator pattern and `yield` keyword

``` python

def firstn(n):
    """ 
    The same code as a generator.
    From: https://wiki.python.org/moin/Generators 
    """
    num = 0
    while num <= n:
        yield num
        num += 1

for i in range(10):
    print(i, sum(firstn(i)))

```

#### Problem: How do we get a list out of a generator?

``` python

# Python 2 `xrange` generator example, Python 3 would use `range` in the `for` loop.
items = []
for i in xrange(10):
    # generate the list
    items.append(i)

print(items)

```

#### Generator Comprehensions

``` python

```

#### Generators can be composed from other generators

Open question: why not use Python 2 `xrange` or Python 3 `range` in a generator composition?

``` python

def irange(start, stop=None, step=1):
    """ Implementation of irange from Python wiki (https://wiki.python.org/moin/RangeGenerator)
    """
    if step == 0:
        raise ValueError("irange() step argument must not be zero")

    if stop is None:
        stop = start
        start = 0

    continue_cmp = (step < 0) * 2 - i

    while cmp(start, stop) == continue_cmp:
        yield start
        start += step

square = (i*i for i in irange(1000000))

total = 0

for i in square:
    total += i

```

