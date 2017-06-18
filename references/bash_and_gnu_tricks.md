## Tricks in GNU and bash 

These are combined because you usually mash them together into a result.




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
