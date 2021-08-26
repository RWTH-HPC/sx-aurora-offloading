# FindArraySectionVisitor






`#include <Visitors.h>`

Inherits from clang::RecursiveASTVisitor< FindArraySectionVisitor >

## Public Functions

|                | Name           |
| -------------- | -------------- |
| | **[FindArraySectionVisitor](Classes/classFindArraySectionVisitor/#function-findarraysectionvisitor)**(std::map< clang::VarDecl *, clang::Expr * > & LowerBoundsMap) |
| bool | **[VisitExpr](Classes/classFindArraySectionVisitor/#function-visitexpr)**(clang::Expr * E) |

## Public Functions Documentation

### function FindArraySectionVisitor

```cpp
inline FindArraySectionVisitor(
    std::map< clang::VarDecl *, clang::Expr * > & LowerBoundsMap
)
```


### function VisitExpr

```cpp
bool VisitExpr(
    clang::Expr * E
)
```


