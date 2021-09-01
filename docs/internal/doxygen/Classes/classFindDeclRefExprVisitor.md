# FindDeclRefExprVisitor






`#include <Visitors.h>`

Inherits from clang::RecursiveASTVisitor< FindDeclRefExprVisitor >

## Public Functions

|                | Name           |
| -------------- | -------------- |
| | **[FindDeclRefExprVisitor](../Classes/classFindDeclRefExprVisitor.md#function-finddeclrefexprvisitor)**() |
| bool | **[VisitStmt](../Classes/classFindDeclRefExprVisitor.md#function-visitstmt)**(clang::Stmt * S) |
| std::unordered_set< clang::VarDecl * > * | **[getVarSet](../Classes/classFindDeclRefExprVisitor.md#function-getvarset)**() |

## Private Attributes

|                | Name           |
| -------------- | -------------- |
| std::unordered_set< clang::VarDecl * > | **[VarSet](../Classes/classFindDeclRefExprVisitor.md#variable-varset)**  |

## Public Functions Documentation

### function FindDeclRefExprVisitor

```cpp linenums="1"
inline FindDeclRefExprVisitor()
```


### function VisitStmt

```cpp linenums="1"
bool VisitStmt(
    clang::Stmt * S
)
```


### function getVarSet

```cpp linenums="1"
inline std::unordered_set< clang::VarDecl * > * getVarSet()
```


## Private Attributes Documentation

### variable VarSet

```cpp linenums="1"
std::unordered_set< clang::VarDecl * > VarSet;
```


