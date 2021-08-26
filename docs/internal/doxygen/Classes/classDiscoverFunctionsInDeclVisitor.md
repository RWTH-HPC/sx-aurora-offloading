# DiscoverFunctionsInDeclVisitor



Traverses (parts of) the AST to find DeclRefExpr that refer to functions that need to be present for that part of the AST to compile correctly.  [More...](#detailed-description)


`#include <Visitors.h>`

Inherits from clang::RecursiveASTVisitor< DiscoverFunctionsInDeclVisitor >

## Public Functions

|                | Name           |
| -------------- | -------------- |
| | **[DiscoverFunctionsInDeclVisitor](Classes/classDiscoverFunctionsInDeclVisitor/#function-discoverfunctionsindeclvisitor)**([FunctionDeclResolver](Classes/classFunctionDeclResolver/) & Functions) |
| bool | **[VisitExpr](Classes/classDiscoverFunctionsInDeclVisitor/#function-visitexpr)**(clang::Expr * E) |

## Public Attributes

|                | Name           |
| -------------- | -------------- |
| | **[__pad0__](Classes/classDiscoverFunctionsInDeclVisitor/#variable-__pad0__)**  |

## Detailed Description

```cpp
class DiscoverFunctionsInDeclVisitor;
```

Traverses (parts of) the AST to find DeclRefExpr that refer to functions that need to be present for that part of the AST to compile correctly. 

This way functions declared and defined in the same compilation unit do not need to be annotated by the 'omp declare target' pragma. The Visitor is not only used to search through target regions, but also through the found functions themselves and through functions that are annotated with the 'omp declare target' pragma, to find all necessary dependencies recursively. 

## Public Functions Documentation

### function DiscoverFunctionsInDeclVisitor

```cpp
DiscoverFunctionsInDeclVisitor(
    FunctionDeclResolver & Functions
)
```


### function VisitExpr

```cpp
bool VisitExpr(
    clang::Expr * E
)
```


## Public Attributes Documentation

### variable __pad0__

```cpp
__pad0__;
```


