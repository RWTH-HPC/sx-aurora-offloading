# FindLoopStmtVisitor






`#include <Visitors.h>`

Inherits from clang::RecursiveASTVisitor< FindLoopStmtVisitor >

## Public Functions

|                | Name           |
| -------------- | -------------- |
| | **[FindLoopStmtVisitor](../Classes/classFindLoopStmtVisitor.md#function-findloopstmtvisitor)**() |
| bool | **[VisitStmt](../Classes/classFindLoopStmtVisitor.md#function-visitstmt)**(clang::Stmt * S) |
| std::unordered_set< clang::VarDecl * > * | **[getVarSet](../Classes/classFindLoopStmtVisitor.md#function-getvarset)**() |

## Private Attributes

|                | Name           |
| -------------- | -------------- |
| [FindDeclRefExprVisitor](../Classes/classFindDeclRefExprVisitor.md) | **[FindDeclRefVisitor](../Classes/classFindLoopStmtVisitor.md#variable-finddeclrefvisitor)**  |

## Public Functions Documentation

### function FindLoopStmtVisitor

```cpp
inline FindLoopStmtVisitor()
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


## Private Attributes Documentation

### variable FindDeclRefVisitor

```cpp
FindDeclRefExprVisitor FindDeclRefVisitor;
```


