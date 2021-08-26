# TargetRegionVariable



Represents a variable captured by a target region.  [More...](#detailed-description)


`#include <TargetRegionVariable.h>`

## Public Classes

|                | Name           |
| -------------- | -------------- |
| class | **[shape_const_kind_iterator](Classes/classTargetRegionVariable_1_1shape__const__kind__iterator.md)** <br>Iterator which acts as a filter over std::vector<TargetRegionVariableShape>::const_iterator (the base_iter) which only passes on [TargetRegionVariableShape](Classes/classTargetRegionVariableShape.md) of the kind specified in [Kind]().  |

## Public Types

|                | Name           |
| -------------- | -------------- |
| using std::vector< [TargetRegionVariableShape](Classes/classTargetRegionVariableShape.md) >::const_iterator | **[shape_const_iterator](Classes/classTargetRegionVariable.md#using-shape_const_iterator)** <br>Iterator of all shapes of this variable.  |
| using llvm::iterator_range< [shape_const_iterator](Classes/classTargetRegionVariable.md#using-shape_const_iterator) > | **[shape_const_range](Classes/classTargetRegionVariable.md#using-shape_const_range)** <br>Range over all shapes of this variable.  |
| using llvm::iterator_range< [shape_const_kind_iterator](Classes/classTargetRegionVariable_1_1shape__const__kind__iterator.md) > | **[shape_const_kind_range](Classes/classTargetRegionVariable.md#using-shape_const_kind_range)** <br>Range over all shapes of a certain kind of this variable.  |

## Public Functions

|                | Name           |
| -------------- | -------------- |
| llvm::StringRef | **[name](Classes/classTargetRegionVariable.md#function-name)**() const<br>The name of the variable.  |
| llvm::StringRef | **[baseTypeName](Classes/classTargetRegionVariable.md#function-basetypename)**() const<br>The name of the base type (stripped of all qualifiers).  |
| clang::VarDecl * | **[getDecl](Classes/classTargetRegionVariable.md#function-getdecl)**() const<br>The Decl node of the variable.  |
| bool | **[containsArray](Classes/classTargetRegionVariable.md#function-containsarray)**() const<br>Whether this variable's type contains an array or not.  |
| bool | **[containsPointer](Classes/classTargetRegionVariable.md#function-containspointer)**() const<br>Whether this variable's type contains a pointer or not.  |
| bool | **[passedByPointer](Classes/classTargetRegionVariable.md#function-passedbypointer)**() const<br>Returns true if this variable is passed by pointer.  |
| llvm::Optional< clang::Expr * > | **[arrayLowerBound](Classes/classTargetRegionVariable.md#function-arraylowerbound)**() const<br>The lower bound of an array slice in the first dimension.  |
| bool | **[operator==](Classes/classTargetRegionVariable.md#function-operator==)**(const [TargetRegionVariable](Classes/classTargetRegionVariable.md) & Other) const |
| [shape_const_range](Classes/classTargetRegionVariable.md#using-shape_const_range) | **[shapes](Classes/classTargetRegionVariable.md#function-shapes)**() const<br>Gives a range over the shape of all dimensions.  |
| [shape_const_kind_range](Classes/classTargetRegionVariable.md#using-shape_const_kind_range) | **[variableArrayShapes](Classes/classTargetRegionVariable.md#function-variablearrayshapes)**() const<br>Gives a range over those shape dimensions which are variable arrays.  |
| | **[TargetRegionVariable](Classes/classTargetRegionVariable.md#function-targetregionvariable)**(const clang::CapturedStmt::Capture * Capture, const std::map< clang::VarDecl *, clang::Expr * > & MappingLowerBounds) |

## Detailed Description

```cpp
class TargetRegionVariable;
```

Represents a variable captured by a target region. 

This class is an abstraction that provides information on how the variable is passed to the target region, whether it is a slice or array and how it's dimensionality is declared 

## Public Types Documentation

### using shape_const_iterator

```cpp
using TargetRegionVariable::shape_const_iterator =  std::vector<TargetRegionVariableShape>::const_iterator;
```

Iterator of all shapes of this variable. 

### using shape_const_range

```cpp
using TargetRegionVariable::shape_const_range =  llvm::iterator_range<shape_const_iterator>;
```

Range over all shapes of this variable. 

### using shape_const_kind_range

```cpp
using TargetRegionVariable::shape_const_kind_range =  llvm::iterator_range<shape_const_kind_iterator>;
```

Range over all shapes of a certain kind of this variable. 

## Public Functions Documentation

### function name

```cpp
inline llvm::StringRef name() const
```

The name of the variable. 

### function baseTypeName

```cpp
inline llvm::StringRef baseTypeName() const
```

The name of the base type (stripped of all qualifiers). 

### function getDecl

```cpp
inline clang::VarDecl * getDecl() const
```

The Decl node of the variable. 

### function containsArray

```cpp
bool containsArray() const
```

Whether this variable's type contains an array or not. 

**Return**: true if an array is contained, false otherwise 

Check if the shape of a [TargetRegionVariable](Classes/classTargetRegionVariable.md) contains an array.


### function containsPointer

```cpp
bool containsPointer() const
```

Whether this variable's type contains a pointer or not. 

**Return**: true if a pointer is contained, false otherwise 

Check if the shape of a [TargetRegionVariable](Classes/classTargetRegionVariable.md) contains an pointer.


### function passedByPointer

```cpp
bool passedByPointer() const
```

Returns true if this variable is passed by pointer. 

This is the case for shared and first-private variables scalars and for arrays. Note that pointer types are generally passed by value and we do not generate an additional * for it. 


### function arrayLowerBound

```cpp
llvm::Optional< clang::Expr * > arrayLowerBound() const
```

The lower bound of an array slice in the first dimension. 

All other dimension can be ignored because libomptarget only transfers continuous data. In case of a scalar (or an array which is mapped completly in the first dimension) this returns 0. 


### function operator==

```cpp
inline bool operator==(
    const TargetRegionVariable & Other
) const
```


### function shapes

```cpp
inline shape_const_range shapes() const
```

Gives a range over the shape of all dimensions. 

### function variableArrayShapes

```cpp
inline shape_const_kind_range variableArrayShapes() const
```

Gives a range over those shape dimensions which are variable arrays. 

This is called while generating the functions argument for variable array sizes. 


### function TargetRegionVariable

```cpp
TargetRegionVariable(
    const clang::CapturedStmt::Capture * Capture,
    const std::map< clang::VarDecl *, clang::Expr * > & MappingLowerBounds
)
```


