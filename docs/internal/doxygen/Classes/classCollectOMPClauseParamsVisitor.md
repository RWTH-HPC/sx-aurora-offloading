# CollectOMPClauseParamsVisitor





Inherits from clang::RecursiveASTVisitor< CollectOMPClauseParamsVisitor >

## Public Functions

|                | Name           |
| -------------- | -------------- |
| | **[CollectOMPClauseParamsVisitor](../Classes/classCollectOMPClauseParamsVisitor.md#function-collectompclauseparamsvisitor)**(std::shared_ptr< [TargetCodeRegion](../Classes/classTargetCodeRegion.md) > & TCR) |
| bool | **[VisitStmt](../Classes/classCollectOMPClauseParamsVisitor.md#function-visitstmt)**(clang::Stmt * S) |

## Private Attributes

|                | Name           |
| -------------- | -------------- |
| CollectOMPClauseParamsVarsVisitor | **[VarsVisitor](../Classes/classCollectOMPClauseParamsVisitor.md#variable-varsvisitor)**  |
| bool | **[InExplicitCast](../Classes/classCollectOMPClauseParamsVisitor.md#variable-inexplicitcast)**  |

## Public Functions Documentation

### function CollectOMPClauseParamsVisitor

```cpp
inline CollectOMPClauseParamsVisitor(
    std::shared_ptr< TargetCodeRegion > & TCR
)
```


### function VisitStmt

```cpp
inline bool VisitStmt(
    clang::Stmt * S
)
```


## Private Attributes Documentation

### variable VarsVisitor

```cpp
CollectOMPClauseParamsVarsVisitor VarsVisitor;
```


### variable InExplicitCast

```cpp
bool InExplicitCast;
```


