# Source Transformation with `sotoc`

The source transformation tool `sotoc` is part of the projects [Clang](https://git.rwth-aachen.de/NEC-RWTH-Projects/clang) repository (under tools/sotoc) and is build automatically with clang. Please see [building\_project](building.md)for build instructions.

## Overview

`sotoc` itself is invoked during compilation by the wrapper tool (see [build-wrapper](build_wrapper.md)), which itself is called by the clang driver instead of the actual target compiler. `sotoc` itself only needs to be invoked directly during development and testing.

The tool can be invoked (both by the wrapper tools and during testing) by the following command line:

``` {.sourceCode .console}
$ sotoc input.c -- <clang command line>
```

where `<clang command line>` contains all command line options that clang uses to compile the target code. This has, at least, to include -fopenmp but **does not include** the -fopenmp-targets option (passing the -fopenmp-targets option will result in an error).

When invoked, `sotoc` searches for all variables, function and type declarations in the input file that are either annotated by a directive `#pragma omp declare target`, or are referenced in a target region or another function required on the target, and copies them into the output source file. It also searches for all target regions in the input file and transforms them into functions, so the region's code can be called independently from its original context. During this transformation, sotoc generates function arguments for all variables captured by the region and generates code to copy those variables into the scope of the new function.

> **note**
>
> To work around limitations of the LLVM/Clang offloading  
> infrastructure, global static variables which are copied into the output source file, have their `static`-keyword removed. This will probably break some code, but there is currently no better workaround available.
>

## Testing

The tool comes with a regression test suite using llvm-lit. If the CMake option `SOTOC_ENABLE_TESTS` is set to `ON`, The tests can be run with:

``` {.sourceCode .console}
$ make check-sotoc
```

Make sure that LLVM's `FileCheck` tool is in the path, then the test suite can be run with `$ make check-sotoc`
