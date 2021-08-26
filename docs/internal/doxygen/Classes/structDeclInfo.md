# DeclInfo



Records information to resolve a single declaration, including if its declared in a system header and other declaration that this declaration depends on. 


`#include <DeclResolver.h>`

## Public Functions

|                | Name           |
| -------------- | -------------- |
| | **[DeclInfo](Classes/structDeclInfo/#function-declinfo)**(clang::Decl * D, bool isFromSysHeader) |

## Public Attributes

|                | Name           |
| -------------- | -------------- |
| const clang::Decl * | **[Decl](Classes/structDeclInfo/#variable-decl)** <br>The declarations AST node itself.  |
| std::set< clang::Decl * > | **[DeclDependencies](Classes/structDeclInfo/#variable-decldependencies)** <br>All other declaration on which this declaration depends.  |
| bool | **[IsFromSystemHeader](Classes/structDeclInfo/#variable-isfromsystemheader)**  |

## Public Functions Documentation

### function DeclInfo

```cpp
inline DeclInfo(
    clang::Decl * D,
    bool isFromSysHeader
)
```


## Public Attributes Documentation

### variable Decl

```cpp
const clang::Decl * Decl;
```

The declarations AST node itself. 

### variable DeclDependencies

```cpp
std::set< clang::Decl * > DeclDependencies;
```

All other declaration on which this declaration depends. 

### variable IsFromSystemHeader

```cpp
bool IsFromSystemHeader;
```


