# clang-tool-example
Shows how to make your own tools based on llvm's libClang / libTooling

## Introduction

LLVM has done some good work to allow access to compiler internals such as the abstact syntax tree.
This allows interesting internally-supported tools like clang-format and clang-tidy to bw written.
However, the LLVM team has not done a great job allowing external tools this same level of access.
The LLVM documentation has several source code examples of how to use
[libClang](https://clang.llvm.org/docs/LibClang.html) and
[libTooling](https://clang.llvm.org/docs/LibTooling.html), but none of them actually show how to
compile / link that source code.

The answer to one of the only [Stack
Overflow](https://stackoverflow.com/questions/26688988/how-to-build-clang-libtooling-on-mac-os)
questions about this is to copy your code into the llvm source tree and build it there. That's .. ok
I guess, but it dismisses decades of software engineering principles about code modularity and
version control. The LLVM team is not interested in my tool, so it doesn't make sense for them to
let me check in my tool's source code into the LLVM git repo. Am I really supposed to not version
control my own tool source code? Or copy it from my git repo into the LLVM tree every time I want to
compile it?

It is amusing that a group specializing in compiling things is so bad at actually showing you how to
compile things, and how hard they make it to do so. So, that is what this repo tries to do. It
attempts to show how, using a modern version of LLVM, you can build a tool that uses libTooling.

This example has been tested on macOS and Linux (ubuntu). Windows users, I love you but you are on your
own here, for now anyway.

Here is an overview of the process:
- Compile your own llvm from source. This step is not strictly necessary, but if you want a reasonable
  amount of control over the tool you want to write, you want to have tight control over your dependencies.
- Install some additional libraries
- Configure this example
- Build this example

Note: as of this writing, libClang is a shared library, which complicates the distribution and use of any
tool you build. Is there a way to build LLVM such that libClang is a static library? I'm not sure - haven't
looked that deeply into the LLVM build process. It would be extremely useful, because it would make these
kind of tools more portable.

## Pre-requisites

### Compile and Install LLVM

```
git clone https://github.com/llvm/llvm-project.git
cd llvm-project
cmake -S llvm -B build -G Ninja -DCMAKE_BUILD_TYPE=Release -DLLVM_ENABLE_PROJECTS='clang;clang-tools-extra'
cmake --build build
cmake --install build --prefix $HOME/llvm
```

### Get libzstd

On macOS: `brew install zstd`. Note the directory where the library was installed (in the Cellar) via `brew list zstd`.

## Configure and build this project

```
cmake -S . -B build -G Ninja -DCMAKE_BUILD_TYPE=Release -DLLVM_DIR=${HOME}/llvm -DZSTD_DIR=<path from above>
cmake --build build
```

That's it. You should now have a tool in `build/TBD`.

## Make it your own

OK. Great. You have built this example. Now what? 



