# Target Code Generation
!!! danger "Attention"
    This page is for internal and development use only.

The general process to the target code generation is as follows:

1. The code's AST is processed with `RecursiveASTVisitor`s ([`clang/tools/sotoc/Visitors.{h,cpp}`](doxygen/Files/Visitors_8cpp.md))
2. The found target code is recorded in [`TargetCodeFragment`](doxygen/Classes/classTargetCodeFragment.md) ([`clang/tools/sotoc/TargetCode.{h,pp}`](doxygen/Files/TargetCode_8cpp.md) and [`clang/tools/sotoc/TargetCodeFragment.{h,cpp}`](doxygen/Files/TargetCodeFragment_8cpp.md))
3. The fragments are then 'reconstituted' into valid target code.

This transforms C code like
``` c linenums="1"
int main(void) {
  int x = 0;
  int y = 1;
  int z = 2;

  #pragma omp target map(tofrom:x)
  {
    x = x + y + z;
  }
}
```
into
``` c linenums="1"
void __omp_offloading_38_272a6c6b_main_l7(int *__sotoc_var_x, int y, int z)
{
   int x = *__sotoc_var_x;

  {
    x = x + y + z;
  }

  *__sotoc_var_x = x;
}
```

The target code is thereby transformed into a function with the mapped variables as arguments.

## Extracting Target Code from the AST
The Clang AST of a source file can be viewed using the following command:

``` shell
clang -Xclang -ast-dump -fsyntax-only -fopenmp code.c
```

!!! info
    Without the `-fopenmp` flag Clang ignores `#!c #pragma omp`.

Target regions are separate statements in the AST and functions and variables declared with `#!c #pragma omp declare target` get a special attribute added to their AST node.
The [`FindTargetCodeVisitor`](doxygen/Classes/classFindTargetCodeVisitor.md) in [`Visitors.{h,cpp}`](doxygen/Files/Visitors_8cpp.md) is used for that.

!!! warning
    This does not apply the type declarations and there is no guaranty that all functions used in the target region are declared in `#!c #pragma omp declare target`.

To solve the issue we search all target regions, declared functions and variables to additional types, functions, and variables.
This is done by the [`DiscoverTypesInDeclVisitor`](doxygen/Classes/classDiscoverTypesInDeclVisitor.md) and [`DiscoverFunctionsInDeclVisitor`](doxygen/Classes/classDiscoverFunctionsInDeclVisitor.md).
As types can be derived from other types (e.g., `#!c struct`s or `#!c typedef`-chains) and
functions can depend on other functions and additional types,
those dependencies have to be resolved using the [`DeclResolver`](doxygen/Classes/classDeclResolver.md) (in [`clang/tools/sotoc/DeclResolver.{h,cpp}`](doxygen/Files/DeclResolver_8cpp.md)).

## Analysing and Recording the Target Code
Before target code can be generated, additional information about variable mappings have to be collected.

- Private variables are not mapped.
  For those we have to create a declaration in the target region using the [`FindPrivateVariablesVisitor`](doxygen/Classes/classFindPrivateVariablesVisitor.md).

- First-private variables (which is the default) are passed by value into the target region.

- Variables mapped using `from` or `tofrom`, are passed by pointer.
  For `ncc` to process them, we bring the variable into scope by copying them into a local variable and afterwards back.

- Arrays are mapped as pointer.
  If only an array slice (e.g., `#!c map(to:array[10:])`) is mapped, we have to detect the bounds with the [`FindArraySectionVisitor`](doxygen/Classes/classFindArraySectionVisitor.md)
  and move the returned pointer (`#!c array[10]`) in the target region.
  Multi-dimensional arrays have to be cast, so they can be accessed using the `#!c array[x]` notation.

To recognize the variable form we use the [`TargetRegionVariable`](doxygen/Classes/classTargetRegionVariable.md) class in [`clang/tools/sotoc/TargetRegionVariable.{h,cpp}`](doxygen/Files/TargetRegionVariable_8cpp.md).

In addition, we have to rewrite the OpenMP pragma directive and add the appropriate clauses ([`OmpPragma.{h,cpp}`](doxygen/Files/OmpPragma_8cpp.md)).
For example if a `#!c #pragma omp target parallel` is encountered, an additional `parallel` region has to be added.
Some clauses are not supported by the reduced `#!c #pragma`. Those are filtered out or replaced.
Parameters to clauses are also transferred as function arguments of the target function.

## Code Generation
An Object of the [`TargetCode`](doxygen/Classes/classTargetCode.md) class, serves as a collection of [`TargetCodeFragment`](doxygen/Classes/classTargetCodeFragment.md)s and generates the code.
When adding code fragments, [`TargetCode`](doxygen/Classes/classTargetCode.md) sorts them according to their position in the original source file.
We try to generate as little code as possible ourselves and let Clangs `PrettyPrinter` do most of the work, like functions and global variables.

!!! bug
    Clangs `PrettyPrinter` is designed for compiler diagnostics and can not do e.g., anonymous `#!c struct`s and `#!c enum`s.

!!! note
    We extended the `PrettyPrinter` to handle `Decl`s.

We still have to generate functions for regions with mapped variables and clause parameters as arguments and local declarations to bring variables into scope as mentioned [above](#analysing-and-recording-the-target-code).

!!! bug
    Mappings with missing elements in the middle are currently not completely mapped by libomptarget/the OpenMP runtime.

--8<-- "includes/abbreviations.md"
