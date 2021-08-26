# TargetRegionVariableShape



Describes the shape, i.e.  [More...](#detailed-description)


`#include <TargetRegionVariable.h>`

## Public Types

|                | Name           |
| -------------- | -------------- |
| enum| **[ShapeKind](Classes/classTargetRegionVariableShape/#enum-shapekind)** { Pointer, Paren, ConstantArray, VariableArray} |

## Public Functions

|                | Name           |
| -------------- | -------------- |
| [ShapeKind](Classes/classTargetRegionVariableShape/#enum-shapekind) | **[getKind](Classes/classTargetRegionVariableShape/#function-getkind)**() const |
| bool | **[isVariableArray](Classes/classTargetRegionVariableShape/#function-isvariablearray)**() const |
| bool | **[isConstantArray](Classes/classTargetRegionVariableShape/#function-isconstantarray)**() const |
| bool | **[isArray](Classes/classTargetRegionVariableShape/#function-isarray)**() const |
| bool | **[isPointer](Classes/classTargetRegionVariableShape/#function-ispointer)**() const |
| unsigned int | **[getVariableDimensionIndex](Classes/classTargetRegionVariableShape/#function-getvariabledimensionindex)**() const<br>If the shape is a variable array, return the array dimension index, (used for generating __sotoc_vla_dimX_ parameters in which the host signals the array's size).  |
| llvm::StringRef | **[getConstantDimensionExpr](Classes/classTargetRegionVariableShape/#function-getconstantdimensionexpr)**() const<br>If the shape is a constant array, it returns the rendered expression for the constant size.  |
| | **[TargetRegionVariableShape](Classes/classTargetRegionVariableShape/#function-targetregionvariableshape)**()<br>Construct a pointer shape by default.  |
| | **[TargetRegionVariableShape](Classes/classTargetRegionVariableShape/#function-targetregionvariableshape)**(const clang::ParenType * Paren)<br>Construct a parentheses shape.  |
| | **[TargetRegionVariableShape](Classes/classTargetRegionVariableShape/#function-targetregionvariableshape)**(const clang::VariableArrayType * Array, unsigned int DimIndex)<br>Construct a shape for a variable array dimension.  |
| | **[TargetRegionVariableShape](Classes/classTargetRegionVariableShape/#function-targetregionvariableshape)**(const clang::ConstantArrayType * Array)<br>Construct a shape for a constant array dimension.  |

## Detailed Description

```cpp
class TargetRegionVariableShape;
```

Describes the shape, i.e. 

a variable dimension of constant or variable size, or a pointer. We collect this information for every parameter of a target region function because the pretty printer does not support the output format for variable and types (e.g. it prints 'int (*)[SIZE] a' instead of 'int (*) a[SIZE]'), so we print this manually in [TargetCode.cpp](Files/TargetCode_8cpp/#file-targetcode.cpp). For this we need every pointer indirection and array dimension which each is saved as shapes for that variable. 

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

```cpp
inline ShapeKind getKind() const
```


### function isVariableArray

```cpp
inline bool isVariableArray() const
```


### function isConstantArray

```cpp
inline bool isConstantArray() const
```


### function isArray

```cpp
inline bool isArray() const
```


### function isPointer

```cpp
inline bool isPointer() const
```


### function getVariableDimensionIndex

```cpp
inline unsigned int getVariableDimensionIndex() const
```

If the shape is a variable array, return the array dimension index, (used for generating __sotoc_vla_dimX_ parameters in which the host signals the array's size). 

### function getConstantDimensionExpr

```cpp
inline llvm::StringRef getConstantDimensionExpr() const
```

If the shape is a constant array, it returns the rendered expression for the constant size. 

### function TargetRegionVariableShape

```cpp
inline TargetRegionVariableShape()
```

Construct a pointer shape by default. 

### function TargetRegionVariableShape

```cpp
inline TargetRegionVariableShape(
    const clang::ParenType * Paren
)
```

Construct a parentheses shape. 

### function TargetRegionVariableShape

```cpp
inline TargetRegionVariableShape(
    const clang::VariableArrayType * Array,
    unsigned int DimIndex
)
```

Construct a shape for a variable array dimension. 

### function TargetRegionVariableShape

```cpp
inline TargetRegionVariableShape(
    const clang::ConstantArrayType * Array
)
```

Construct a shape for a constant array dimension. 

