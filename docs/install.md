# Installation

This page details, how to install or build all components for SX-Aurora offloading.

## Installing the Package
NEC provides LLVM including our OpenMP offloading implementation as package in a YUM repository.
The packaged version is not always up to date with the state of development but includes many other features and functions.

=== "Install from RPM"
    1. Download `llvm-ve-rv-{{ version.rpm }}-{{ version.rpm }}-1.el8.x86_64.rpm`
      ``` shell
      wget https://sx-aurora.com/repos/llvm/x86_64/llvm-ve-rv-{{ version.rpm }}-{{ version.rpm }}-1.el8.x86_64.rpm
      ```
    2. Install RPM
      ``` shell
      sudo yum install ./llvm-ve-rv-{{ version.rpm }}-{{ version.rpm }}-1.el8.x86_64.rpm
      ```

=== "Install from YUM Repository"
    1. Add the `https://sx-aurora.com/repos/llvm/x86_64/` yum repository to your `/etc/yum.repo.d` (consult [How to add a Yum repository](https://www.redhat.com/sysadmin/add-yum-repository#manually-set-up-a-respository){target=_blank} by Red Hat)
    2. Install `llvm-ve-rv-{{ version.rpm }}`
      ``` shell
      sudo yum install llvm-ve-rv-{{ version.rpm }}
      ```

## Building the Project
This project now comes as a single [llvm-project]({{ link.llvm }}){target=_blank} repository,
forked from LLVM's upstream repository.
All components can be checked out from a single source and built,
closely following the [Clang build instructions](https://Clang.llvm.org/get_started.html){target=_blank}.

To build the project, first check out the [llvm-project]({{ link.llvm }}){target=_blank} repository and
switch to the `aurora-offloading` branch before configuring the project with CMake.

### Configure with CMake
After checking out the `aurora-offloading` branch,
change the working directory to `llvm-project/llvm` and run CMake with, at least,
the following CMake variables:

- Set `LLVM_ENABLE_PROJECTS` to `clang;openmp;libcxx;libcxxabi` to enable at least *clang*, *openmp*, *libcxx* and *libcxxabi*.
- Set `OPENMP_LIBOMPTARGET` to `ON` to enable libomptarget

Additionally, make sure that:

- `LIBOMPTARGET_DEP_VEO_LIBRARIES` Points to an installation of `libveo.so` (usually found under `/opt/nec/ve/veos/lib64/`)
- `LIBOMPTARGET_DEP_VEOSINFO_LIBRARIES` Points to an installation of `libveosinfo.so` (usually found under `/opt/nec/ve/veos/lib64/`)
- `NECAURORA_TARGET_COMPILER_NCC` points to your installation of `ncc` (usually found under `/opt/nec/ve/bin`).

#### Static Linking
To be able to statically link the target image, please make sure that, additionally, the following CMake variables are set

- `NECAURORA_LIBAVEOVE_STATIC`, pointing to `libaveoVE.a`
- `NECAURORA_LIBURPCVE_STATIC`, pointing to `liburpcVE_omp.a`
- `NECAURORA_LIBVEIO`, pointing to `libveio.so`

Usually these libraries are installed at `/opt/nec/ve/lib`.

#### Enable Testing
To enable the test suite for the source transformation, simply set `SOTOC_ENABLE_TESTS` to `ON`.

The test suite uses the `llvm-lit` and `FileCheck` tool build together with the project and uses the project's Clang as test compiler.

### CMake Options
- `NECAURORA_LIBELF_INCLUDE_DIR`
Points to the include directory containing the headers for `libelf.so` (required for static linking).

- `NECAURORA_LIBELF_LIBRARIES`
  Points to a `libelf.so` (required for static linking).

- `NECAURORA_LIBAVEOVE_STATIC`
  Points to `libaveoVE.a` (required for static linking).

- `NECAURORA_LIBURPCVE_STATIC`
  Points to `liburpcVE_omp.a` (required for static linking).

- `NECAURORA_LIBVEIO`
  Points to `libveio.so` (required for static linking).

- `NECAURORA_TARGET_COMPILER_CLANG`
  The path to the Clang compiler used for target compilations with the option `-fopenmp-nec-compiler=clang`.

- `NECAURORA_TARGET_COMPILER_RVCLANG`
  The path to the target compiler used for target compilations with the option `-fopenmp-nec-compiler=rclang` preset.

- `NECAURORA_TARGET_COMPILER_NCC`
  The path to the target compiler used for target compilations with the option `-fopenmp-nec-compiler=ncc`.

- `NECAURORA_DEFAULT_TARGET_OPTION`
  The default option for `-fopenmp-nec-compiler=` (defaults to `ncc`).

- `SOTOC_DEBUG_OUTPUT`
  Enables debug output for sotoc (when the env-var `SOTOC_DEBUG=1` is set).

- `SOTOC_ENABLE_TESTS`
  Enables the test suite for sotoc (can be called with make `check-sotoc`).

- `SOTOC_LLVM_LIT_EXECUTABLE`
  The `llvm-lit` executable required for testing.

- `LIBOMPTARGET_DEP_LIBFFI_INCLUDE_DIR`
  The include-directory for a `libffi` installation (required for Run-On-Host).

- `LIBOMPTARGET_DEP_LIBFFI_LIBRARIES`
  The path to a `libffi.so` (required for Run-On-Host).

- `LIBOMPTARGET_DEP_VEO_INCLUDE_DIR`
  The include-directory for `ve_offload.h`.

- `LIBOMPTARGET_DEP_VEO_LIBRARIES`
  Path to `libveo.so`/`libaveo.so`.

--8<-- "includes/abbreviations.md"
