# Managing Registers for Vim Macro Templates


### Problem: macro templating

If you want to slightly modify a macro for special cases, you need to be able to manipulate its register easily.


### Vim Macro Review

In vim, macros can be used for repetitive tasks.

The typical use case is to record a macro and play it back when needed.

A macro is recorded into a register.

You can see your registers by typing `reg` in the ex prompt. It looks like this: `:reg`.


#### How to make a macro template

You could store a file where each line is a macro template. Then you can yank that line and paste it into the command buffer and modify it in `Example: step 1`.

For example, you might paste an existing macro with `"lp` or paste your paste buffer directly with `p`.


##### Methods for Copying Macros

On any empty line, you can paste an existing register, `j`, into another register, `l`: `"jp"ldd`

Or in `ex mode`, use the command: `:let @l=@j`


### Example

The example looks like this: `q:ij^["ldd:q`

This is a simple way to edit a register without using a file.

Instead we will use the command buffer as an anonymous buffer.

This example will create the macro that executes `j` which moves the cursor down 1 line.

You can replace j with any vim macro.

The `^[` key simply means the escape key.  You can also do this chord directly to escape, also written as `ctrl+[`.  

It can be typed as `^[` ,the two character combo in a macro or as the single character `` which is accessed with the `` character followed by the `` character.

You cannot use `ctrl+c` (also known as `^c` or ``) here because it will put you back into `ex mode` with your typed command in the ex buffer. We want to stay in the command buffer.


### Breakdown of Example

1. Access the command buffer: `q:` and enter insert mode with `i`
    - You may paste a macro template instead of directly entering insert mode
    - To paste directly from register `k`, type `"kp`
2. Make your modifications: `j` can be replaced by any line representing your macro.
3. Exit insert mode: ``
4. Move your text into the buffer: `"ldd`
5. Quit command mode: `:q`
6. Run your macro: `@l`


