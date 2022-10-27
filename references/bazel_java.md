
# Bazel and Java

Installed `bazel` and `adoptopenjdk` via homebrew for now.


## Goal

Get a java env up suitable for modern java dev. Make something interesting.

### Subgoals:

1. easily use tmux+vim to navigate and work
	- build on file change
2. follow modern java patterns
	- maven
	- bazel
3. deploy to aws lambda, ecs, or to local k3s


## How do I target AWS java

No idea, guess I install it and specify it in the bazel build?

- amazon-corretto-11
- amazon-corretto-8
- java-1.8.0-openjdk


## References

- [bazelbuild/rules_jvm_external](https://github.com/bazelbuild/rules_jvm_external)
- [bazelbuild/bazel: Java and Bazel](https://github.com/bazelbuild/bazel/blob/master/site/docs/bazel-and-java.md)
- [Bazel Tutorial: Build a Java Project](https://github.com/bazelbuild/bazel/blob/master/site/docs/tutorial/java.md)
- [aws lambda: java](https://docs.aws.amazon.com/lambda/latest/dg/lambda-java.html)
- [aws sample java handlers](https://docs.aws.amazon.com/lambda/latest/dg/java-handler.html#java-handler-samples)