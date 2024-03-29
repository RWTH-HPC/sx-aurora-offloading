# TargetRegionVariable



Represents a variable captured by a target region.  [More...](#detailed-description)


`#include <TargetRegionVariable.h>`

## Public Classes

|                | Name           |
| -------------- | -------------- |
| class | **[shape_const_kind_iterator](../Classes/classTargetRegionVariable_1_1shape__const__kind__iterator.md)** <br>Iterator which acts as a filter over std::vector<TargetRegionVariableShape>::const_iterator (the base_iter) which only passes on [TargetRegionVariableShape](../Classes/classTargetRegionVariableShape.md) of the kind specified in [Kind]().  |

## Public Types

|                | Name           |
| -------------- | -------------- |
| using std::vector< [TargetRegionVariableShape](../Classes/classTargetRegionVariableShape.md) >::const_iterator | **[shape_const_iterator](../Classes/classTargetRegionVariable.md#using-shape_const_iterator)** <br>Iterator of all shapes of this variable.  |
| using llvm::iterator_range< [shape_const_iterator](../Classes/classTargetRegionVariable.md#using-shape_const_iterator) > | **[shape_const_range](../Classes/classTargetRegionVariable.md#using-shape_const_range)** <br>Range over all shapes of this variable.  |
| using llvm::iterator_range< [shape_const_kind_iterator](../Classes/classTargetRegionVariable_1_1shape__const__kind__iterator.md) > | **[shape_const_kind_range](../Classes/classTargetRegionVariable.md#using-shape_const_kind_range)** <br>Range over all shapes of a certain kind of this variable.  |

## Public Functions

|                | Name           |
| -------------- | -------------- |
| llvm::StringRef | **[name](../Classes/classTargetRegionVariable.md#function-name)**() const<br>The name of the variable.  |
| llvm::StringRef | **[baseTypeName](../Classes/classTargetRegionVariable.md#function-basetypename)**() const<br>The name of the base type (stripped of all qualifiers).  |
| clang::VarDecl * | **[getDecl](../Classes/classTargetRegionVariable.md#function-getdecl)**() const<br>The Decl node of the variable.  |
| bool | **[containsArray](../Classes/classTargetRegionVariable.md#function-containsarray)**() const<br>Whether this variable's type contains an array or not.  |
| bool | **[containsPointer](../Classes/classTargetRegionVariable.md#function-containspointer)**() const<br>Whether this variable's type contains a pointer or not.  |
| bool | **[passedByPointer](../Classes/classTargetRegionVariable.md#function-passedbypointer)**() const<br>Returns true if this variable is passed by pointer.  |
| llvm::Optional< clang::Expr * > | **[arrayLowerBound](../Classes/classTargetRegionVariable.md#function-arraylowerbound)**() const<br>The lower bound of an array slice in the first dimension.  |
| bool | **[operator==](../Classes/classTargetRegionVariable.md#function-operator==)**(const [TargetRegionVariable](../Classes/classTargetRegionVariable.md) & Other) const |
| [shape_const_range](../Classes/classTargetRegionVariable.md#using-shape_const_range) | **[shapes](../Classes/classTargetRegionVariable.md#function-shapes)**() const<br>Gives a range over the shape of all dimensions.  |
| [shape_const_kind_range](../Classes/classTargetRegionVariable.md#using-shape_const_kind_range) | **[variableArrayShapes](../Classes/classTargetRegionVariable.md#function-variablearrayshapes)**() const<br>Gives a range over those shape dimensions which are variable arrays.  |
| | **[TargetRegionVariable](../Classes/classTargetRegionVariable.md#function-targetregionvariable)**(const clang::CapturedStmt::Capture * Capture, const std::map< clang::VarDecl *, clang::Expr * > & MappingLowerBounds)<br>Construct a new Target Region Variable:: Target Region Variable object.  |

## Private Functions

|                | Name           |
| -------------- | -------------- |
| void | **[determineShapes](../Classes/classTargetRegionVariable.md#function-determineshapes)**(clang::QualType T)<br>Determine variable shape.  |

## Private Attributes

|                | Name           |
| -------------- | -------------- |
| const clang::CapturedStmt::Capture * | **[Capture](../Classes/classTargetRegionVariable.md#variable-capture)**  |
| clang::VarDecl * | **[Decl](../Classes/classTargetRegionVariable.md#variable-decl)**  |
| std::string | **[VarName](../Classes/classTargetRegionVariable.md#variable-varname)**  |
| std::string | **[BaseTypeName](../Classes/classTargetRegionVariable.md#variable-basetypename)** <br>This is the base type name, i.e.  |
| std::vector< [TargetRegionVariableShape](../Classes/classTargetRegionVariableShape.md) > | **[Shapes](../Classes/classTargetRegionVariable.md#variable-shapes)**  |
| unsigned int | **[NumVariableArrayDims](../Classes/classTargetRegionVariable.md#variable-numvariablearraydims)**  |
| const std::map< clang::VarDecl *, clang::Expr * > & | **[OmpMappingLowerBound](../Classes/classTargetRegionVariable.md#variable-ompmappinglowerbound)**  |

## Detailed Description

```cpp linenums="1"
class TargetRegionVariable;
```

Represents a variable captured by a target region. 

This class is an abstraction that provides information on how the variable is passed to the target region, whether it is a slice or array and how it's dimensionality is declared 

## Public Types Documentation

### using shape_const_iterator

```cpp linenums="1"
using TargetRegionVariable::shape_const_iterator =  std::vector<TargetRegionVariableShape>::const_iterator;
```

Iterator of all shapes of this variable. 

### using shape_const_range

```cpp linenums="1"
using TargetRegionVariable::shape_const_range =  llvm::iterator_range<shape_const_iterator>;
```

Range over all shapes of this variable. 

### using shape_const_kind_range

```cpp linenums="1"
using TargetRegionVariable::shape_const_kind_range =  llvm::iterator_range<shape_const_kind_iterator>;
```

Range over all shapes of a certain kind of this variable. 

## Public Functions Documentation

### function name

```cpp linenums="1"
inline llvm::StringRef name() const
```

The name of the variable. 

### function baseTypeName

```cpp linenums="1"
inline llvm::StringRef baseTypeName() const
```

The name of the base type (stripped of all qualifiers). 

### function getDecl

```cpp linenums="1"
inline clang::VarDecl * getDecl() const
```

The Decl node of the variable. 

### function containsArray

```cpp linenums="1"
bool containsArray() const
```

Whether this variable's type contains an array or not. 

**Return**: true if an array is contained, false otherwise 

Check if the shape of a [TargetRegionVariable](../Classes/classTargetRegionVariable.md) contains an array.


### function containsPointer

```cpp linenums="1"
bool containsPointer() const
```

Whether this variable's type contains a pointer or not. 

**Return**: true if a pointer is contained, false otherwise 

Check if the shape of a [TargetRegionVariable](../Classes/classTargetRegionVariable.md) contains an pointer.


### function passedByPointer

```cpp linenums="1"
bool passedByPointer() const
```

Returns true if this variable is passed by pointer. 

**Return**: true If a variable is passed by pointer 

false If a variable is not passed by pointer 

Determines whether a variable is passed by pointer.

This is the case for shared and first-private variables scalars and for arrays. Note that pointer types are generally passed by value and we do not generate an additional * for it.


### function arrayLowerBound

```cpp linenums="1"
llvm::Optional< clang::Expr * > arrayLowerBound() const
```

The lower bound of an array slice in the first dimension. 

**Return**: llvm::Optional<clang::Expr *> Lower bound 

Finds the lower bound of an array.

All other dimension can be ignored because libomptarget only transfers continuous data. In case of a scalar (or an array which is mapped completly in the first dimension) this returns 0.


### function operator==

```cpp linenums="1"
inline bool operator==(
    const TargetRegionVariable & Other
) const
```


### function shapes

```cpp linenums="1"
inline shape_const_range shapes() const
```

Gives a range over the shape of all dimensions. 

### function variableArrayShapes

```cpp linenums="1"
inline shape_const_kind_range variableArrayShapes() const
```

Gives a range over those shape dimensions which are variable arrays. 

This is called while generating the functions argument for variable array sizes. 


### function TargetRegionVariable

```cpp linenums="1"
TargetRegionVariable(
    const clang::CapturedStmt::Capture * Capture,
    const std::map< clang::VarDecl *, clang::Expr * > & MappingLowerBounds
)
```

Construct a new Target Region Variable:: Target Region Variable object. 

**Parameters**: 

  * **Capture** 
  * **MappingLowerBounds** 


## Private Functions Documentation

### function determineShapes

```cpp linenums="1"
void determineShapes(
    clang::QualType T
)
```

Determine variable shape. 

**Parameters**: 

  * **T** Type 


Determines the shape of a varable by resolving its type.


## Private Attributes Documentation

### variable Capture

```cpp linenums="1"
const clang::CapturedStmt::Capture * Capture;
```


### variable Decl

```cpp linenums="1"
clang::VarDecl * Decl;
```


### variable VarName

```cpp linenums="1"
std::string VarName;
```


### variable BaseTypeName

```cpp linenums="1"
std::string BaseTypeName;
```

This is the base type name, i.e. 

the name of the type without pointer or array qualifiers. 


### variable Shapes

```cpp linenums="1"
std::vector< TargetRegionVariableShape > Shapes;
```


### variable NumVariableArrayDims

```cpp linenums="1"
unsigned int NumVariableArrayDims;
```


### variable OmpMappingLowerBound

```cpp linenums="1"
const std::map< clang::VarDecl *, clang::Expr * > & OmpMappingLowerBound;
```



