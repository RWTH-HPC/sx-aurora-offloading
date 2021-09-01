# FunctionDeclResolver



Implements [DeclResolver]() for functions used in target regions.  [More...](#detailed-description)


`#include <DeclResolver.h>`

Inherits from [DeclResolver](../Classes/classDeclResolver.md)

## Public Functions

|                | Name           |
| -------------- | -------------- |
| | **[FunctionDeclResolver](../Classes/classFunctionDeclResolver.md#function-functiondeclresolver)**([TypeDeclResolver](../Classes/classTypeDeclResolver.md) & Types) |

## Private Functions

|                | Name           |
| -------------- | -------------- |
| virtual void | **[runOwnVisitor](../Classes/classFunctionDeclResolver.md#function-runownvisitor)**(clang::Decl * D, std::function< void(clang::Decl *Dep)> Fn) override<br>With this function, the resolver runs a visitor on the declaration added to find and add all declarations that the added declaration depends on and adds them to the resolver.  |
| virtual void | **[findDependDecls](../Classes/classFunctionDeclResolver.md#function-finddependdecls)**(clang::Decl * D, std::unordered_set< clang::Decl * > & UnresolvedDecls) override<br>Overrides [DeclResolver::findDependDecls]() to also find types required by this function.  |

## Private Attributes

|                | Name           |
| -------------- | -------------- |
| [TypeDeclResolver](../Classes/classTypeDeclResolver.md) & | **[Types](../Classes/classFunctionDeclResolver.md#variable-types)**  |

## Additional inherited members

**Public Functions inherited from [DeclResolver](../Classes/classDeclResolver.md)**

|                | Name           |
| -------------- | -------------- |
| virtual | **[~DeclResolver](../Classes/classDeclResolver.md#function-~declresolver)**() =0 |
| void | **[addDecl](../Classes/classDeclResolver.md#function-adddecl)**(clang::Decl * D)<br>Records a Decl and automatically adds all Decls that this Decl depends on.  |
| void | **[orderAndAddFragments](../Classes/classDeclResolver.md#function-orderandaddfragments)**([TargetCode](../Classes/classTargetCode.md) & TC)<br>Creates a [TargetCodeFragment](../Classes/classTargetCodeFragment.md) for each recorded Decl and adds them to the [TargetCode](../Classes/classTargetCode.md) object in the correct order.  |

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


## Detailed Description

```cpp linenums="1"
class FunctionDeclResolver;
```

Implements [DeclResolver]() for functions used in target regions.

Does also search for additional types in the functions found and adds them to a [TypeDeclResolver](../Classes/classTypeDeclResolver.md) instance.

## Public Functions Documentation

### function FunctionDeclResolver

```cpp linenums="1"
inline FunctionDeclResolver(
    TypeDeclResolver & Types
)
```


## Private Functions Documentation

### function runOwnVisitor

```cpp linenums="1"
virtual void runOwnVisitor(
    clang::Decl * D,
    std::function< void(clang::Decl *Dep)> Fn
) override
```

With this function, the resolver runs a visitor on the declaration added to find and add all declarations that the added declaration depends on and adds them to the resolver.

**Reimplements**: [DeclResolver::runOwnVisitor](../Classes/classDeclResolver.md#function-runownvisitor)


### function findDependDecls

```cpp linenums="1"
virtual void findDependDecls(
    clang::Decl * D,
    std::unordered_set< clang::Decl * > & UnresolvedDecls
) override
```

Overrides [DeclResolver::findDependDecls]() to also find types required by this function.

**Reimplements**: [DeclResolver::findDependDecls](../Classes/classDeclResolver.md#function-finddependdecls)


## Private Attributes Documentation

### variable Types

```cpp linenums="1"
TypeDeclResolver & Types;
```


