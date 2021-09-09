# TargetRegionPrinterHelper



Print Helper Class. 

Inherits from PrinterHelper

## Public Functions

|                | Name           |
| -------------- | -------------- |
| | **[TargetRegionPrinterHelper](../Classes/classTargetRegionPrinterHelper.md#function-targetregionprinterhelper)**(clang::PrintingPolicy PP)<br>Construct a new Target Region Printer Helper object.  |
| bool | **[handledStmt](../Classes/classTargetRegionPrinterHelper.md#function-handledstmt)**(clang::Stmt * E, llvm::raw_ostream & OS)<br>Handle Statement.  |

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

Construct a new Target Region Printer Helper object. 

**Parameters**: 

  * **PP** 


### function handledStmt

```cpp linenums="1"
inline bool handledStmt(
    clang::Stmt * E,
    llvm::raw_ostream & OS
)
```

Handle Statement. 

**Parameters**: 

  * **E** Statement 
  * **OS** Out stream 


## Private Attributes Documentation

### variable PP

```cpp linenums="1"
clang::PrintingPolicy PP;
```



