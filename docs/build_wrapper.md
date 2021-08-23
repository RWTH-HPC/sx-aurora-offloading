# Build Wrapper

The project comes with a wrapper tool, necaurora-ofld-wrapper,
which helps integrating the target compiler and the source transformation tool
(see [Source Transformation](source_transformation.md)) and static linking into the build process of the Clang driver.

When the Clang driver compiles a \*.c file for a target, it calls the wrapper tool instead of a compiler.
The wrapper tool then applies the source transformation tool to the input .c file and saves the output in a temporary file.
Then the wrapper tool forwards the compiler arguments it got from the Clang driver to the real target compiler,
substituting the real input .c file with the output of the source transformation.

When the Clang driver tries to statically link object files into a static target image (with `-Xlinker -fopenmp-static`),
then the wrapper tool intercepts that call to the linker,
creates a .c file with a symbol table required by the VEO api and constructs a correct command line to call ncc for static linking.

In all other cases, the wrapper tool just passes on its command line to the target compiler.

## Command Line Arguments

The wrapper tool tries forwards all input arguments to the target compiler (except in case of static linking). It has only two command line arguments that are its own and are never forwarded:

- `--sotoc-path=`: With this argument, the driver can set the path to the source transformation tool to be used during compilation by the wrapper.
- `-fopenmp-nec-compiler=` selects the compiler for target compilation. This flag has the same semantics as the `-fopenmp-nec-compiler=` flag of the clang driver (the argument is passed through from the clang driver). See usage for details.
- `-Xlinker -fopenmp-target`: With this argument, the driver can instruct the wrapper to use static linking of the target image.

# Environment Variables

The behaviour of the wrapper can be influenced by the following environment variables

**TMPDIR**, **TEMP**, **TMP**
Like Clang, the wrapper tool checks each of these environment variables in that order,
to find the place to store its temporary files (for the source transformation and the static linking symbol table).
When none of these exist, it falls back to `/tmp`.
When the environment variable `NECAURORA_KEEP_FILES_DIR` is set, the specified path is used instead.

**NECAURORA_KEEP_FILES_DIR**
If this environment variable is set, the wrapper tools will store its temporary files in the specified directory and will NOT delete them after the tool is done.
