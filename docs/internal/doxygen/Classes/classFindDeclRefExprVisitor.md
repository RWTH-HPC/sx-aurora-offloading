# FindDeclRefExprVisitor






`#include <Visitors.h>`

Inherits from clang::RecursiveASTVisitor< FindDeclRefExprVisitor >

## Public Functions

|                | Name           |
| -------------- | -------------- |
| | **[FindDeclRefExprVisitor](../Classes/classFindDeclRefExprVisitor.md#function-finddeclrefexprvisitor)**() |
| bool | **[VisitStmt](../Classes/classFindDeclRefExprVisitor.md#function-visitstmt)**(clang::Stmt * S)<br>Visit function for statements.  |
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

Visit function for statements. 

**Parameters**: 

  * **S** Given statement 


Statement Visitor for the [FindDeclRefExprVisitor](../Classes/classFindDeclRefExprVisitor.md)


### function getVarSet

```cpp linenums="1"
inline std::unordered_set< clang::VarDecl * > * getVarSet()
```


## Private Attributes Documentation

### variable VarSet

```cpp linenums="1"
std::unordered_set< clang::VarDecl * > VarSet;
```



