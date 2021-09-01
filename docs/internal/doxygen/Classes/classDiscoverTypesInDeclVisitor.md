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

## Private Functions

|                | Name           |
| -------------- | -------------- |
| void | **[processType](../Classes/classDiscoverTypesInDeclVisitor.md#function-processtype)**(const clang::Type * D)<br>Retrieves the declaration of the type found and passes it on.  |

## Public Attributes

|                | Name           |
| -------------- | -------------- |
| | **[__pad0__](../Classes/classDiscoverTypesInDeclVisitor.md#variable-__pad0__)**  |

## Private Attributes

|                | Name           |
| -------------- | -------------- |
| std::function< void(clang::TypeDecl *)> | **[OnEachTypeRef](../Classes/classDiscoverTypesInDeclVisitor.md#variable-oneachtyperef)** <br>Function run on the declaration of each type found by the visitor.  |

## Detailed Description

```cpp linenums="1"
class DiscoverTypesInDeclVisitor;
```

Traverses (parts of) the AST to find DeclRefExpr that refer to types that need to be present for that part of the AST to compile correctly.

The visitor is not only used to search through target regions and functions, but also through type declarations themselves, in order to also find types that the already found types depend on to compile.

## Public Functions Documentation

### function DiscoverTypesInDeclVisitor

```cpp linenums="1"
DiscoverTypesInDeclVisitor(
    TypeDeclResolver & Types
)
```


### function VisitDecl

```cpp linenums="1"
bool VisitDecl(
    clang::Decl * D
)
```


### function VisitExpr

```cpp linenums="1"
bool VisitExpr(
    clang::Expr * D
)
```


### function VisitType

```cpp linenums="1"
bool VisitType(
    clang::Type * T
)
```


## Private Functions Documentation

### function processType

```cpp linenums="1"
void processType(
    const clang::Type * D
)
```

Retrieves the declaration of the type found and passes it on.

## Public Attributes Documentation

### variable __pad0__

```cpp linenums="1"
__pad0__;
```


## Private Attributes Documentation

### variable OnEachTypeRef

```cpp linenums="1"
std::function< void(clang::TypeDecl *)> OnEachTypeRef;
```

Function run on the declaration of each type found by the visitor.

