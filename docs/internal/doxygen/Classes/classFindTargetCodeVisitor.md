# FindTargetCodeVisitor



Traverses the AST to find target and process target regions and function and variables that are annotated by an 'omp declare target' target pragma. 


`#include <Visitors.h>`

Inherits from clang::RecursiveASTVisitor< FindTargetCodeVisitor >

## Public Functions

|                | Name           |
| -------------- | -------------- |
| | **[FindTargetCodeVisitor](../Classes/classFindTargetCodeVisitor.md#function-findtargetcodevisitor)**([TargetCode](../Classes/classTargetCode.md) & Code, [TypeDeclResolver](../Classes/classTypeDeclResolver.md) & Types, [FunctionDeclResolver](../Classes/classFunctionDeclResolver.md) & Functions, clang::ASTContext & Context) |
| bool | **[TraverseDecl](../Classes/classFindTargetCodeVisitor.md#function-traversedecl)**(clang::Decl * D) |
| bool | **[VisitStmt](../Classes/classFindTargetCodeVisitor.md#function-visitstmt)**(clang::Stmt * S) |
| bool | **[VisitDecl](../Classes/classFindTargetCodeVisitor.md#function-visitdecl)**(clang::Decl * D) |

## Public Functions Documentation

### function FindTargetCodeVisitor

```cpp
inline FindTargetCodeVisitor(
    TargetCode & Code,
    TypeDeclResolver & Types,
    FunctionDeclResolver & Functions,
    clang::ASTContext & Context
)
```


### function TraverseDecl

```cpp
bool TraverseDecl(
    clang::Decl * D
)
```


### function VisitStmt

```cpp
bool VisitStmt(
    clang::Stmt * S
)
```


### function VisitDecl

```cpp
bool VisitDecl(
    clang::Decl * D
)
```


