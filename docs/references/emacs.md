## Simpler Emacs

I intend to install a number of packages from spacemacs.


### Quickref

1. `M-x`: get a prompt

#### At the prompt

nb: `RET` is `return key`, the whitespace is for readability.

- `package-list-packages RET`: list packages
- `package-install RET`: get a package install prompt
    - `evil RET`: i did not find `evil-mode` in the packages, so installed `evil`

### Installing Packages

The emacs wiki has a [guide](https://www.emacswiki.org/emacs/InstallingPackages).

### Installing use-package

An easier way to install packages? People like it. Seems heavy to me...

- [init.el example with use-package](http://cachestocaches.com/2015/8/getting-started-use-package/)
    - [code](https://github.com/CachesToCaches/getting_started_with_use_package/blob/master/init-use-package.el)


### Customize Group

- M-x customize-group seems to have context for customizing stuff
  - try it and choose `undo-tree`

### Notes

1. M-<key>: You can press escape then the key instead of meta.


### Future

1. [Evil Plugins](https://www.emacswiki.org/emacs/Evil#toc6)
    - lots of additional features
1. Undo Tree should go to a directory in $HOME?  right now it goes to $TMPDIR in macos which may be deleted??
1. Undo Tree & Persistent Buffer - done?
    - [emacswiki.org: Category Undo](https://www.emacswiki.org/emacs/CategoryUndo)
    - [UndoTree](https://www.emacswiki.org/emacs/UndoTree): like vim?
        - apparently has a corruption bug with this feature, a fork is incomplete
        - apparently undo-tree does this but it has a major corruption bug with this specific feature, and the solution right now is to use emacs server, so i'm going to do that
1. emacs server - the only way to get persistent undo for now as you never exit the session


### Desired Spacemacs Packages

1. helm
2. evil-mode

### Resources

- [Aaron Bieber's "Vim to Emacs in 14 days" post](https://blog.aaronbieber.com/2015/05/24/from-vim-to-emacs-in-fourteen-days.html)
    - this was pretty out of date but a good general guide
    - took lots of googling to find the right command for evil-mode stuff
- [emacswiki.org: evil](https://www.emacswiki.org/emacs/Evil)
    - [evil plugins](https://www.emacswiki.org/emacs/evil#toc6)
