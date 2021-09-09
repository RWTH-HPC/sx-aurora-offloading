# CollectOMPClauseParamsVarsVisitor



OMP clause visitor. 

Inherits from clang::RecursiveASTVisitor< CollectOMPClauseParamsVarsVisitor >

## Public Functions

|                | Name           |
| -------------- | -------------- |
| | **[CollectOMPClauseParamsVarsVisitor](../Classes/classCollectOMPClauseParamsVarsVisitor.md#function-collectompclauseparamsvarsvisitor)**(std::shared_ptr< [TargetCodeRegion](../Classes/classTargetCodeRegion.md) > & TCR) |
| bool | **[VisitStmt](../Classes/classCollectOMPClauseParamsVarsVisitor.md#function-visitstmt)**(clang::Stmt * S) |

## Private Attributes

|                | Name           |
| -------------- | -------------- |
| std::shared_ptr< [TargetCodeRegion](../Classes/classTargetCodeRegion.md) > | **[TCR](../Classes/classCollectOMPClauseParamsVarsVisitor.md#variable-tcr)**  |

## Public Functions Documentation

### function CollectOMPClauseParamsVarsVisitor

```cpp linenums="1"
inline CollectOMPClauseParamsVarsVisitor(
    std::shared_ptr< TargetCodeRegion > & TCR
)
```


### function VisitStmt

```cpp linenums="1"
inline bool VisitStmt(
    clang::Stmt * S
)
```


## Private Attributes Documentation

### variable TCR

```cpp linenums="1"
std::shared_ptr< TargetCodeRegion > TCR;
```



