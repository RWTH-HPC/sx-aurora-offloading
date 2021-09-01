# FindPrivateVariablesVisitor






`#include <Visitors.h>`

Inherits from clang::RecursiveASTVisitor< FindPrivateVariablesVisitor >

## Public Functions

|                | Name           |
| -------------- | -------------- |
| | **[FindPrivateVariablesVisitor](../Classes/classFindPrivateVariablesVisitor.md#function-findprivatevariablesvisitor)**(clang::SourceLocation TopSourceLocation, clang::SourceManager & SM) |
| bool | **[VisitExpr](../Classes/classFindPrivateVariablesVisitor.md#function-visitexpr)**(clang::Expr * E) |
| std::set< clang::VarDecl * > & | **[getVarSet](../Classes/classFindPrivateVariablesVisitor.md#function-getvarset)**() |

## Private Attributes

|                | Name           |
| -------------- | -------------- |
| clang::SourceManager & | **[SM](../Classes/classFindPrivateVariablesVisitor.md#variable-sm)**  |
| clang::SourceLocation | **[RegionTopSourceLocation](../Classes/classFindPrivateVariablesVisitor.md#variable-regiontopsourcelocation)**  |
| std::set< clang::VarDecl * > | **[VarSet](../Classes/classFindPrivateVariablesVisitor.md#variable-varset)**  |

## Public Functions Documentation

### function FindPrivateVariablesVisitor

```cpp linenums="1"
inline FindPrivateVariablesVisitor(
    clang::SourceLocation TopSourceLocation,
    clang::SourceManager & SM
)
```


### function VisitExpr

```cpp linenums="1"
bool VisitExpr(
    clang::Expr * E
)
```


### function getVarSet

```cpp linenums="1"
inline std::set< clang::VarDecl * > & getVarSet()
```


## Private Attributes Documentation

### variable SM

```cpp linenums="1"
clang::SourceManager & SM;
```


### variable RegionTopSourceLocation

```cpp linenums="1"
clang::SourceLocation RegionTopSourceLocation;
```


### variable VarSet

```cpp linenums="1"
std::set< clang::VarDecl * > VarSet;
```


