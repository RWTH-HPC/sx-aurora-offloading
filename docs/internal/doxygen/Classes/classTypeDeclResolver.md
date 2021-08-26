# TypeDeclResolver



Implements [DeclResolver]() for types (typedefs, structs enums) used in target regions. 


`#include <DeclResolver.h>`

Inherits from [DeclResolver](../Classes/classDeclResolver.md)

## Private Functions

|                | Name           |
| -------------- | -------------- |
| virtual void | **[runOwnVisitor](../Classes/classTypeDeclResolver.md#function-runownvisitor)**(clang::Decl * D, std::function< void(clang::Decl *Dep)> Fn) override<br>With this function, the resolver runs a visitor on the declaration added to find and add all declarations that the added declaration depends on and adds them to the resolver.  |

## Additional inherited members

**Public Functions inherited from [DeclResolver](../Classes/classDeclResolver.md)**

|                | Name           |
| -------------- | -------------- |
| virtual | **[~DeclResolver](../Classes/classDeclResolver.md#function-~declresolver)**() =0 |
| void | **[addDecl](../Classes/classDeclResolver.md#function-adddecl)**(clang::Decl * D)<br>Records a Decl and automatically adds all Decls that this Decl depends on.  |
| void | **[orderAndAddFragments](../Classes/classDeclResolver.md#function-orderandaddfragments)**([TargetCode](../Classes/classTargetCode.md) & TC)<br>Creates a [TargetCodeFragment](../Classes/classTargetCodeFragment.md) for each recorded Decl and adds them to the [TargetCode](../Classes/classTargetCode.md) object in the correct order.  |

**Protected Functions inherited from [DeclResolver](../Classes/classDeclResolver.md)**

|                | Name           |
| -------------- | -------------- |
| virtual void | **[findDependDecls](../Classes/classDeclResolver.md#function-finddependdecls)**(clang::Decl * D, std::unordered_set< clang::Decl * > & UnresolvedDecls)<br>This function uses a visitor to find references to other declarations in the declaration being added.  |

**Private Functions inherited from [DeclResolver](../Classes/classDeclResolver.md)**

|                | Name           |
| -------------- | -------------- |
| void | **[topoSort](../Classes/classDeclResolver.md#function-toposort)**(std::stack< clang::Decl * > & q)<br>This functions does a topological sorting on the dependency graph of all Decls recorded into this object by calling [addDecl](../Classes/classDeclResolver.md#function-adddecl).  |
| void | **[topoSortUtil](../Classes/classDeclResolver.md#function-toposortutil)**(std::stack< clang::Decl * > & q, std::map< clang::Decl *, bool > & visited, clang::Decl * D)<br>Helper function for [topoSort](../Classes/classDeclResolver.md#function-toposort), to do an recursive DFS.  |

**Private Attributes inherited from [DeclResolver](../Classes/classDeclResolver.md)**

|                | Name           |
| -------------- | -------------- |
| [DeclMap](../Files/DeclResolver_8h.md#using-declmap) | **[AllDecls](../Classes/classDeclResolver.md#variable-alldecls)** <br>Records all declarations added to the resolver.  |
| std::set< clang::Decl * > | **[NonDependentDecls](../Classes/classDeclResolver.md#variable-nondependentdecls)** <br>All declarations which do not depend on other declarations.  |
| std::set< std::string > | **[RequiredSystemHeaders](../Classes/classDeclResolver.md#variable-requiredsystemheaders)** <br>When a declaration is inside a system header, that header is recorded here instead of the declaratoin.  |


## Private Functions Documentation

### function runOwnVisitor

```cpp
virtual void runOwnVisitor(
    clang::Decl * D,
    std::function< void(clang::Decl *Dep)> Fn
) override
```

With this function, the resolver runs a visitor on the declaration added to find and add all declarations that the added declaration depends on and adds them to the resolver. 

**Reimplements**: [DeclResolver::runOwnVisitor](../Classes/classDeclResolver.md#function-runownvisitor)


