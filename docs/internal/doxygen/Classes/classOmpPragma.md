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

## Private Functions

|                | Name           |
| -------------- | -------------- |
| bool | **[isClausePrintable](../Classes/classOmpPragma.md#function-isclauseprintable)**(clang::OMPClause * Clause) |
| void | **[rewriteParam](../Classes/classOmpPragma.md#function-rewriteparam)**(clang::OMPClause * Clause, std::string * In) |
| void | **[addShared](../Classes/classOmpPragma.md#function-addshared)**(clang::OMPClause * Clause, std::string * In, llvm::raw_ostream & Out) |
| void | **[printClauses](../Classes/classOmpPragma.md#function-printclauses)**(llvm::raw_ostream & Out) |

## Private Attributes

|                | Name           |
| -------------- | -------------- |
| clang::PrintingPolicy | **[PP](../Classes/classOmpPragma.md#variable-pp)**  |
| llvm::ArrayRef< clang::OMPClause * > | **[Clauses](../Classes/classOmpPragma.md#variable-clauses)**  |
| clang::OpenMPDirectiveKind | **[Kind](../Classes/classOmpPragma.md#variable-kind)**  |
| unsigned int | **[ClauseParamCounter](../Classes/classOmpPragma.md#variable-clauseparamcounter)**  |

## Detailed Description

```cpp linenums="1"
class OmpPragma;
```

A helper class to rewrite some "pragma omp" (mostly teams and similar combined constructs), which are not supported by sotoc.

We currently only support one team to be run on the target because ncc does not support 'freestanding' teams. So we need to remove teams and distribute constructs from the generated target code. But teams constructs can also appear in combined constructs. These combined constructs cannot simply be removed, they must be replace by "non-team" equivalents to preserve correctness. This class provides helper functions that finds a suitable replacement for omp pragmas that contain teams constructs. It is used during code generation: The omp pragma of each target region that is declared as part of a combined construct and each pragma found during pretty printing is encapsulated by an object of this class which is then used to generate a replacement.

## Public Functions Documentation

### function OmpPragma

```cpp linenums="1"
inline OmpPragma(
    TargetCodeRegion * TCR
)
```


### function OmpPragma

```cpp linenums="1"
inline OmpPragma(
    clang::OMPExecutableDirective * Directive,
    clang::PrintingPolicy PP
)
```


### function needsStructuredBlock

```cpp linenums="1"
bool needsStructuredBlock()
```

Returns true if the omp pragma encapsulated, needs to be followed by a structured block (i.e.

{...}).


### function printReplacement

```cpp linenums="1"
void printReplacement(
    llvm::raw_ostream & Out
)
```

Prints a replacement omp pragma for the encapsulated pragma onto `Out`.

### function printAddition

```cpp linenums="1"
void printAddition(
    llvm::raw_ostream & Out
)
```


### function isReplaceable

```cpp linenums="1"
static bool isReplaceable(
    clang::OMPExecutableDirective * Directive
)
```


### function needsAdditionalPragma

```cpp linenums="1"
static bool needsAdditionalPragma(
    clang::OMPExecutableDirective * Directive
)
```


## Private Functions Documentation

### function isClausePrintable

```cpp linenums="1"
bool isClausePrintable(
    clang::OMPClause * Clause
)
```


### function rewriteParam

```cpp linenums="1"
void rewriteParam(
    clang::OMPClause * Clause,
    std::string * In
)
```


### function addShared

```cpp linenums="1"
void addShared(
    clang::OMPClause * Clause,
    std::string * In,
    llvm::raw_ostream & Out
)
```


### function printClauses

```cpp linenums="1"
void printClauses(
    llvm::raw_ostream & Out
)
```


## Private Attributes Documentation

### variable PP

```cpp linenums="1"
clang::PrintingPolicy PP;
```


### variable Clauses

```cpp linenums="1"
llvm::ArrayRef< clang::OMPClause * > Clauses;
```


### variable Kind

```cpp linenums="1"
clang::OpenMPDirectiveKind Kind;
```


### variable ClauseParamCounter

```cpp linenums="1"
unsigned int ClauseParamCounter;
```


