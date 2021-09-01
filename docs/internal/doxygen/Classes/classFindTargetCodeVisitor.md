# FindTargetCodeVisitor



Traverses the AST to find target and process target regions and function and variables that are annotated by an 'omp declare target' target pragma.


`#include <Visitors.h>`

Inherits from clang::RecursiveASTVisitor< FindTargetCodeVisitor >

## Public Functions

|                | Name           |
| -------------- | -------------- |
| | **[FindTargetCodeVisitor](../Classes/classFindTargetCodeVisitor.md#function-findtargetcodevisitor)**([TargetCode](../Classes/classTargetCode.md) & Code, [TypeDeclResolver](../Classes/classTypeDeclResolver.md) & Types, [FunctionDeclResolver](../Classes/classFunctionDeclResolver.md) & Functions, clang::ASTContext & Context) |
| bool | **[TraverseDecl](../Classes/classFindTargetCodeVisitor.md#function-traversedecl)**(clang::Decl * D) |
| bool | **[VisitStmt](../Classes/classFindTargetCodeVisitor.md#function-visitstmt)**(clang::Stmt * S) |
| bool | **[VisitDecl](../Classes/classFindTargetCodeVisitor.md#function-visitdecl)**(clang::Decl * D) |

## Private Functions

|                | Name           |
| -------------- | -------------- |
| bool | **[processTargetRegion](../Classes/classFindTargetCodeVisitor.md#function-processtargetregion)**(clang::OMPExecutableDirective * TargetDirective)<br>Extracts the necessary information about the target region from the AST, such as captured variables and relevant OpenMP clauses, and adds an [TargetCodeRegion](../Classes/classTargetCodeRegion.md) to the [TargetCode](../Classes/classTargetCode.md) instance.  |
| void | **[addTargetRegionArgs](../Classes/classFindTargetCodeVisitor.md#function-addtargetregionargs)**(clang::CapturedStmt * S, clang::OMPExecutableDirective * TargetDirective, std::shared_ptr< [TargetCodeRegion](../Classes/classTargetCodeRegion.md) > TCR)<br>Finds and adds all variables required by the target regions as arguments to the generated function.  |

## Private Attributes

|                | Name           |
| -------------- | -------------- |
| clang::ASTContext & | **[Context](../Classes/classFindTargetCodeVisitor.md#variable-context)**  |
| [TargetCode](../Classes/classTargetCode.md) & | **[TargetCodeInfo](../Classes/classFindTargetCodeVisitor.md#variable-targetcodeinfo)** <br>The collection where target regions and other code is added to.  |
| [DiscoverTypesInDeclVisitor](../Classes/classDiscoverTypesInDeclVisitor.md) | **[DiscoverTypeVisitor](../Classes/classFindTargetCodeVisitor.md#variable-discovertypevisitor)** <br>A Visitor to find references to the types required by the target code.  |
| [DiscoverFunctionsInDeclVisitor](../Classes/classDiscoverFunctionsInDeclVisitor.md) | **[DiscoverFunctionVisitor](../Classes/classFindTargetCodeVisitor.md#variable-discoverfunctionvisitor)** <br>A Visitor to find references to all functions required by the target code.  |
| [FunctionDeclResolver](../Classes/classFunctionDeclResolver.md) & | **[Functions](../Classes/classFindTargetCodeVisitor.md#variable-functions)** <br>Collection of all functions referenced and required by target code (and referenced by other required functions).  |
| [FindDeclRefExprVisitor](../Classes/classFindDeclRefExprVisitor.md) | **[FindDeclRefVisitor](../Classes/classFindTargetCodeVisitor.md#variable-finddeclrefvisitor)**  |
| std::stack< clang::FunctionDecl * > | **[LastVisitedFuncDecl](../Classes/classFindTargetCodeVisitor.md#variable-lastvisitedfuncdecl)** <br>The last function the visitor traversed.  |
| std::unordered_set< std::string > | **[FuncDeclWithoutBody](../Classes/classFindTargetCodeVisitor.md#variable-funcdeclwithoutbody)** <br>Function with 'omp declare target' pragma, for which the visitor has not yet found a body.  |

## Public Functions Documentation

### function FindTargetCodeVisitor

```cpp linenums="1"
inline FindTargetCodeVisitor(
    TargetCode & Code,
    TypeDeclResolver & Types,
    FunctionDeclResolver & Functions,
    clang::ASTContext & Context
)
```


### function TraverseDecl

```cpp linenums="1"
bool TraverseDecl(
    clang::Decl * D
)
```


### function VisitStmt

```cpp linenums="1"
bool VisitStmt(
    clang::Stmt * S
)
```


### function VisitDecl

```cpp linenums="1"
bool VisitDecl(
    clang::Decl * D
)
```


## Private Functions Documentation

### function processTargetRegion

```cpp linenums="1"
bool processTargetRegion(
    clang::OMPExecutableDirective * TargetDirective
)
```

Extracts the necessary information about the target region from the AST, such as captured variables and relevant OpenMP clauses, and adds an [TargetCodeRegion](../Classes/classTargetCodeRegion.md) to the [TargetCode](../Classes/classTargetCode.md) instance.

### function addTargetRegionArgs

```cpp linenums="1"
void addTargetRegionArgs(
    clang::CapturedStmt * S,
    clang::OMPExecutableDirective * TargetDirective,
    std::shared_ptr< TargetCodeRegion > TCR
)
```

Finds and adds all variables required by the target regions as arguments to the generated function.

## Private Attributes Documentation

### variable Context

```cpp linenums="1"
clang::ASTContext & Context;
```


### variable TargetCodeInfo

```cpp linenums="1"
TargetCode & TargetCodeInfo;
```

The collection where target regions and other code is added to.

### variable DiscoverTypeVisitor

```cpp linenums="1"
DiscoverTypesInDeclVisitor DiscoverTypeVisitor;
```

A Visitor to find references to the types required by the target code.

### variable DiscoverFunctionVisitor

```cpp linenums="1"
DiscoverFunctionsInDeclVisitor DiscoverFunctionVisitor;
```

A Visitor to find references to all functions required by the target code.

### variable Functions

```cpp linenums="1"
FunctionDeclResolver & Functions;
```

Collection of all functions referenced and required by target code (and referenced by other required functions).

### variable FindDeclRefVisitor

```cpp linenums="1"
FindDeclRefExprVisitor FindDeclRefVisitor;
```


### variable LastVisitedFuncDecl

```cpp linenums="1"
std::stack< clang::FunctionDecl * > LastVisitedFuncDecl;
```

The last function the visitor traversed.

This is stored to be able to later compute the function name for the target region.


### variable FuncDeclWithoutBody

```cpp linenums="1"
std::unordered_set< std::string > FuncDeclWithoutBody;
```

Function with 'omp declare target' pragma, for which the visitor has not yet found a body.

