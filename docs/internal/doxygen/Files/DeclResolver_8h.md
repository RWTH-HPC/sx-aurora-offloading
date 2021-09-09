# src/DeclResolver.h

This file implements the class [DeclResolver](../Classes/classDeclResolver.md) which is used to record and order types and functions in the input code that are required by the target regions. 

## Namespaces

| Name           |
| -------------- |
| **[clang](../Namespaces/namespaceclang.md)**  |

## Classes

|                | Name           |
| -------------- | -------------- |
| struct | **[DeclInfo](../Classes/structDeclInfo.md)** <br>Records information to resolve a single declaration, including if its declared in a system header and other declaration that this declaration depends on.  |
| class | **[DeclResolver](../Classes/classDeclResolver.md)** <br>Records, orders and finds the dependencies of Decls (TypeDecls or FunctionDecls)  |
| class | **[TypeDeclResolver](../Classes/classTypeDeclResolver.md)** <br>Implements [DeclResolver]() for types (typedefs, structs enums) used in target regions.  |
| class | **[FunctionDeclResolver](../Classes/classFunctionDeclResolver.md)** <br>Implements [DeclResolver]() for functions used in target regions.  |

## Types

|                | Name           |
| -------------- | -------------- |
| using std::map< clang::Decl *, [DeclInfo](../Classes/structDeclInfo.md) > | **[DeclMap](../Files/DeclResolver_8h.md#using-declmap)**  |

## Functions

|                | Name           |
| -------------- | -------------- |
| llvm::Optional< std::string > | **[getSystemHeaderForDecl](../Files/DeclResolver_8h.md#function-getsystemheaderfordecl)**(const clang::Decl * D) |

## Types Documentation

### using DeclMap

```cpp linenums="1"
using DeclMap =  std::map<clang::Decl *, DeclInfo>;
```



## Functions Documentation

### function getSystemHeaderForDecl

```cpp linenums="1"
llvm::Optional< std::string > getSystemHeaderForDecl(
    const clang::Decl * D
)
```




## Source code
```cpp linenums="1"
//===-- sotoc/src/DeclResolver.h -----------------------------------------===//
//
//                     The LLVM Compiler Infrastructure
//
// This file is distributed under the University of Illinois Open Source
// License. See LICENSE.TXT for details.
//
//===----------------------------------------------------------------------===//
//===----------------------------------------------------------------------===//
#pragma once

#include <map>
#include <set>
#include <stack>
#include <unordered_set>

llvm::Optional<std::string> getSystemHeaderForDecl(const clang::Decl *D);

namespace clang {
class Decl;
}

class TargetCode;

struct DeclInfo {
  const clang::Decl *Decl;
  std::set<clang::Decl *> DeclDependencies;
  // std::set<clang::Decl *> ForwardDecls;  // for the moment we solve this
  // differently
  bool IsFromSystemHeader;

  DeclInfo(clang::Decl *D, bool isFromSysHeader)
      : Decl(D), IsFromSystemHeader(isFromSysHeader){};
};

using DeclMap = std::map<clang::Decl *, DeclInfo>;

class DeclResolver {
  DeclMap AllDecls;
  std::set<clang::Decl *> NonDependentDecls;
  std::set<std::string> RequiredSystemHeaders;

public:
  virtual ~DeclResolver() = 0;
  void addDecl(clang::Decl *D);
  void orderAndAddFragments(TargetCode &TC);

protected:
  virtual void runOwnVisitor(clang::Decl *D,
                             std::function<void(clang::Decl *Dep)> Fn) = 0;
  virtual void
  findDependDecls(clang::Decl *D,
                  std::unordered_set<clang::Decl *> &UnresolvedDecls);

private:
  void topoSort(std::stack<clang::Decl *> &q);
  void topoSortUtil(std::stack<clang::Decl *> &q,
                    std::map<clang::Decl *, bool> &visited, clang::Decl *D);
};

class TypeDeclResolver : public DeclResolver {
private:
  void runOwnVisitor(clang::Decl *D,
                     std::function<void(clang::Decl *Dep)> Fn) override;
};

class FunctionDeclResolver : public DeclResolver {
  TypeDeclResolver &Types;

public:
  FunctionDeclResolver(TypeDeclResolver &Types) : Types(Types){};

private:
  void runOwnVisitor(clang::Decl *D,
                     std::function<void(clang::Decl *Dep)> Fn) override;
  void
  findDependDecls(clang::Decl *D,
                  std::unordered_set<clang::Decl *> &UnresolvedDecls) override;
};
```



