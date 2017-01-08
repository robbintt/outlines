## info pages

info pages are like man pages. They apparently have hypertext before web type hyperlinks, and are emacs style documentation.

Henner says info pages are good references for C.

I should probably read all of `coreutils.info` and `info info`


### FUTURE

Take notes on `info info` and include below.


### Running `info`

Info can be used a few different ways

- `info` to get the directory root node for info files.
- `info printf` to get info on the node "printf".
- `info --apropos="printf" to search all nodes for "printf"


### Navigation

- `space`: page down
    - Also carries you to the next node regardless of level
- `backspace`: page up
    - Also carries you to the previous node regardless of level
- `[`: go to the next node in the current document
- `]`: go to the previous node in the current document
- `n`: go to the next node at the same level in the current document
- `p`: go to the previous node at the same level in the current document
- `u`: go the parent node
- `l`: go to the last node
- follow a link: move cursor over a link, a word preceded by an asterisk, press enter
- `q`: quit
- `m`: go to the menu item you write if it exists

- `info --vi-keys printf`: use vi type keybindings
    - FUTURE: map out exactly what varies between standard nav and vi mode


### Notes from `info info`



### Notes from `man info`

Note on `man info` are integrated elsewhere in this outline.

`info coreutils printf`: get printf in coreutils (if there are more than one printf files)

I read that there are some flags to store and restore keystrokes pressed in an info file.


### References

- [info (Unix) on Wikipedia](https://en.wikipedia.org/wiki/Info_(Unix))
- `man info`
- `info info`
