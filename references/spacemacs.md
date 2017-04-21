# Spacemacs Reference Document

A general reference for getting into spacemacs from vim.  Mostly derivative of other guides.


## Table of Contents

This does not have all sections listed, just main sections and popular reference areas.

1. [Reference](#Reference)
    1. [Notes](#notes-from-references)
        1. [Spacemacs State Color Codes](#spacemacs-state-color-codes)
2. [Spacemacs Fixes](#spacemacs-fixes)
3. [Greg's elisp notes](#gregs-elisp-notes)
4. [Why I switched](#why-i-switched-to-spacemacs)

## Reference

### Useful Sequences

1. See all active `minor-modes` and `major mode`: `C-h m`
    1. another get major-mode: `C-h v major-mode`
    2. another get minor-mode: `C-h v minor-mode-list`
    3. [spacemacs minor-mode stuff](https://github.com/syl20bnr/spacemacs/blob/master/doc/DOCUMENTATION.org#minor-modes)
2. Reload stuff/settings: `SPC f e R`
3. Load up non-GUI mode: `$ emacs -nw`
4. Insert any character: `C-q `
5. Increment by q (q=1 by default): `q SPC n -`
    - has some sort of minor mode where you can keep pressing stuff, try it
6. Clear search highlighting: `SPC s c`
7. Navigate buffers: `SPC b b`
    - Check out the `Messages` buffer
    - kill buffer: `SPC b d`
    - next or prev buffer: `SPC b n` or `SPC b p`
8. Jump between matched tags: `%`
9. Exit insert mode (evil-escape): `fd`
    - note that this should take you to `evil normal mode` from anywhere
    - this may work identically to `C-g`
10. Find a file and open in a new buffer: `SPC f f`
11. "help describe": `SPC h d`
    - "help describe function" `SPC h d f`
    - "help describe key" `SPC h d k`
12. [guide-key](https://github.com/kai2nenobu/guide-key), a menu of stuff: `SPC`
13. Insert lorem ipsum: `SPC i l l`
    - (lorem-ipsum) has several nice insert options `SPC i l`
14. Note that the vim `.` repeater works on `SPC`-leader macros..
    - try `SPC i l l . . . . .`
15. Using `evil-nerd-commenter`
    - comment or uncomment a block of lines `SPC c l`
    - toggle comment on each line in a block of lines `SPC c ;`
        - can be used to simultaneously uncomment and comment neighboring lines
16. `SPC m` is aliased to `,` and accesses the current `major-mode` menu


### Interesting Sequences
1. Incremental Search: `C-s stuff`
    - Note: `/ style` search is already incremental in spacemacs.
2. Learn emacs lisp: `SPC h i elisp RET`


### Future

1. Mess with `iedit` and `iedit-insert` states
2. Try out the other `SPC s` search options
3. Test out spacemacs regex `SPC x` which uses `pcre2el` package
    - [further reference](https://github.com/syl20bnr/spacemacs/blob/master/doc/DOCUMENTATION.org#regular-expressions)
4. [editing lisp code & lisp keybindings](https://github.com/syl20bnr/spacemacs/blob/master/doc/DOCUMENTATION.org#editing-lisp-code)
5. [managing projects](https://github.com/syl20bnr/spacemacs/blob/master/doc/DOCUMENTATION.org#managing-projects)
6. [compiling code](https://github.com/syl20bnr/spacemacs/blob/master/doc/DOCUMENTATION.org#compiling)


### External References
1. [Spacemacs documentation](https://github.com/syl20bnr/spacemacs/blob/master/doc/DOCUMENTATION.org)
2. [Migrating from Vim](https://github.com/syl20bnr/spacemacs/blob/master/doc/VIMUSERS.org)
    1. [Remapping keys](https://github.com/syl20bnr/spacemacs/blob/master/doc/VIMUSERS.org#keybindings)
3. [guide-key](https://github.com/kai2nenobu/guide-key)
4. [learn elisp in 15 minutes](https://learnxinyminutes.com/docs/elisp/)
5. [GNU emacs manual](https://www.gnu.org/software/emacs/manual/emacs.html)
6. [Configuration "Tutorial" Orientation for contributing layers](http://thume.ca/howto/2015/03/07/configuring-spacemacs-a-tutorial/)



### Notes (From References)

Each note should have a `####` header and be included in the TOC.


#### What is `setq`?

Set Quoted. `(set (quote scroll-margin) 5)` is equivalent to `(setq scroll-margin 5)`.

#### Spacemacs State Color Codes

There are [10 states](https://github.com/syl20bnr/spacemacs/blob/master/doc/DOCUMENTATION.org#states).

The state table is from the [Spacemacs documentation](https://raw.githubusercontent.com/syl20bnr/spacemacs/master/doc/DOCUMENTATION.org).

| State        | Default Color | Description                                                                                                |
|--------------|---------------|------------------------------------------------------------------------------------------------------------|
| normal       | orange        | like the =normal mode of Vim=, used to execute and combine commands                                        |
| insert       | green         | like the =insert mode of Vim=, used to actually insert text                                                |
| visual       | gray          | like the =visual mode of Vim=, used to make text selection                                                 |
| motion       | purple        | exclusive to =Evil=, used to navigate read only buffers                                                    |
| emacs        | blue          | exclusive to =Evil=, using this state is like using a regular Emacs without Vim                            |
| replace      | chocolate     | exclusive to =Evil=, overwrites the character under point instead of inserting a new one                   |
| hybrid       | blue          | exclusive to Spacemacs, this is like the insert state except that all the emacs key bindings are available |
| evilified    | light brown   | exclusive to Spacemacs, this is an =emacs state= modified to bring Vim navigation, selection and search.   |
| lisp         | pink          | exclusive to Spacemacs, used to navigate Lisp code and modify it (more [[#editing-lisp-code][info]])                               |
| iedit        | red           | exclusive to Spacemacs, used to navigate between multiple regions of text using =iedit= (more [[#replacing-text-with-iedit][info]])        |
| iedit-insert | red           | exclusive to Spacemacs, used to replace multiple regions of text using =iedit= (more [[#replacing-text-with-iedit][info]])                 |



# Spacemacs Fixes

Things I think need fixed.


## Identified as `needs fixed for spacemacs`

6. Make default colors the same as default terminal colors...
  - not sure how to let these pass through, spacemacs has magic colors
9. Consider moving my hotkeys to a helm menu or something, with a space leader instead of C-<key> pattern. Also includes vim functions.
10. Rewrite vim functions for spacemacs
11. Consider alias for bash for spacemacs nongui as default `emacs -nw`
  - Also, consider installing the emacs-plus package from homebrew cask on mac
  - The emacs-plus package is apparently the recommended package by spacemacs, no idea why
12. Store undo history between sessions for all edited files.
  - manage branching undo history better? may just need training...
14. C-c should exit insert mode
15. Fix ridiculous html indentation
16. Disable the mouse... try the (disable-mouse) package?


## Needs Deeper Research

2. tabs->spaces
  - looks like highlight and <|> indent by 4 spaces in html extension files... not sure how it varies by file extension
  - we want this to be 2 spaces by default and 4 spaces in the .py file extension
  - indentation with the tab also does not always work, it seems to try to force a style from somewhere, tab does not always have an effect

  - html specific
    - tab seems to add spaces when it allows input... this should not follow complex rules, tab should just put 2 spaces in regardless
    - in html when exiting insert mode, it seems to do some postprocessing on my editing, visual mode gets weird
    - things in html mode are generally not working, especially with regards to <tab> <esc> <dj> and similar


13. Esc (1/2 second pause or less) followed by a key is a meta-key leader... need it to be dead key from now on
  - this is related: https://github.com/syl20bnr/spacemacs/issues/2756
  - this seems to have abated, i think i toggled a mode
  - i do not know why it would have abated but i did restart my computer
  - still reloading emacs settings should be enough, mysterious

7. How do I drill down to my packages? How do I learn about my evil mode configuration and contribute to the evil mode emacs plugin?
  - i have been reading the elisp in the .spacemacs.d layers
  
8. How do I manage undo branches?

## Done

1. line numbers on startup, line number toggle?
3. note taken - How do i search for tabs, e.g. \t
4. scroll-margin set to 5
8. C-l should redraw the screen - redraw does not clear search highlighting in emacs...
  - Clear a search with `SPC s c`
5. Turn off auto add closing quotes, braces, brackets, tildes, etc.
  - in init.el: put smartparens in dotspacemacs-excluded-packages


## Optional

1. redraw screen with some key combo? - https://www.gnu.org/software/emacs/manual/html_node/elisp/Refresh-Screen.html
  - May already be in spacemacs, check around


----------------------------------------

# Greg's elisp notes

I'm starting by reading An Introduction to Programming in Emacs Lisp.

To get to this, open emacs with no arguments, hit ctrl-h i <ret>.

C-h is for help.
i is for the info reader, which lets you browse manuals.

Then you're presented with a long menu.

Hit m for menu, then type Emacs Lisp Intro into the mini buffer. Then
hit enter.

That gets you to the elisp intro.

Lisp stands for LISt Processing.

A list:

    '(rose
      violet
      daisy
      buttercup)

Awesome and beautiful quote from the book:
"The elements of this list are the names of the four different flowers,
separated from each other by whitespace and surrounded by parentheses,
like flowers in a field with a stone wall around them."

Text between double quotation marks is also an atom.

If there is no apostraphe before a preceding list then the first item
of the list is a function. If there is an apostophe then the list is just
taken as is.



# Why I switched to Spacemacs

I wrote these out for someone. I prefer to see spacemacs as a vim featureset expansion.

1. Vimscript sucks and vim isn't really great wrt extendability, extensions are all over the place.
2. I like scheme/lisp and am writing a lot of C this year, emacs seems much better suited for working in both.
3. Spacemacs provides most common keys in vim (but not all!).
    - For example `C-a` in vim is `SPC n +` in spacemacs. It drops chording, a net positive.
4. Vim promises leader keys but you effectively chord enough of your actions that it's a fake claim. Spacemacs uses a space leader for most things.
5. Vim feels stagnant, even if it isn't.
6. The `core featureset` of vim doesn't really need `vim the application` anymore
