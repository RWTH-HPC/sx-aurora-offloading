# Basic Structure and Design

## Libomptarget
Libomptarget provides the offloading implementation for the target devices via plugins.
Libomptarget and the plugins can be found in the [llvm repository](%%llvm%%) in the `openmp/libomptarget`
and `openmp/libomptarget/plugins*` directories respectively.

!!! note
    The plugin API is in `openmp/libomptarget/include/omptargetplugin.h`

The Aurora VE plugin (`openmp/libomptarget/plugins/ve`) is based on the generic x64 offloading plugin
`generic-elf-64bit` (`openmp/libomptarget/plugins/generic-elf-64bit/`).
The AVEO library is used to implement the plugin functions and NECs `libveosinfo` provides with `veo_node_info` additional information about the nodes.
These are used to provide the number of present devices in the `__tgt_rtl_number_of_devices` plugin function.
The target image can be either linked dynamically as a normal shared library or as statically linked executable (ELF).

## Target Table
In addition to the *target image*, a *target table* is inserted by the compiler into the host-binary.
This table has entries for every target region and global variable in the form of an array of `struct __tgt_offload_entry`(openmp/libomptarget/include/omptarget.h).

!!! note
    The Table does not include functions marked by `#pragma omp declare target`.

The libomptarget plugin function `__tgt_rtl_load_binary` passes the target table of the host binary to the plugin and expects a target table with the host addresses of all the symbols in return.
`veo_get_sym` is used to resolve all the symbols in the table.

To examine the target table of a host binary, the following command can be used:
``` shell
objdump -s -j omp_offloading_entries a.out
```

## Clang integration

