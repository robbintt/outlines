## Tricks in GNU and bash 

These are combined because you usually mash them together into a result.




### strace - trace system calls and signals

1. Example: `sudo strace -f -o slack.trace su robbintt -c 'slack'`

I used this to trace where my ubuntu 16.04 `slack` app was silently failing. I thought it must be a file permissions error because the command `slack` would run for root but not for user. Strace showed me the files touched before failing.
