# src/Visitors.h



## Namespaces

| Name           |
| -------------- |
| **[clang](../Namespaces/namespaceclang.md)**  |

## Classes

|                | Name           |
| -------------- | -------------- |
| class | **[DiscoverTypesInDeclVisitor](../Classes/classDiscoverTypesInDeclVisitor.md)** <br>Traverses (parts of) the AST to find DeclRefExpr that refer to types that need to be present for that part of the AST to compile correctly.  |
| class | **[DiscoverFunctionsInDeclVisitor](../Classes/classDiscoverFunctionsInDeclVisitor.md)** <br>Traverses (parts of) the AST to find DeclRefExpr that refer to functions that need to be present for that part of the AST to compile correctly.  |
| class | **[FindDeclRefExprVisitor](../Classes/classFindDeclRefExprVisitor.md)**  |
| class | **[FindLoopStmtVisitor](../Classes/classFindLoopStmtVisitor.md)**  |
| class | **[FindTargetCodeVisitor](../Classes/classFindTargetCodeVisitor.md)** <br>Traverses the AST to find target and process target regions and function and variables that are annotated by an 'omp declare target' target pragma.  |
| class | **[FindArraySectionVisitor](../Classes/classFindArraySectionVisitor.md)**  |
| class | **[FindPrivateVariablesVisitor](../Classes/classFindPrivateVariablesVisitor.md)**  |




## Source code
```cpp linenums="1"
//===-- sotoc/src/Visitor.h -----------------------------------------------===//
//
//                     The LLVM Compiler Infrastructure
//
// This file is distributed under the University of Illinois Open Source
// License. See LICENSE.TXT for details.
//
//===----------------------------------------------------------------------===//

#pragma once

#include <unordered_set>

#include "DeclResolver.h"
#include "clang/AST/RecursiveASTVisitor.h"
#include "llvm/ADT/Optional.h"

namespace clang {
class Stmt;
class Decl;
class Type;
class CapturedStmt;
class OMPExecutableDirective;
class SourceLocation;
class FunctionDecl;
class Attr;
class Rewriter;
class ASTContext;
} // namespace clang

class TargetCode;
class TargetCodeFragment;
class TargetCodeRegion;

class TypeDeclResolver;

class DiscoverTypesInDeclVisitor
    : public clang::RecursiveASTVisitor<DiscoverTypesInDeclVisitor> {

  std::function<void(clang::TypeDecl *)> OnEachTypeRef;
  void processType(const clang::Type *D);

public:
  DiscoverTypesInDeclVisitor(TypeDeclResolver &Types);
  DiscoverTypesInDeclVisitor(std::function<void(clang::TypeDecl *)> F)
      : OnEachTypeRef(F){};
  bool VisitDecl(clang::Decl *D);
  bool VisitExpr(clang::Expr *D);
  bool VisitType(clang::Type *T);
};

class DiscoverFunctionsInDeclVisitor
    : public clang::RecursiveASTVisitor<DiscoverFunctionsInDeclVisitor> {

  std::function<void(clang::FunctionDecl *)> OnEachFuncRef;

public:
  DiscoverFunctionsInDeclVisitor(FunctionDeclResolver &Functions);
  DiscoverFunctionsInDeclVisitor(std::function<void(clang::FunctionDecl *)> F)
      : OnEachFuncRef(F){};

  bool VisitExpr(clang::Expr *E);
};

class FindDeclRefExprVisitor
    : public clang::RecursiveASTVisitor<FindDeclRefExprVisitor> {

  std::unordered_set<clang::VarDecl *> VarSet;

public:
  FindDeclRefExprVisitor() {}
  bool VisitStmt(clang::Stmt *S);
  // bool VisitDecl(clang::Decl *D);
  std::unordered_set<clang::VarDecl *> *getVarSet() { return &VarSet; }
};

class FindLoopStmtVisitor
    : public clang::RecursiveASTVisitor<FindLoopStmtVisitor> {

  FindDeclRefExprVisitor FindDeclRefVisitor;

public:
  FindLoopStmtVisitor() {}
  bool VisitStmt(clang::Stmt *S);
  std::unordered_set<clang::VarDecl *> *getVarSet() {
    return FindDeclRefVisitor.getVarSet();
  }
};

class FindTargetCodeVisitor
    : public clang::RecursiveASTVisitor<FindTargetCodeVisitor> {

  clang::ASTContext &Context;

  TargetCode &TargetCodeInfo;
  DiscoverTypesInDeclVisitor DiscoverTypeVisitor;
  DiscoverFunctionsInDeclVisitor DiscoverFunctionVisitor;
  FunctionDeclResolver &Functions;
  FindDeclRefExprVisitor FindDeclRefVisitor;

  std::stack<clang::FunctionDecl *> LastVisitedFuncDecl;
  std::unordered_set<std::string> FuncDeclWithoutBody;

public:
  FindTargetCodeVisitor(TargetCode &Code, TypeDeclResolver &Types,
                        FunctionDeclResolver &Functions,
                        clang::ASTContext &Context)
      : Context(Context), TargetCodeInfo(Code), DiscoverTypeVisitor(Types),
        DiscoverFunctionVisitor(Functions), Functions(Functions){};
  bool TraverseDecl(clang::Decl *D);
  bool VisitStmt(clang::Stmt *S);
  bool VisitDecl(clang::Decl *D);

private:
  bool processTargetRegion(clang::OMPExecutableDirective *TargetDirective);
  void addTargetRegionArgs(clang::CapturedStmt *S,
                           clang::OMPExecutableDirective *TargetDirective,
                           std::shared_ptr<TargetCodeRegion> TCR);
};

class FindArraySectionVisitor
    : public clang::RecursiveASTVisitor<FindArraySectionVisitor> {

  std::map<clang::VarDecl *, clang::Expr *> &LowerBoundsMap;

public:
  FindArraySectionVisitor(
      std::map<clang::VarDecl *, clang::Expr *> &LowerBoundsMap)
      : LowerBoundsMap(LowerBoundsMap) {}
  bool VisitExpr(clang::Expr *E);
};

class FindPrivateVariablesVisitor
    : public clang::RecursiveASTVisitor<FindPrivateVariablesVisitor> {

  clang::SourceManager &SM;
  clang::SourceLocation RegionTopSourceLocation;
  std::set<clang::VarDecl *> VarSet;

public:
  FindPrivateVariablesVisitor(clang::SourceLocation TopSourceLocation, clang::SourceManager &SM)
      : SM(SM), RegionTopSourceLocation(TopSourceLocation) {}

  bool VisitExpr(clang::Expr *E);
  std::set<clang::VarDecl *> &getVarSet() {
    return VarSet;
  }
};
```



