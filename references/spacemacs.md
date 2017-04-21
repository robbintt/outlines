# Spacemacs Reference Document

## Table of Contents

1. [Reference](#Reference)
  1. [Notes](#Notes)
    1. [Spacemacs State Color Codes](#Spacemacs State Color Codes)
2. [Spacemacs Fixes](#Spacemacs Fixes)
3. [Greg's elisp notes](# Greg's elisp notes)


## Reference

### Useful Sequences

1. Get your major-mode: `C-h v major-mode`
2. Reload stuff/settings: `SPC f e R`
3. Load up non-GUI mode: `$ emacs -nw`
4. Insert any character: `C-q `
1. Increment by q (q=1 by default): `q SPC n -`
  - has some sort of minor mode where you can keep pressing stuff, try it


### Interesting Sequences
1. Incremental Search: `C-s stuff`
  - Note: `/ style` search is already incremental in spacemacs.



### External References
  1. [Migrating from Vim](https://github.com/syl20bnr/spacemacs/blob/master/doc/VIMUSERS.org)



### Notes (From References)

Each note should have a `####` header and be included in the TOC.


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

