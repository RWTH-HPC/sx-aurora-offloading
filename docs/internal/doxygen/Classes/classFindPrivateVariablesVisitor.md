# FindPrivateVariablesVisitor






`#include <Visitors.h>`

Inherits from clang::RecursiveASTVisitor< FindPrivateVariablesVisitor >

## Public Functions

|                | Name           |
| -------------- | -------------- |
| | **[FindPrivateVariablesVisitor](Classes/classFindPrivateVariablesVisitor.md#function-findprivatevariablesvisitor)**(clang::SourceLocation TopSourceLocation, clang::SourceManager & SM) |
| bool | **[VisitExpr](Classes/classFindPrivateVariablesVisitor.md#function-visitexpr)**(clang::Expr * E) |
| std::set< clang::VarDecl * > & | **[getVarSet](Classes/classFindPrivateVariablesVisitor.md#function-getvarset)**() |

## Public Functions Documentation

### function FindPrivateVariablesVisitor

```cpp
inline FindPrivateVariablesVisitor(
    clang::SourceLocation TopSourceLocation,
    clang::SourceManager & SM
)
```


### function VisitExpr

```cpp
bool VisitExpr(
    clang::Expr * E
)
```


### function getVarSet

```cpp
inline std::set< clang::VarDecl * > & getVarSet()
```


