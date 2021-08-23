# Building the Project

This page details, how to build all components for SX-Aurora offloading.

This project now comes as a single [llvm-project](%%llvm%%) repository,
forked from LLVM's upstream repository.
All components can be checked out from a single source and built,
closely following the [Clang build instructions](https://clang.llvm.org/get_started.html).

To build the project, first check out the [llvm-project](%%llvm%%) repository and
switch to the aurora-offloading-prototype branch before configuring the project with CMake.

## Configure with CMake

After checking out the aurora-offloading-prototype branch,
change the working directory to llvm-project/llvm and run CMake with, at least,
the following CMake variables:

- Set **LLVM_ENABLE_PROJECTS** to `clang;openmp;libcxx;libcxxabi` to enable at least *clang*, *openmp*, *libcxx* and *libcxxabi*.
- Set **OPENMP_LIBOMPTARGET** to `ON` to enable libomptarget

Additionally, make sure that:

- **LIBOMPTARGET_DEP_VEO_LIBRARIES** Points to an installation of `libveo.so` (usually found under `/opt/nec/ve/veos/lib64/`)
- **LIBOMPTARGET_DEP_VEOSINFO_LIBRARIES** Points to an installation of `libveosinfo.so` (usually found under `/opt/nec/ve/veos/lib64/`)
- **NECAURORA_TARGET_COMPILER_NCC** points to your installation of `ncc` (usually found under `/opt/nec/ve/bin`).

### Static Linking

To be able to statically link the target image, please make sure that, additionally, the following CMake variables are set

- **NECAURORA_LIBAVEOVE_STATIC**, pointing to libaveoVE.a
- **NECAURORA_LIBURPCVE_STATIC**, pointing to liburpcVE_omp.a
- **NECAURORA_LIBVEIO**, pointing to libveio.so

Usually these libraries are installed at `/opt/nec/ve/lib`.

### Enable Testing

To enable the test suite for the source transformation, simply:

- Set **SOTOC_ENABLE_TESTS** to `ON`.

the test suite uses the `llvm-lit` and `FileCheck` tool build together with the project and uses the project's Clang as test compiler.

## CMake Options

- **NECAURORA_LIBELF_INCLUDE_DIR**
Points to the include directory containing the headers for libelf (required for static linking).

- **NECAURORA_LIBELF_LIBRARIES**
  Points to a libelf.so (required for static linking).

- **NECAURORA_LIBAVEOVE_STATIC**
  Points to libaveoVE.a (required for static linking).

- **NECAURORA_LIBURPCVE_STATIC**
  Points to liburpcVE_omp.a (required for static linking).

- **NECAURORA_LIBVEIO**
  Points to libveio.so (required for static linking).

- **NECAURORA_TARGET_COMPILER_CLANG**
  The path to the clang compiler used for target compilations with the option `-fopenmp-nec-compiler=clang`.

- **NECAURORA_TARGET_COMPILER_RVCLANG**
  The path to the target compiler used for target compilations with the option `-fopenmp-nec-compiler=rclang` preset.

- **NECAURORA_TARGET_COMPILER_NCC**
  The path to the target compiler used for target compilations with the option `-fopenmp-nec-compiler=ncc`.

- **NECAURORA_DEFAULT_TARGET_OPTION**
  The default option for `-fopenmp-nec-compiler=` (defaults to `ncc`).

- **SOTOC_DEBUG_OUTPUT**
  Enables debug output for sotoc (when the env-var `SOTOC_DEBUG=1` is set).

- **SOTOC_ENABLE_TESTS**
  Enables the test suite for sotoc (can be called with make check-sotoc).

- **SOTOC_LLVM_LIT_EXECUTABLE**
  The llvm-lit executable required for testing.

- **LIBOMPTARGET_DEP_LIBFFI_INCLUDE_DIR**
  The include directory for a libffi installation (required for Run-On-Host).

- **LIBOMPTARGET_DEP_LIBFFI_LIBRARIES**
  The path to a libffi.so (required for Run-On-Host).

- **LIBOMPTARGET_DEP_VEO_INCLUDE_DIR**
  The include directory for ve_offload.h.

- **LIBOMPTARGET_DEP_VEO_LIBRARIES**
  Path to libveo.so/libaveo.so.

--8<-- "includes/abbreviations.md"
