
# Identified as `needs fixed for spacemacs`

5. Turn off auto add closing quotes, braces, brackets, tildes, etc.
6. Make default colors the same as default terminal colors...
7. How do I drill down to my packages? How do I learn about my evil mode configuration and contribute to the evil mode emacs plugin?
9. Consider moving my hotkeys to a helm menu or something, with a space leader instead of C-<key> pattern. Also includes vim functions.
10. Rewrite vim functions for spacemacs
11. Consider alias for bash for spacemacs nongui as default `emacs -nw`
  - Also, consider installing the emacs-plus package from homebrew cask on mac
  - The emacs-plus package is apparently the recommended package by spacemacs, no idea why...
12. Store undo history between sessions for all edited files.
  - manage branching undo history better? may just need training...

# Needs Deeper Research

2. tabs->spaces
  - looks like highlight and <|> indent by 4 spaces in html extension files... not sure how it varies by file extension
  - we want this to be 2 spaces by default and 4 spaces in the .py file extension
  - indentation with the tab also does not always work, it seems to try to force a style from somewhere, tab does not always have an effect
  - tab seems to add spaces when it allows input... this should not follow complex rules, tab should just put 2 spaces in regardless


# Done

1. line numbers on startup, line number toggle?
3. note taken - How do i search for tabs, e.g. \t
4. scroll-margin set to 5
8. C-l should redraw the screen - redraw does not clear search highlighting in emacs...
  - Clear a search with `SPC s c`


# Optional

1. redraw screen with some key combo? - https://www.gnu.org/software/emacs/manual/html_node/elisp/Refresh-Screen.html
  - May already be in spacemacs, check


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

