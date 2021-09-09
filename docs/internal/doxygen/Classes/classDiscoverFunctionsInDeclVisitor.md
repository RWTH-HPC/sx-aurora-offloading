# DiscoverFunctionsInDeclVisitor



Traverses (parts of) the AST to find DeclRefExpr that refer to functions that need to be present for that part of the AST to compile correctly.  [More...](#detailed-description)


`#include <Visitors.h>`

Inherits from clang::RecursiveASTVisitor< DiscoverFunctionsInDeclVisitor >

## Public Functions

|                | Name           |
| -------------- | -------------- |
| | **[DiscoverFunctionsInDeclVisitor](../Classes/classDiscoverFunctionsInDeclVisitor.md#function-discoverfunctionsindeclvisitor)**([FunctionDeclResolver](../Classes/classFunctionDeclResolver.md) & Functions)<br>Construct a new Discover Functions In Decl Visitor:: Discover Functions In Decl Visitor object.  |
| bool | **[VisitExpr](../Classes/classDiscoverFunctionsInDeclVisitor.md#function-visitexpr)**(clang::Expr * E)<br>Visit function for Expressions.  |

## Public Attributes

|                | Name           |
| -------------- | -------------- |
| | **[__pad0__](../Classes/classDiscoverFunctionsInDeclVisitor.md#variable-__pad0__)**  |

## Private Attributes

|                | Name           |
| -------------- | -------------- |
| std::function< void(clang::FunctionDecl *)> | **[OnEachFuncRef](../Classes/classDiscoverFunctionsInDeclVisitor.md#variable-oneachfuncref)**  |

## Detailed Description

```cpp linenums="1"
class DiscoverFunctionsInDeclVisitor;
```

Traverses (parts of) the AST to find DeclRefExpr that refer to functions that need to be present for that part of the AST to compile correctly. 

This way functions declared and defined in the same compilation unit do not need to be annotated by the 'omp declare target' pragma. The Visitor is not only used to search through target regions, but also through the found functions themselves and through functions that are annotated with the 'omp declare target' pragma, to find all necessary dependencies recursively. 

## Public Functions Documentation

### function DiscoverFunctionsInDeclVisitor

```cpp linenums="1"
DiscoverFunctionsInDeclVisitor(
    FunctionDeclResolver & Functions
)
```

Construct a new Discover Functions In Decl Visitor:: Discover Functions In Decl Visitor object. 

**Parameters**: 

  * **Functions** 


### function VisitExpr

```cpp linenums="1"
bool VisitExpr(
    clang::Expr * E
)
```

Visit function for Expressions. 

**Parameters**: 

  * **E** Given expression 


Expression Visitor in [DiscoverFunctionsInDeclVisitor](../Classes/classDiscoverFunctionsInDeclVisitor.md)


## Public Attributes Documentation

### variable __pad0__

```cpp linenums="1"
__pad0__;
```


## Private Attributes Documentation

### variable OnEachFuncRef

```cpp linenums="1"
std::function< void(clang::FunctionDecl *)> OnEachFuncRef;
```



