# TargetRegionPrinterHelper





Inherits from PrinterHelper

## Public Functions

|                | Name           |
| -------------- | -------------- |
| | **[TargetRegionPrinterHelper](../Classes/classTargetRegionPrinterHelper.md#function-targetregionprinterhelper)**(clang::PrintingPolicy PP) |
| bool | **[handledStmt](../Classes/classTargetRegionPrinterHelper.md#function-handledstmt)**(clang::Stmt * E, llvm::raw_ostream & OS) |

## Private Attributes

|                | Name           |
| -------------- | -------------- |
| clang::PrintingPolicy | **[PP](../Classes/classTargetRegionPrinterHelper.md#variable-pp)**  |

## Public Functions Documentation

### function TargetRegionPrinterHelper

```cpp linenums="1"
inline TargetRegionPrinterHelper(
    clang::PrintingPolicy PP
)
```


### function handledStmt

```cpp linenums="1"
inline bool handledStmt(
    clang::Stmt * E,
    llvm::raw_ostream & OS
)
```


## Private Attributes Documentation

### variable PP

```cpp linenums="1"
clang::PrintingPolicy PP;
```


