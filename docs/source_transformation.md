# Source Transformation with sotoc

The source transformation tool sotoc is now part of the [llvm-project]({{ link.llvm }}){target=_blank}
repository (under `clang/tools/sotoc`) and is build automatically with Clang.
Please see [Installation](install.md) for installation or build instructions.

## Overview
sotoc itself is invoked during compilation by the wrapper tool (see [Build Wrapper](build_wrapper.md)),
which itself is called by the Clang driver instead of the actual target compiler.
sotoc itself only needs to be invoked directly during development and testing.

The tool can be invoked (both by the wrapper tools and during testing) by the following command line:

``` shell
sotoc input.c -- <clang command line>
```

Where `<clang command line>` contains all command line options that Clang uses to compile the target code.
This has, at least, to include `-fopenmp` but **does not include** the `-fopenmp-targets` option (passing the `-fopenmp-targets` option will result in an error).

When invoked, sotoc searches for all variables, function, and type declarations in the input file that are either annotated by a directive, `#!c #pragma omp declare target`,
or are referenced in a target region or another function required on the target.
It then copies them into the output source file.
sotoc also searches for all target regions in the input file and transforms them into functions,
so the region's code can be called independently of its original context.
During this transformation, sotoc generates function arguments for all variables captured by the region and generates code to copy those variables into the scope of the new function.

!!! warning
    To work around limitations of the LLVM/Clang offloading infrastructure,
    global static variables which are copied into the output source file,
    have their `static`-keyword removed.
    This will probably break some code, but there is currently no better workaround available.

!!! example
    === "Original Code"
        ``` c linenums="1"
        # pragma omp declare target
        int n = 10240;
        # pragma omp end declare target
        void saxpy () {
            float a = 42.0f; float b = 23.0f; float *x, *y;
            // Allocate and init x , y ...
            # pragma omp target map (to: x[0:n], a) map(tofrom: y[0:n])
            # pragma omp parallel for
            for (int i = 0; i < n; ++i) {
                y[i] = a * x[i] + y[i];
            }
        }
        ```
    === "Transformed Code"
        ``` c linenums="1"
        int n = 10240;
        void __omp_ofld_b73b_saxpy_l4 (int n, float *y, float *__sotoc_var_a, float *x) {
            float a = *__sotoc_var_a;
            # pragma omp parallel for
                for (int i = 0; i < n; ++i) {
                    y[i] = a * x[i] + y[i];
                }
            *__sotoc_var_a = a;
        }
        ```

## Testing
The tool comes with a regression test suite using `llvm-lit`.
If the CMake option `SOTOC_ENABLE_TESTS` is set to `ON`, The tests can be run with:

``` shell
make check-sotoc
```

Make sure that LLVM's `FileCheck` tool is in the path, then the test suite can be run with `#!shell make check-sotoc`

--8<-- "includes/abbreviations.md"
