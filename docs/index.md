# Welcome to Aurora OpenMP Offloading Documentation!

This Project's aim is, to create a prototype infrastructure to offload
OpenMP target code written in C to NEC's new SX-Aurora VE architecture.
It uses Clang as driver and host compiler, libomptarget, NEC's `AVEO`
interface to run the code on the VE. As compiler the target code, the
project can work with NEC's ncc compiler or with a Clang compiler which
supports VE as a target for LLVM.

## Usage

To compile a source file which contains target code for the VE
architecture with ncc as target compiler, compile the source code with
this project's clang and set the openmp target triple to
`aurora-nec-veort-unknown` e.g.

``` console
clang -fopenmp -fopenmp-targets=aurora-nec-veort-unknown input.c
```

## Overview

To provide OpenMP offloading to SX-Aurora VE devices with Clang as host
compiler, this project provides the following components:

-   A version of LLVM, modified so that Clang can recognize a new target
    triple for the VE architecture (Whether or not Clang/LLVM is actually
    used as target compiler).
-   A modified version of Clang that can invoke the projects source
    transformation tool and a target compiler for offloading. As part of
    the Clang repository:
    -   A source transformation tool to extract target code from an
        input file and rewrite it as input for a target compiler.
    -   A set of wrapper tools that Clang can call to automatically
        transform and compile the input code with the selected target
        compiler.
-   A plugin for LLVM's libomptarget which offloads the target code at
    runtime using NEC's AVEO api.

All these components are provided within a single
[llvm-project](%%llvm%%)-repository.
