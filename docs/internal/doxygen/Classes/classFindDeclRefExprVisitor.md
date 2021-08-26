# FindDeclRefExprVisitor






`#include <Visitors.h>`

Inherits from clang::RecursiveASTVisitor< FindDeclRefExprVisitor >

## Public Functions

|                | Name           |
| -------------- | -------------- |
| | **[FindDeclRefExprVisitor](Classes/classFindDeclRefExprVisitor.md#function-finddeclrefexprvisitor)**() |
| bool | **[VisitStmt](Classes/classFindDeclRefExprVisitor.md#function-visitstmt)**(clang::Stmt * S) |
| std::unordered_set< clang::VarDecl * > * | **[getVarSet](Classes/classFindDeclRefExprVisitor.md#function-getvarset)**() |

## Public Functions Documentation

### function FindDeclRefExprVisitor

```cpp
inline FindDeclRefExprVisitor()
```


### function VisitStmt

```cpp
bool VisitStmt(
    clang::Stmt * S
)
```


### function getVarSet

```cpp
inline std::unordered_set< clang::VarDecl * > * getVarSet()
```


