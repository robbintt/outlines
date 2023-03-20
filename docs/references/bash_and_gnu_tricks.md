## Tricks in GNU and bash 

These are combined because you usually mash them together into a result.


### History

Taken from `https://www.washington.edu/computing/unix/history.html`

It is also possible to use certain words from commands and do a regular expression type modifier.  This may not be worth learning.

- `!!` repeat last command
- `!-n` repeat n commands ago, examples:
    - `!-2`, repeat 2 commands ago
    - `!-1` == `!!`, repeat last command
- `!n` repeat nth command as indexed in `history` command
- `!<substring>` repeats most recent command beginning with `<substring>`


### strace - trace system calls and signals

1. Example: `sudo strace -f -o slack.trace su robbintt -c 'slack'`

I used this to trace where my ubuntu 16.04 `slack` app was silently failing. I thought it must be a file permissions error because the command `slack` would run for root but not for user. Strace showed me the files touched before failing.


### reverse-I Search

Use ctrl+r and start typing.  This 'reverse-I-search' is a 
more convenient way to search history.

It is also a nice trick to tag commands you will need.

For example:

ls -la /some/long/directory # mytag

Then just search the tag in reverse i search
