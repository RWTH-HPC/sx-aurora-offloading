# TypeDeclResolver



Implements [DeclResolver]() for types (typedefs, structs enums) used in target regions. 


`#include <DeclResolver.h>`

Inherits from [DeclResolver](Classes/classDeclResolver.md)

## Additional inherited members

**Public Functions inherited from [DeclResolver](Classes/classDeclResolver.md)**

|                | Name           |
| -------------- | -------------- |
| virtual | **[~DeclResolver](Classes/classDeclResolver.md#function-~declresolver)**() =0 |
| void | **[addDecl](Classes/classDeclResolver.md#function-adddecl)**(clang::Decl * D)<br>Records a Decl and automatically adds all Decls that this Decl depends on.  |
| void | **[orderAndAddFragments](Classes/classDeclResolver.md#function-orderandaddfragments)**([TargetCode](Classes/classTargetCode.md) & TC)<br>Creates a [TargetCodeFragment](Classes/classTargetCodeFragment.md) for each recorded Decl and adds them to the [TargetCode](Classes/classTargetCode.md) object in the correct order.  |

**Protected Functions inherited from [DeclResolver](Classes/classDeclResolver.md)**

|                | Name           |
| -------------- | -------------- |
| virtual void | **[findDependDecls](Classes/classDeclResolver.md#function-finddependdecls)**(clang::Decl * D, std::unordered_set< clang::Decl * > & UnresolvedDecls)<br>This function uses a visitor to find references to other declarations in the declaration being added.  |


