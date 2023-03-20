## import madness

This talk only works in Python 3!!

This title `import madness` is executable. If we import it we get an `ImportError` without that module existing.

What is a module? A python file.

What else is a module? An object loaded that represents a **python module** (as in: Python file)

Python has a standard `module` type. `__import__` will initialize a module by executing all the source of the module file in main.




### Can you implement a mergesort algorithm using the Python `import` keyword?

Merge

Yes! Should you? Obviously, no.

> Speaker discusses mergesort.

>When you import a module in Python, Python executes the entire source of that module.

`madness` is a wrapper module which will import mergesort.  It will then create new modules for the left side and right side and continue.

Solve most `import` errors with `sys.path`.

### DANGER!! WARNING!!

`import` is dangerous!! Python imports the containing module to find any function you import from that module.  Including uploading all your ssh keys to pastebin, encrypting your drive, and deleting the line of code that did that.


### Some of the source

bit.ly/2s8YmzL

```
current_module = sys.modules(__name__)
module_source = inspect.getsource(current_module)
```

```
# buckle up!
from merge_sort import sorted_sublist as sorted_list
```


