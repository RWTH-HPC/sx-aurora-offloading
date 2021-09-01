# DeclResolver



Records, orders and finds the dependencies of Decls (TypeDecls or FunctionDecls)


`#include <DeclResolver.h>`

Inherited by [FunctionDeclResolver](../Classes/classFunctionDeclResolver.md), [TypeDeclResolver](../Classes/classTypeDeclResolver.md)

## Public Functions

|                | Name           |
| -------------- | -------------- |
| virtual | **[~DeclResolver](../Classes/classDeclResolver.md#function-~declresolver)**() =0 |
| void | **[addDecl](../Classes/classDeclResolver.md#function-adddecl)**(clang::Decl * D)<br>Records a Decl and automatically adds all Decls that this Decl depends on.  |
| void | **[orderAndAddFragments](../Classes/classDeclResolver.md#function-orderandaddfragments)**([TargetCode](../Classes/classTargetCode.md) & TC)<br>Creates a [TargetCodeFragment](../Classes/classTargetCodeFragment.md) for each recorded Decl and adds them to the [TargetCode](../Classes/classTargetCode.md) object in the correct order.  |

## Protected Functions

|                | Name           |
| -------------- | -------------- |
| virtual void | **[runOwnVisitor](../Classes/classDeclResolver.md#function-runownvisitor)**(clang::Decl * D, std::function< void(clang::Decl *Dep)> Fn) =0<br>With this function, the resolver runs a visitor on the declaration added to find and add all declarations that the added declaration depends on and adds them to the resolver.  |
| virtual void | **[findDependDecls](../Classes/classDeclResolver.md#function-finddependdecls)**(clang::Decl * D, std::unordered_set< clang::Decl * > & UnresolvedDecls)<br>This function uses a visitor to find references to other declarations in the declaration being added.  |

## Private Functions

|                | Name           |
| -------------- | -------------- |
| void | **[topoSort](../Classes/classDeclResolver.md#function-toposort)**(std::stack< clang::Decl * > & q)<br>This functions does a topological sorting on the dependency graph of all Decls recorded into this object by calling [addDecl](../Classes/classDeclResolver.md#function-adddecl).  |
| void | **[topoSortUtil](../Classes/classDeclResolver.md#function-toposortutil)**(std::stack< clang::Decl * > & q, std::map< clang::Decl *, bool > & visited, clang::Decl * D)<br>Helper function for [topoSort](../Classes/classDeclResolver.md#function-toposort), to do an recursive DFS.  |

## Private Attributes

|                | Name           |
| -------------- | -------------- |
| [DeclMap](../Files/DeclResolver_8h.md#using-declmap) | **[AllDecls](../Classes/classDeclResolver.md#variable-alldecls)** <br>Records all declarations added to the resolver.  |
| std::set< clang::Decl * > | **[NonDependentDecls](../Classes/classDeclResolver.md#variable-nondependentdecls)** <br>All declarations which do not depend on other declarations.  |
| std::set< std::string > | **[RequiredSystemHeaders](../Classes/classDeclResolver.md#variable-requiredsystemheaders)** <br>When a declaration is inside a system header, that header is recorded here instead of the declaratoin.  |

## Public Functions Documentation

### function ~DeclResolver

```cpp linenums="1"
virtual ~DeclResolver() =0
```


### function addDecl

```cpp linenums="1"
void addDecl(
    clang::Decl * D
)
```

Records a Decl and automatically adds all Decls that this Decl depends on.

**Parameters**:

  * **D** the Decl to be added to the resolver.


### function orderAndAddFragments

```cpp linenums="1"
void orderAndAddFragments(
    TargetCode & TC
)
```

Creates a [TargetCodeFragment](../Classes/classTargetCodeFragment.md) for each recorded Decl and adds them to the [TargetCode](../Classes/classTargetCode.md) object in the correct order.

**Parameters**:

  * **TC** the [TargetCode](../Classes/classTargetCode.md) object, the fragments will be added to.


## Protected Functions Documentation

### function runOwnVisitor

```cpp linenums="1"
virtual void runOwnVisitor(
    clang::Decl * D,
    std::function< void(clang::Decl *Dep)> Fn
) =0
```

With this function, the resolver runs a visitor on the declaration added to find and add all declarations that the added declaration depends on and adds them to the resolver.

**Reimplemented by**: [TypeDeclResolver::runOwnVisitor](../Classes/classTypeDeclResolver.md#function-runownvisitor), [FunctionDeclResolver::runOwnVisitor](../Classes/classFunctionDeclResolver.md#function-runownvisitor)


### function findDependDecls

```cpp linenums="1"
virtual void findDependDecls(
    clang::Decl * D,
    std::unordered_set< clang::Decl * > & UnresolvedDecls
)
```

This function uses a visitor to find references to other declarations in the declaration being added.

**Parameters**:

  * **D** the declaration that was added via [addDecl](../Classes/classDeclResolver.md#function-adddecl).
  * **UnresolvedDecls** a set of declarations which D depends on and which are currently unresolved.


**Reimplemented by**: [FunctionDeclResolver::findDependDecls](../Classes/classFunctionDeclResolver.md#function-finddependdecls)


If the declaration being added references other declarations outside the standard library, we need to add those declaration to the target code too.


## Private Functions Documentation

### function topoSort

```cpp linenums="1"
void topoSort(
    std::stack< clang::Decl * > & q
)
```

This functions does a topological sorting on the dependency graph of all Decls recorded into this object by calling [addDecl](../Classes/classDeclResolver.md#function-adddecl).

**Parameters**:

  * **q** an queue where the ordered Decls are save to.


This method uses an DFS approach to be able to deal with possible cycles.


### function topoSortUtil

```cpp linenums="1"
void topoSortUtil(
    std::stack< clang::Decl * > & q,
    std::map< clang::Decl *, bool > & visited,
    clang::Decl * D
)
```

Helper function for [topoSort](../Classes/classDeclResolver.md#function-toposort), to do an recursive DFS.

## Private Attributes Documentation

### variable AllDecls

```cpp linenums="1"
DeclMap AllDecls;
```

Records all declarations added to the resolver.

### variable NonDependentDecls

```cpp linenums="1"
std::set< clang::Decl * > NonDependentDecls;
```

All declarations which do not depend on other declarations.

### variable RequiredSystemHeaders

```cpp linenums="1"
std::set< std::string > RequiredSystemHeaders;
```

When a declaration is inside a system header, that header is recorded here instead of the declaratoin.

