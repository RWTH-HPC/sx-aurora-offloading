# TargetRegionVariableShape



Describes the shape, i.e.  [More...](#detailed-description)


`#include <TargetRegionVariable.h>`

## Public Types

|                | Name           |
| -------------- | -------------- |
| enum| **[ShapeKind](../Classes/classTargetRegionVariableShape.md#enum-shapekind)** { Pointer, Paren, ConstantArray, VariableArray} |

## Public Functions

|                | Name           |
| -------------- | -------------- |
| [ShapeKind](../Classes/classTargetRegionVariableShape.md#enum-shapekind) | **[getKind](../Classes/classTargetRegionVariableShape.md#function-getkind)**() const |
| bool | **[isVariableArray](../Classes/classTargetRegionVariableShape.md#function-isvariablearray)**() const |
| bool | **[isConstantArray](../Classes/classTargetRegionVariableShape.md#function-isconstantarray)**() const |
| bool | **[isArray](../Classes/classTargetRegionVariableShape.md#function-isarray)**() const |
| bool | **[isPointer](../Classes/classTargetRegionVariableShape.md#function-ispointer)**() const |
| unsigned int | **[getVariableDimensionIndex](../Classes/classTargetRegionVariableShape.md#function-getvariabledimensionindex)**() const<br>If the shape is a variable array, return the array dimension index, (used for generating __sotoc_vla_dimX_ parameters in which the host signals the array's size).  |
| llvm::StringRef | **[getConstantDimensionExpr](../Classes/classTargetRegionVariableShape.md#function-getconstantdimensionexpr)**() const<br>If the shape is a constant array, it returns the rendered expression for the constant size.  |
| | **[TargetRegionVariableShape](../Classes/classTargetRegionVariableShape.md#function-targetregionvariableshape)**()<br>Construct a pointer shape by default.  |
| | **[TargetRegionVariableShape](../Classes/classTargetRegionVariableShape.md#function-targetregionvariableshape)**(const clang::ParenType * Paren)<br>Construct a parentheses shape.  |
| | **[TargetRegionVariableShape](../Classes/classTargetRegionVariableShape.md#function-targetregionvariableshape)**(const clang::VariableArrayType * Array, unsigned int DimIndex)<br>Construct a shape for a variable array dimension.  |
| | **[TargetRegionVariableShape](../Classes/classTargetRegionVariableShape.md#function-targetregionvariableshape)**(const clang::ConstantArrayType * Array)<br>Construct a shape for a constant array dimension.  |

## Private Attributes

|                | Name           |
| -------------- | -------------- |
| unsigned int | **[VariableDimensionIndex](../Classes/classTargetRegionVariableShape.md#variable-variabledimensionindex)**  |
| std::string | **[ConstantDimensionExpr](../Classes/classTargetRegionVariableShape.md#variable-constantdimensionexpr)**  |
| [ShapeKind](../Classes/classTargetRegionVariableShape.md#enum-shapekind) | **[Kind](../Classes/classTargetRegionVariableShape.md#variable-kind)**  |

## Detailed Description

```cpp linenums="1"
class TargetRegionVariableShape;
```

Describes the shape, i.e.

a variable dimension of constant or variable size, or a pointer. We collect this information for every parameter of a target region function because the pretty printer does not support the output format for variable and types (e.g. it prints 'int (*)[SIZE] a' instead of 'int (*) a[SIZE]'), so we print this manually in [TargetCode.cpp](../Files/TargetCode_8cpp.md#file-targetcode.cpp). For this we need every pointer indirection and array dimension which each is saved as shapes for that variable.

## Public Types Documentation

### enum ShapeKind

| Enumerator | Value | Description |
| ---------- | ----- | ----------- |
| Pointer | |   |
| Paren | |   |
| ConstantArray | |   |
| VariableArray | |   |




## Public Functions Documentation

### function getKind

```cpp linenums="1"
inline ShapeKind getKind() const
```


### function isVariableArray

```cpp linenums="1"
inline bool isVariableArray() const
```


### function isConstantArray

```cpp linenums="1"
inline bool isConstantArray() const
```


### function isArray

```cpp linenums="1"
inline bool isArray() const
```


### function isPointer

```cpp linenums="1"
inline bool isPointer() const
```


### function getVariableDimensionIndex

```cpp linenums="1"
inline unsigned int getVariableDimensionIndex() const
```

If the shape is a variable array, return the array dimension index, (used for generating __sotoc_vla_dimX_ parameters in which the host signals the array's size).

### function getConstantDimensionExpr

```cpp linenums="1"
inline llvm::StringRef getConstantDimensionExpr() const
```

If the shape is a constant array, it returns the rendered expression for the constant size.

### function TargetRegionVariableShape

```cpp linenums="1"
inline TargetRegionVariableShape()
```

Construct a pointer shape by default.

### function TargetRegionVariableShape

```cpp linenums="1"
inline TargetRegionVariableShape(
    const clang::ParenType * Paren
)
```

Construct a parentheses shape.

### function TargetRegionVariableShape

```cpp linenums="1"
inline TargetRegionVariableShape(
    const clang::VariableArrayType * Array,
    unsigned int DimIndex
)
```

Construct a shape for a variable array dimension.

### function TargetRegionVariableShape

```cpp linenums="1"
inline TargetRegionVariableShape(
    const clang::ConstantArrayType * Array
)
```

Construct a shape for a constant array dimension.

## Private Attributes Documentation

### variable VariableDimensionIndex

```cpp linenums="1"
unsigned int VariableDimensionIndex;
```


### variable ConstantDimensionExpr

```cpp linenums="1"
std::string ConstantDimensionExpr;
```


### variable Kind

```cpp linenums="1"
ShapeKind Kind;
```


