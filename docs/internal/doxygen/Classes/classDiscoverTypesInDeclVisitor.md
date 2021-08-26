# DiscoverTypesInDeclVisitor



Traverses (parts of) the AST to find DeclRefExpr that refer to types that need to be present for that part of the AST to compile correctly.  [More...](#detailed-description)


`#include <Visitors.h>`

Inherits from clang::RecursiveASTVisitor< DiscoverTypesInDeclVisitor >

## Public Functions

|                | Name           |
| -------------- | -------------- |
| | **[DiscoverTypesInDeclVisitor](../Classes/classDiscoverTypesInDeclVisitor.md#function-discovertypesindeclvisitor)**([TypeDeclResolver](../Classes/classTypeDeclResolver.md) & Types) |
| bool | **[VisitDecl](../Classes/classDiscoverTypesInDeclVisitor.md#function-visitdecl)**(clang::Decl * D) |
| bool | **[VisitExpr](../Classes/classDiscoverTypesInDeclVisitor.md#function-visitexpr)**(clang::Expr * D) |
| bool | **[VisitType](../Classes/classDiscoverTypesInDeclVisitor.md#function-visittype)**(clang::Type * T) |

## Public Attributes

|                | Name           |
| -------------- | -------------- |
| | **[__pad0__](../Classes/classDiscoverTypesInDeclVisitor.md#variable-__pad0__)**  |

## Detailed Description

```cpp
class DiscoverTypesInDeclVisitor;
```

Traverses (parts of) the AST to find DeclRefExpr that refer to types that need to be present for that part of the AST to compile correctly. 

The visitor is not only used to search through target regions and functions, but also through type declarations themselves, in order to also find types that the already found types depend on to compile. 

## Public Functions Documentation

### function DiscoverTypesInDeclVisitor

```cpp
DiscoverTypesInDeclVisitor(
    TypeDeclResolver & Types
)
```


### function VisitDecl

```cpp
bool VisitDecl(
    clang::Decl * D
)
```


### function VisitExpr

```cpp
bool VisitExpr(
    clang::Expr * D
)
```


### function VisitType

```cpp
bool VisitType(
    clang::Type * T
)
```


## Public Attributes Documentation

### variable __pad0__

```cpp
__pad0__;
```


