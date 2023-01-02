# Git Patch and General Patching

General patching, especially wrt git repositories, both:

1. Committed Changes
2. Uncommitted Changes

## Processes

Some processes are listed below.

1. Patch between two directories with `diff`/`patch` - NO SCM REQUIRED!
    - No need for git, you can keep your files in a signed tarball. Not as useful in a world with popular, collaborative SCM tools.
1. Patch individual files with `git diff`/`patch`.
    - You could actually diff two different files, but in this case it's easier to `git diff` between the file at HEAD and the current file.
1. Patch a git repository by applying actual commits with `git diff`/`git apply`
    - A similar process exists for SVN but is not detailed below, it can also be used to push patches from git to SVN.


### Individual Files and Uncommitted Changes: Use the `patch` command

This process does not require a git repository. You just need two files (or groups of files) to diff to get the output. Then anyone can apply the diff to the old file to get the new one.

1. Make the patch in the desired directory: `git diff --no-prefix > some-feature.diff`
    - This git feature can provide output that `patch` can use.
    - If you are using git: Find where you want to patch from and check the commit out headless, then you can proceed as if the changes are uncommitted (using `patch`).
1. Apply the patch in the same directory: `patch < some-feature.diff`
    - This is not a git feature, it only interacts with the filesystem.


### Committed Changes: Use the `git apply` command

This process requires a git repository.  You can patch commit history onto another `.git` instance.

1. Use the git patch tools: `git diff` and `git apply`
    - This isn't so different than the `patch` command: https://www.lullabot.com/articles/git-best-practices-upgrading-the-patch-process


## Resources

- http://scribu.net/wordpress/svn-patches-from-git.html
- https://markjaquith.wordpress.com/2005/11/02/my-wordpress-toolbox/
- `patch` manpage
