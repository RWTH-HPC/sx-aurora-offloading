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
| bool | **[isReplaceable](../Classes/classOmpPragma.md#function-isreplaceable)**(clang::OMPExecutableDirective * Directive)<br>Determines whether a pragma is replacable.  |
| bool | **[needsAdditionalPragma](../Classes/classOmpPragma.md#function-needsadditionalpragma)**(clang::OMPExecutableDirective * Directive)<br>Determines whether a additional pragma is needed.  |

## Private Functions

|                | Name           |
| -------------- | -------------- |
| bool | **[isClausePrintable](../Classes/classOmpPragma.md#function-isclauseprintable)**(clang::OMPClause * Clause)<br>Determine whether a clause is printable.  |
| void | **[rewriteParam](../Classes/classOmpPragma.md#function-rewriteparam)**(std::string * In)<br>Rewrite clause parameters.  |
| void | **[printClauses](../Classes/classOmpPragma.md#function-printclauses)**(llvm::raw_ostream & Out)<br>Print OMP Clauses.  |

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

**Return**: true If a structured block is needed 

false If no structured block is needed 

Determines whether a structured block is needed for a pragma.

{...}).


### function printReplacement

```cpp linenums="1"
void printReplacement(
    llvm::raw_ostream & Out
)
```

Prints a replacement omp pragma for the encapsulated pragma onto `Out`. 

**Parameters**: 

  * **Out** Out stream 


Print replacement pragmas.

In some cases we have to modify the printed pragma. If we have a combined constructs with target, remove target because we are already running on the target device. If we have a combined construct with teams, remove teams because the runtime can decide to spawn only a single team. If we have a simd, we prepend `#pragma _NEC ivdep` to indicate no dependencies.


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

Determines whether a pragma is replacable. 

**Parameters**: 

  * **Directive** Given Directive 


**Return**: true If the directive is replacable 

false If the directive is not replacable 

### function needsAdditionalPragma

```cpp linenums="1"
static bool needsAdditionalPragma(
    clang::OMPExecutableDirective * Directive
)
```

Determines whether a additional pragma is needed. 

**Parameters**: 

  * **Directive** given directive 


**Return**: true Directive needs an additional pragma 

false Directive does not need an additional pragma 

## Private Functions Documentation

### function isClausePrintable

```cpp linenums="1"
bool isClausePrintable(
    clang::OMPClause * Clause
)
```

Determine whether a clause is printable. 

**Parameters**: 

  * **Clause** Clause to check 


**Return**: true If the clause is printable 

false If the clause is not printable 

Checks for a clause the clause kind and determines which clauses are printable.


### function rewriteParam

```cpp linenums="1"
void rewriteParam(
    std::string * In
)
```

Rewrite clause parameters. 

**Parameters**: 

  * **In** Parameter as string (everything in brackets) 


Rewrites OMP clause parameters if they are variables to replace the variable name with the one we will use as the function argument.


### function printClauses

```cpp linenums="1"
void printClauses(
    llvm::raw_ostream & Out
)
```

Print OMP Clauses. 

**Parameters**: 

  * **Out** Out stream 


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



