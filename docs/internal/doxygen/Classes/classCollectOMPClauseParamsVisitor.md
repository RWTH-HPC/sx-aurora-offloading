# CollectOMPClauseParamsVisitor





Inherits from clang::RecursiveASTVisitor< CollectOMPClauseParamsVisitor >

## Public Functions

|                | Name           |
| -------------- | -------------- |
| | **[CollectOMPClauseParamsVisitor](../Classes/classCollectOMPClauseParamsVisitor.md#function-collectompclauseparamsvisitor)**(std::shared_ptr< [TargetCodeRegion](../Classes/classTargetCodeRegion.md) > & TCR) |
| bool | **[VisitStmt](../Classes/classCollectOMPClauseParamsVisitor.md#function-visitstmt)**(clang::Stmt * S) |

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


