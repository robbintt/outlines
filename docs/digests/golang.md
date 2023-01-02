# Golang Reference


## Local Docs

- go install golang.org/x/tools/cmd/godoc@latest
- godoc -http=:6060


## Path & Setup/Install

This handles go on home path I like. Might replace with asdf or something.

This also handles go commands installed on $GOPATH, like godoc.

```
export GOPATH=$HOME/code/go
export PATH=$PATH:$HOME/.go/go/bin # version these maybe or does asdf handle this?
export PATH=$PATH:$GOPATH/bin
```
