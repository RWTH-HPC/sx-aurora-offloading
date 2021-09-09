# DeclInfo



Records information to resolve a single declaration, including if its declared in a system header and other declaration that this declaration depends on. 


`#include <DeclResolver.h>`

## Public Functions

|                | Name           |
| -------------- | -------------- |
| | **[DeclInfo](../Classes/structDeclInfo.md#function-declinfo)**(clang::Decl * D, bool isFromSysHeader) |

## Public Attributes

|                | Name           |
| -------------- | -------------- |
| const clang::Decl * | **[Decl](../Classes/structDeclInfo.md#variable-decl)** <br>The declarations AST node itself.  |
| std::set< clang::Decl * > | **[DeclDependencies](../Classes/structDeclInfo.md#variable-decldependencies)** <br>All other declaration on which this declaration depends.  |
| bool | **[IsFromSystemHeader](../Classes/structDeclInfo.md#variable-isfromsystemheader)**  |

## Public Functions Documentation

### function DeclInfo

```cpp linenums="1"
inline DeclInfo(
    clang::Decl * D,
    bool isFromSysHeader
)
```


## Public Attributes Documentation

### variable Decl

```cpp linenums="1"
const clang::Decl * Decl;
```

The declarations AST node itself. 

### variable DeclDependencies

```cpp linenums="1"
std::set< clang::Decl * > DeclDependencies;
```

All other declaration on which this declaration depends. 

### variable IsFromSystemHeader

```cpp linenums="1"
bool IsFromSystemHeader;
```



