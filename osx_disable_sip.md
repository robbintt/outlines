### How to get a terminal and remove System Integrity Protection in OSX

1. Hold [CMD+R] to get a recovery menu.
    - If this doesn't work (osx sierra bug) then use [CMD+OPT+R], internet recovery.
2. In the top menu choose `Utilities->Terminal`
3. Type `csrutil disable`
    - Success message will show
4. Perform system modifications
5. `csrutil enable` - ENABLE SIP AGAIN.  This is a pretty good defense mechanism. 

