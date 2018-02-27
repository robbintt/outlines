
### Python Reference Materials

Try to migrate the key component of these reference materials into this document.  Links will inevitably become unavailable and the document should preserve the information. Most information here will likely be from a derivative source anyways, so some long term effort could be made to resubstantiate each section with a primary reference in the Python reference, library, PEPs, source code, etc.

### Sections

#### Quick HTTP Server

- `python -m http.server`

#### Python Operator Precedence

[Original Source](http://www.ibiblio.org/g2swap/byteofpython/read/operator-precedence.html)


#### Helpful `and` and `or` Idioms

1. Set a default value with `or`

    ```python
    `def thing(foo, *, opt=None): opt = opt or {}`
    ```

2. Avoid a zero division error with `and` when adding if statements

    ```python
    b = 0
    a = (b and 100 / b)
    a
    ```

#### 'sqlite3' Context Manager

- [PyCon 2016 SQLite Class Video](https://youtu.be/D7wSMnapDp4?t=9m37s)
- [PyCon 2016 SQLite Class Code](https://github.com/kingsawyer/python_sqlite_talk/blob/master/stock_db.py)
