
### Python Reference Materials

Try to migrate the key component of these reference materials into this document.  Links will inevitably become unavailable and the document should preserve the information. Most information here will likely be from a derivative source anyways, so some long term effort could be made to resubstantiate each section with a primary reference in the Python reference, library, PEPs, source code, etc.

### Sections


#### Python Operator Precedence

[Original Source](http://www.ibiblio.org/g2swap/byteofpython/read/operator-precedence.html)


#### Using `and` and `or` to set default arguments

1. Set a default value with `or`
    - `or`: `def thing(foo, *, opt=None): opt = opt or {}`

2. Avoid a zero division error with `and` when adding if statements
    - 
        ```python
        b = 0
        a = (b and 100 / b)
        a
        ```
