# FunctionDeclResolver



Implements [DeclResolver]() for functions used in target regions.  [More...](#detailed-description)


`#include <DeclResolver.h>`

Inherits from [DeclResolver](Classes/classDeclResolver/)

## Public Functions

|                | Name           |
| -------------- | -------------- |
| | **[FunctionDeclResolver](Classes/classFunctionDeclResolver/#function-functiondeclresolver)**([TypeDeclResolver](Classes/classTypeDeclResolver/) & Types) |

## Additional inherited members

**Public Functions inherited from [DeclResolver](Classes/classDeclResolver/)**

|                | Name           |
| -------------- | -------------- |
| virtual | **[~DeclResolver](Classes/classDeclResolver/#function-~declresolver)**() =0 |
| void | **[addDecl](Classes/classDeclResolver/#function-adddecl)**(clang::Decl * D)<br>Records a Decl and automatically adds all Decls that this Decl depends on.  |
| void | **[orderAndAddFragments](Classes/classDeclResolver/#function-orderandaddfragments)**([TargetCode](Classes/classTargetCode/) & TC)<br>Creates a [TargetCodeFragment](Classes/classTargetCodeFragment/) for each recorded Decl and adds them to the [TargetCode](Classes/classTargetCode/) object in the correct order.  |


## Detailed Description

```cpp
class FunctionDeclResolver;
```

Implements [DeclResolver]() for functions used in target regions. 

Does also search for additional types in the functions found and adds them to a [TypeDeclResolver](Classes/classTypeDeclResolver/) instance. 

## Public Functions Documentation

### function FunctionDeclResolver

```cpp
inline FunctionDeclResolver(
    TypeDeclResolver & Types
)
```


