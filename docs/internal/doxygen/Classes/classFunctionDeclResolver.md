# FunctionDeclResolver



Implements [DeclResolver]() for functions used in target regions.  [More...](#detailed-description)


`#include <DeclResolver.h>`

Inherits from [DeclResolver](Classes/classDeclResolver.md)

## Public Functions

|                | Name           |
| -------------- | -------------- |
| | **[FunctionDeclResolver](Classes/classFunctionDeclResolver.md#function-functiondeclresolver)**([TypeDeclResolver](Classes/classTypeDeclResolver.md) & Types) |

## Additional inherited members

**Public Functions inherited from [DeclResolver](Classes/classDeclResolver.md)**

|                | Name           |
| -------------- | -------------- |
| virtual | **[~DeclResolver](Classes/classDeclResolver.md#function-~declresolver)**() =0 |
| void | **[addDecl](Classes/classDeclResolver.md#function-adddecl)**(clang::Decl * D)<br>Records a Decl and automatically adds all Decls that this Decl depends on.  |
| void | **[orderAndAddFragments](Classes/classDeclResolver.md#function-orderandaddfragments)**([TargetCode](Classes/classTargetCode.md) & TC)<br>Creates a [TargetCodeFragment](Classes/classTargetCodeFragment.md) for each recorded Decl and adds them to the [TargetCode](Classes/classTargetCode.md) object in the correct order.  |


## Detailed Description

```cpp
class FunctionDeclResolver;
```

Implements [DeclResolver]() for functions used in target regions. 

Does also search for additional types in the functions found and adds them to a [TypeDeclResolver](Classes/classTypeDeclResolver.md) instance. 

## Public Functions Documentation

### function FunctionDeclResolver

```cpp
inline FunctionDeclResolver(
    TypeDeclResolver & Types
)
```


