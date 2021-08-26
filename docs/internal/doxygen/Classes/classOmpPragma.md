# OmpPragma



A helper class to rewrite some "pragma omp" (mostly teams and similar combined constructs), which are not supported by sotoc.  [More...](#detailed-description)


`#include <OmpPragma.h>`

## Public Functions

|                | Name           |
| -------------- | -------------- |
| | **[OmpPragma](../Classes/classOmpPragma.md#function-omppragma)**([TargetCodeRegion](../Classes/classTargetCodeRegion.md) * TCR) |
| | **[OmpPragma](../Classes/classOmpPragma.md#function-omppragma)**(clang::OMPExecutableDirective * Directive, clang::PrintingPolicy PP) |
| bool | **[needsStructuredBlock](../Classes/classOmpPragma.md#function-needsstructuredblock)**()<br>Returns true if the omp pragma encapsulated, needs to be followed by a structured block (i.e.  |
| void | **[printReplacement](../Classes/classOmpPragma.md#function-printreplacement)**(llvm::raw_ostream & Out)<br>Prints a replacement omp pragma for the encapsulated pragma onto `Out`.  |
| void | **[printAddition](../Classes/classOmpPragma.md#function-printaddition)**(llvm::raw_ostream & Out) |
| bool | **[isReplaceable](../Classes/classOmpPragma.md#function-isreplaceable)**(clang::OMPExecutableDirective * Directive) |
| bool | **[needsAdditionalPragma](../Classes/classOmpPragma.md#function-needsadditionalpragma)**(clang::OMPExecutableDirective * Directive) |

## Detailed Description

```cpp
class OmpPragma;
```

A helper class to rewrite some "pragma omp" (mostly teams and similar combined constructs), which are not supported by sotoc. 

We currently only support one team to be run on the target because ncc does not support 'freestanding' teams. So we need to remove teams and distribute constructs from the generated target code. But teams constructs can also appear in combined constructs. These combined constructs cannot simply be removed, they must be replace by "non-team" equivalents to preserve correctness. This class provides helper functions that finds a suitable replacement for omp pragmas that contain teams constructs. It is used during code generation: The omp pragma of each target region that is declared as part of a combined construct and each pragma found during pretty printing is encapsulated by an object of this class which is then used to generate a replacement. 

## Public Functions Documentation

### function OmpPragma

```cpp
inline OmpPragma(
    TargetCodeRegion * TCR
)
```


### function OmpPragma

```cpp
inline OmpPragma(
    clang::OMPExecutableDirective * Directive,
    clang::PrintingPolicy PP
)
```


### function needsStructuredBlock

```cpp
bool needsStructuredBlock()
```

Returns true if the omp pragma encapsulated, needs to be followed by a structured block (i.e. 

{...}). 


### function printReplacement

```cpp
void printReplacement(
    llvm::raw_ostream & Out
)
```

Prints a replacement omp pragma for the encapsulated pragma onto `Out`. 

### function printAddition

```cpp
void printAddition(
    llvm::raw_ostream & Out
)
```


### function isReplaceable

```cpp
static bool isReplaceable(
    clang::OMPExecutableDirective * Directive
)
```


### function needsAdditionalPragma

```cpp
static bool needsAdditionalPragma(
    clang::OMPExecutableDirective * Directive
)
```


