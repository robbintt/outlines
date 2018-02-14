# Managing Registers for Vim Macro Templates


### Problem: macro templating

If you want to slightly modify a macro for special cases, you need to be able to manipulate its register easily.


### Vim Macro Review

In vim, macros can be used for repetitive tasks.

The typical use case is to record a macro and play it back when needed.

A macro is recorded into a register.

You can see your registers by typing `reg` in the ex prompt. It looks like this: `:reg`.


### How to use Macro Templates

Macro Templates are not special features, they are simply `lines of text` you have stored to put back into a `register` for use as a macro.

You could store a file where some lines are macro templates and others have comments.

For example, you might paste an existing register, `l`, with `"lp`.


##### Methods for Copying Macros

A macro doesn't really exist in vim, it's really a register, e.g. register `l` that is played back with the macro key, `@`, e.g. `@l`.

1. On any empty line, you can paste an existing register, `j`, into another register, `l`: `"jp"ldd`
2. In `ex mode`, use the command: `:let @l=@j`


### Example

We will use the `command buffer` as an anonymous buffer to avoid needing to modify a file to modify the register.

The example looks like this: `q:ij^["ldd:q`


This example will fill the register `l` that executes `j` which moves the cursor down 1 line.

**You should replace `j` with any vim macro you wish.**


### Breakdown of Example

1. Access the command buffer: `q:` and enter insert mode with `i`
    - You may paste a macro template instead of directly entering insert mode
    - To paste directly from register `k`, type `"kp`
2. Make your modifications: `j` can be replaced by any line representing your macro.
3. Exit insert mode: ``
4. Move your text into the buffer: `"ldd`
5. Quit command mode: `:q`
6. Run your macro: `@l`


#### Detour: The Escape Key

In a browser you probably cannot see the escape character, typically rendered as `^[` but as one glyph, ``, not two.

The `^[` key simply means the escape key.  You can also do this chord directly to escape, also written as `ctrl+[`.  

It can be typed as `^[` ,the two character combo in a macro or as the single character `` which is accessed with the `` character followed by the `` character.

You cannot use `ctrl+c` (also known as `^c` or ``) here because it will put you back into `ex mode` with your typed command in the ex buffer. We want to stay in the command buffer.


