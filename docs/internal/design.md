# Basic Structure and Design

!!! danger
    This page is for internal and development use only.

## Libomptarget
Libomptarget provides the offloading implementation for the target devices via plugins.
Libomptarget and the plugins can be found in the [llvm repository](%%llvm%%) in the `openmp/libomptarget`
and `openmp/libomptarget/plugins*` directories respectively.

!!! note
    The plugin API is in `openmp/libomptarget/include/omptargetplugin.h`

The Aurora VE plugin (`openmp/libomptarget/plugins/ve`) is based on the generic x64 offloading plugin
`generic-elf-64bit` (`openmp/libomptarget/plugins/generic-elf-64bit/`).
The AVEO library is used to implement the plugin functions and NECs `libveosinfo` provides with `veo_node_info` additional information about the nodes.
These are used to provide the number of present devices in the `#!c __tgt_rtl_number_of_devices` plugin function.
The target image can be either linked dynamically as a normal shared library or as statically linked executable (ELF).

## Target Table
In addition to the *target image*, a *target table* is inserted by the compiler into the host-binary.
This table has entries for every target region and global variable in the form of an array of `#!c struct __tgt_offload_entry` (`openmp/libomptarget/include/omptarget.h`).

!!! note
    The Table does not include functions marked by `#!c #pragma omp declare target`.

The libomptarget plugin function `#!c __tgt_rtl_load_binary` passes the target table of the host binary to the plugin and expects a target table with the host addresses of all the symbols in return.
`#!c veo_get_sym` is used to resolve all the symbols in the table.

To examine the target table of a host binary, the following command can be used:
``` shell
objdump -s -j omp_offloading_entries a.out
```

## Clang integration
The compilation pipeline is scheduled by the clang driver (`lang/lib/Driver/`).
The toolchains for the different architectures can be found in `clang/lib/Driver/ToolChains`.
For the offloading pipeline, additional compile and link jobs are added to the usual compilation pipeline. Those will produce the target image.
Afterwards the `clang-offload-wrapper` is used to wrap the image into the LLVM bitcode file, so it can be linked into the host binary.

!!! note
    In case the user splits the compilation and linking (e.g. `#!shell clang -c`), the `clang-offload-bundler` is used to combine the files to one.

The Aurora pipeline is defined in `clang/lib/Driver/ToolChains/NECAuroraOffload.{h,cpp}`, which, in the end, calls `#!shell ncc`.
Some additional code is located in `clang/lib/Driver/Driver.cpp` and `clang/lib/Driver/Compilation.cpp`.

Because `#!shell ncc` is the host compiler for the VE, the code received by clang has to be split up in the host and target sections. This is done with the source transformation tool `#!shell sotoc`.
For that the toolchain calls `clang/tools/nec-aurora-build`.
