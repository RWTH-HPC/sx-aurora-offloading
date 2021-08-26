# TargetRegionVariable::shape_const_kind_iterator



Iterator which acts as a filter over std::vector<TargetRegionVariableShape>::const_iterator (the base_iter) which only passes on [TargetRegionVariableShape](Classes/classTargetRegionVariableShape.md) of the kind specified in [Kind](). 


`#include <TargetRegionVariable.h>`

## Public Types

|                | Name           |
| -------------- | -------------- |
| using std::vector< [TargetRegionVariableShape](Classes/classTargetRegionVariableShape.md) >::const_iterator | **[base_iter](Classes/classTargetRegionVariable_1_1shape__const__kind__iterator.md#using-base_iter)**  |
| using [TargetRegionVariableShape](Classes/classTargetRegionVariableShape.md) | **[value_type](Classes/classTargetRegionVariable_1_1shape__const__kind__iterator.md#using-value_type)**  |
| using const [TargetRegionVariableShape](Classes/classTargetRegionVariableShape.md) & | **[reference](Classes/classTargetRegionVariable_1_1shape__const__kind__iterator.md#using-reference)**  |
| using const [TargetRegionVariableShape](Classes/classTargetRegionVariableShape.md) * | **[pointer](Classes/classTargetRegionVariable_1_1shape__const__kind__iterator.md#using-pointer)**  |
| using std::forward_iterator_tag | **[iterator_category](Classes/classTargetRegionVariable_1_1shape__const__kind__iterator.md#using-iterator_category)**  |
| using std::ptrdiff_t | **[difference_type](Classes/classTargetRegionVariable_1_1shape__const__kind__iterator.md#using-difference_type)**  |
| using [TargetRegionVariableShape::ShapeKind](Classes/classTargetRegionVariableShape.md#enum-shapekind) | **[ShapeKind](Classes/classTargetRegionVariable_1_1shape__const__kind__iterator.md#using-shapekind)**  |

## Public Functions

|                | Name           |
| -------------- | -------------- |
| | **[shape_const_kind_iterator](Classes/classTargetRegionVariable_1_1shape__const__kind__iterator.md#function-shape_const_kind_iterator)**() |
| | **[shape_const_kind_iterator](Classes/classTargetRegionVariable_1_1shape__const__kind__iterator.md#function-shape_const_kind_iterator)**([ShapeKind](Classes/classTargetRegionVariableShape.md#enum-shapekind) Kind, [base_iter](Classes/classTargetRegionVariable_1_1shape__const__kind__iterator.md#using-base_iter) I)<br>Explicitly constructs an iterator from the base_iter- Both the start and end of the iterator will be set to the same paramter `I`.  |
| | **[shape_const_kind_iterator](Classes/classTargetRegionVariable_1_1shape__const__kind__iterator.md#function-shape_const_kind_iterator)**([ShapeKind](Classes/classTargetRegionVariableShape.md#enum-shapekind) Kind, [base_iter](Classes/classTargetRegionVariable_1_1shape__const__kind__iterator.md#using-base_iter) I, [base_iter](Classes/classTargetRegionVariable_1_1shape__const__kind__iterator.md#using-base_iter) End)<br>Explicitly constructs an iterator from cbegin() and cend() of base_iter.  |
| [shape_const_kind_iterator](Classes/classTargetRegionVariable_1_1shape__const__kind__iterator.md) & | **[operator++](Classes/classTargetRegionVariable_1_1shape__const__kind__iterator.md#function-operator++)**() |
| [shape_const_kind_iterator](Classes/classTargetRegionVariable_1_1shape__const__kind__iterator.md) | **[operator++](Classes/classTargetRegionVariable_1_1shape__const__kind__iterator.md#function-operator++)**(int ) |
| [reference](Classes/classTargetRegionVariable_1_1shape__const__kind__iterator.md#using-reference) | **[operator*](Classes/classTargetRegionVariable_1_1shape__const__kind__iterator.md#function-operator*)**() const |
| [pointer](Classes/classTargetRegionVariable_1_1shape__const__kind__iterator.md#using-pointer) | **[operator->](Classes/classTargetRegionVariable_1_1shape__const__kind__iterator.md#function-operator->)**() |

## Friends

|                | Name           |
| -------------- | -------------- |
| bool | **[operator==](Classes/classTargetRegionVariable_1_1shape__const__kind__iterator.md#friend-operator==)**([shape_const_kind_iterator](Classes/classTargetRegionVariable_1_1shape__const__kind__iterator.md) X, [shape_const_kind_iterator](Classes/classTargetRegionVariable_1_1shape__const__kind__iterator.md) Y)  |
| bool | **[operator!=](Classes/classTargetRegionVariable_1_1shape__const__kind__iterator.md#friend-operator!=)**([shape_const_kind_iterator](Classes/classTargetRegionVariable_1_1shape__const__kind__iterator.md) X, [shape_const_kind_iterator](Classes/classTargetRegionVariable_1_1shape__const__kind__iterator.md) Y)  |

## Public Types Documentation

### using base_iter

```cpp
using TargetRegionVariable::shape_const_kind_iterator::base_iter =  std::vector<TargetRegionVariableShape>::const_iterator;
```


### using value_type

```cpp
using TargetRegionVariable::shape_const_kind_iterator::value_type =  TargetRegionVariableShape;
```


### using reference

```cpp
using TargetRegionVariable::shape_const_kind_iterator::reference =  const TargetRegionVariableShape &;
```


### using pointer

```cpp
using TargetRegionVariable::shape_const_kind_iterator::pointer =  const TargetRegionVariableShape *;
```


### using iterator_category

```cpp
using TargetRegionVariable::shape_const_kind_iterator::iterator_category =  std::forward_iterator_tag;
```


### using difference_type

```cpp
using TargetRegionVariable::shape_const_kind_iterator::difference_type =  std::ptrdiff_t;
```


### using ShapeKind

```cpp
using TargetRegionVariable::shape_const_kind_iterator::ShapeKind =  TargetRegionVariableShape::ShapeKind;
```


## Public Functions Documentation

### function shape_const_kind_iterator

```cpp
shape_const_kind_iterator()
```


### function shape_const_kind_iterator

```cpp
inline explicit shape_const_kind_iterator(
    ShapeKind Kind,
    base_iter I
)
```

Explicitly constructs an iterator from the base_iter- Both the start and end of the iterator will be set to the same paramter `I`. 

Use this to construct an end() iterator from std::vector<>::cend(). 


### function shape_const_kind_iterator

```cpp
inline explicit shape_const_kind_iterator(
    ShapeKind Kind,
    base_iter I,
    base_iter End
)
```

Explicitly constructs an iterator from cbegin() and cend() of base_iter. 

Use this to construct a begin() from std::vector<>::cbegin() and std::vector<>::cend(). The iterator needs to operate on the base_iter at construction to ensure that a non-empty vector which does not contain elements of the right [Kind](Classes/classTargetRegionVariable_1_1shape__const__kind__iterator.md#variable-kind) is handled correctly. 


### function operator++

```cpp
inline shape_const_kind_iterator & operator++()
```


### function operator++

```cpp
inline shape_const_kind_iterator operator++(
    int 
)
```


### function operator*

```cpp
inline reference operator*() const
```


### function operator->

```cpp
inline pointer operator->()
```


## Friends

### friend operator==

```cpp
friend bool operator==(
    shape_const_kind_iterator X,

    shape_const_kind_iterator Y
);
```


### friend operator!=

```cpp
friend bool operator!=(
    shape_const_kind_iterator X,

    shape_const_kind_iterator Y
);
```


