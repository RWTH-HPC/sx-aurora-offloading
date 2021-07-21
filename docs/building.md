# Building the Project

This page details, how to build all components for SX-Aurora offloading.

This project now comes as a single [llvm-project](https://github.com/rwth-hpc/llvm-project) repository, forked from LLVM's upstream repository. All components can be checked out from a single source and built, closely following the [Clang build instructions at clang.llvm.org](https://clang.llvm.org/get_started.html).

To build the project, first check out this project [llvm-project](https://github.com/rwth-hpc/llvm-project) respository and switch to the aurora-offloading-prototype brannch before configuring the project with CMake.

## Configure with CMake

After checking out the aurora-offloading-prorotype branch, change the working directory to llvm-project/llvm and run CMake with, at least, the following CMake variables:

-   Set **LLVM\_ENABLE\_PROJECTS** to `clang;openmp;libcxx;libcxxabi` to enable at least *clang*, *openmp*, *libcxx* and *libcxxabi*.
-   Set **OPENMP\_LIBOMPTARGET** to `ON` to enable libomptarget

Additionally, make sure that:

-   **LIBOMPTARGET\_DEP\_VEO\_LIBRARIES** Points to an installation of `libveo.so` (usually found under `/opt/nec/ve/veos/lib64/`)
-   **LIBOMPTARGET\_DEP\_VEOSINFO\_LIBRARIES** Points to an installation of `libveosinfo.so` (usually found under `/opt/nec/ve/veos/lib64/`)
-   **NECAURORA\_TARGET\_COMPILER\_NCC** points to your installation of `ncc` (usually found under `/opt/nec/ve/bin`).

### Static Linking

To be able to statically link the target image, please make sure that, additionally, the following CMake variables are set

-   **NECAURORA\_LIBAVEOVE\_STATIC**, pointing to libaveoVE.a
-   **NECAURORA\_LIBURPCVE\_STATIC**, pointing to liburpcVE\_omp.a
-   **NECAURORA\_LIBVEIO**, pointing to libveio.so

Usually these libraries are installed at /opt/nec/ve/lib.

### Enable Testing

To enable the test suite for the source transformation, simply:

-   Set **SOTOC\_ENABLE\_TESTS** to `ON`.

the test suite uses the `llvm-lit` and `FileCheck` tool build together with the project and uses the project's Clang as test compiler.

## CMake Options

**NECAURORA\_LIBELF\_INCLUDE\_DIR**  
Points to the include directory containing the headers for libelf (required for static linking).

**NECAURORA\_LIBELF\_LIBRARIES**  
Points to a libelf.so (required for static linking).

**NECAURORA\_LIBAVEOVE\_STATIC**  
Points to libaveoVE.a (required for static linking).

**NECAURORA\_LIBURPCVE\_STATIC**  
Points to liburpcVE\_omp.a (required for static linking).

**NECAURORA\_LIBVEIO**  
Points to libveio.so (required for static linking).

**NECAURORA\_TARGET\_COMPILER\_CLANG**  
The path to the clang compiler used for target compilations with the option `-fopenmp-nec-compiler=clang`.

**NECAURORA\_TARGET\_COMPILER\_RVCLANG**  
The path to the target compiler used for target compilations with the option `-fopenmp-nec-compiler=rclang` preset.

**NECAURORA\_TARGET\_COMPILER\_NCC**  
The path to the target compiler used for target compilations with the option `-fopenmp-nec-compiler=ncc`.

**NECAURORA\_DEFAULT\_TARGET\_OPTION**  
The default option for `-fopenmp-nec-compiler=` (defaults to `ncc`).

**SOTOC\_DEBUG\_OUTPUT**  
Enables debug output for sotoc (when the env-var `SOTOC_DEBUG=1` is set).

**SOTOC\_ENABLE\_TESTS**  
Enables the test suite for sotoc (can be called with make check-sotoc).

**SOTOC\_LLVM\_LIT\_EXECUTABLE**  
The llvm-lit executable required for testing.

**LIBOMPTARGET\_DEP\_LIBFFI\_INCLUDE\_DIR**  
The include directory for a libffi installtion (required for Run-On-Host).

**LIBOMPTARGET\_DEP\_LIBFFI\_LIBRARIES**  
The path to a libffi.so (required for Run-On-Host).

**LIBOMPTARGET\_DEP\_VEO\_INCLUDE\_DIR**  
The include directory for ve\_offload.h.

**LIBOMPTARGET\_DEP\_VEO\_LIBRARIES**  
Path to libveo.so.


