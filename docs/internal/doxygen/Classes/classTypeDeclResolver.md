# TypeDeclResolver



Implements [DeclResolver]() for types (typedefs, structs enums) used in target regions. 


`#include <DeclResolver.h>`

Inherits from [DeclResolver](Classes/classDeclResolver/)

## Additional inherited members

**Public Functions inherited from [DeclResolver](Classes/classDeclResolver/)**

|                | Name           |
| -------------- | -------------- |
| virtual | **[~DeclResolver](Classes/classDeclResolver/#function-~declresolver)**() =0 |
| void | **[addDecl](Classes/classDeclResolver/#function-adddecl)**(clang::Decl * D)<br>Records a Decl and automatically adds all Decls that this Decl depends on.  |
| void | **[orderAndAddFragments](Classes/classDeclResolver/#function-orderandaddfragments)**([TargetCode](Classes/classTargetCode/) & TC)<br>Creates a [TargetCodeFragment](Classes/classTargetCodeFragment/) for each recorded Decl and adds them to the [TargetCode](Classes/classTargetCode/) object in the correct order.  |

**Protected Functions inherited from [DeclResolver](Classes/classDeclResolver/)**

|                | Name           |
| -------------- | -------------- |
| virtual void | **[findDependDecls](Classes/classDeclResolver/#function-finddependdecls)**(clang::Decl * D, std::unordered_set< clang::Decl * > & UnresolvedDecls)<br>This function uses a visitor to find references to other declarations in the declaration being added.  |


