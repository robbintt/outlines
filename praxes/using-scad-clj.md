# Using the `scad-clj` OpenSCAD DSL

This DSL [domain specific language](https://en.wikipedia.org/wiki/Domain-specific_language) was used by [adereth](https://twitter.com/adereth) to make the [dactyl keyboard](https://github.com/adereth/dactyl-keyboard).

OpenSCAD becomes insane after awhile and what it needs most is lisp, because everything needs lisp.


## Install leiningen

What is **leiningen**? 

There are a lot of ways to do this.

- check out the [leiningen website](https://leiningen.org/)
- macos: `brew install leiningen`

On 2017/12/28 the project page says:

> be sure you get version 2.x

### Check your version in a shell

```
$ lein -v

Leiningen 2.8.1 on Java 1.8.0_144 Java HotSpot(TM) 64-Bit Server VM
```

## Get `scad-clj`

Available on github: `https://github.com/farrellm/scad-clj`


### Quickstart!

Based on Adereth's 2014/3/19 Post: [3d printing with Clojure](http://adereth.github.io/blog/2014/04/09/3d-printing-with-clojure/)

Save this code as `example.clj` in the git repository `scad-clj` that you just cloned:

```
;; import scad-clj objects or something
(ns scad-demo.core
  (:use [scad-clj.scad])
  (:use [scad-clj.model]))

;; make something called primitives
(def primitives (sphere 50))

;; export primitives to scad
(spit "example.scad" (write-scad primitives))
```

1. In a shell, `cd` into the scad-clj project directory: `cd scad-clj`
1. Run the `example.clj` file: `$ lein repl < example.clj`
1. Start the OpenSCAD program
	1. Navigate to and open the generated example.scad in OpenSCAD
	1. You can now make changes to `example.clj` as you wish, recompile them, and reload the file in OpenSCAD.
	1. As an example, try changing the sphere to size 50 in `example.clj`
		1. run the repl command
		1. your OpenSCAD instance should auto reload
		1. If not, choose `file->reload` or `CMD+r` on a mac.
1. Todo: run from **your own project directory**, `not scad-clj`.
	- Otherwise it's messy and hard to keep stuff under source control.
  - Use adereth's `dactyl` project as a template (avoid users needing to know much about clojure/lein/OpenSCAD before starting)


### References

1. [OpenSCAD User Manual/The OpenSCAD Language](https://en.wikibooks.org/wiki/OpenSCAD_User_Manual/The_OpenSCAD_Language)

