# FindArraySectionVisitor






`#include <Visitors.h>`

Inherits from clang::RecursiveASTVisitor< FindArraySectionVisitor >

## Public Functions

|                | Name           |
| -------------- | -------------- |
| | **[FindArraySectionVisitor](../Classes/classFindArraySectionVisitor.md#function-findarraysectionvisitor)**(std::map< clang::VarDecl *, clang::Expr * > & LowerBoundsMap) |
| bool | **[VisitExpr](../Classes/classFindArraySectionVisitor.md#function-visitexpr)**(clang::Expr * E) |

## Private Attributes

|                | Name           |
| -------------- | -------------- |
| std::map< clang::VarDecl *, clang::Expr * > & | **[LowerBoundsMap](../Classes/classFindArraySectionVisitor.md#variable-lowerboundsmap)**  |

## Public Functions Documentation

### function FindArraySectionVisitor

```cpp linenums="1"
inline FindArraySectionVisitor(
    std::map< clang::VarDecl *, clang::Expr * > & LowerBoundsMap
)
```


### function VisitExpr

```cpp linenums="1"
bool VisitExpr(
    clang::Expr * E
)
```


## Private Attributes Documentation

### variable LowerBoundsMap

```cpp linenums="1"
std::map< clang::VarDecl *, clang::Expr * > & LowerBoundsMap;
```


