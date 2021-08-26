# CollectOMPClauseParamsVarsVisitor





Inherits from clang::RecursiveASTVisitor< CollectOMPClauseParamsVarsVisitor >

## Public Functions

|                | Name           |
| -------------- | -------------- |
| | **[CollectOMPClauseParamsVarsVisitor](Classes/classCollectOMPClauseParamsVarsVisitor.md#function-collectompclauseparamsvarsvisitor)**(std::shared_ptr< [TargetCodeRegion](Classes/classTargetCodeRegion.md) > & TCR) |
| bool | **[VisitStmt](Classes/classCollectOMPClauseParamsVarsVisitor.md#function-visitstmt)**(clang::Stmt * S) |

## Public Functions Documentation

### function CollectOMPClauseParamsVarsVisitor

```cpp
inline CollectOMPClauseParamsVarsVisitor(
    std::shared_ptr< TargetCodeRegion > & TCR
)
```


### function VisitStmt

```cpp
inline bool VisitStmt(
    clang::Stmt * S
)
```


