# src/TargetCodeFragment.h



## Namespaces

| Name           |
| -------------- |
| **[clang](../Namespaces/namespaceclang.md)**  |

## Classes

|                | Name           |
| -------------- | -------------- |
| class | **[TargetCodeFragment](../Classes/classTargetCodeFragment.md)** <br>An abstract base class for all fragments of the original code (except header includes) that need to be copied to our generated source code.  |
| class | **[TargetCodeRegion](../Classes/classTargetCodeRegion.md)** <br>Represents one target region.  |
| class | **[TargetCodeDecl](../Classes/classTargetCodeDecl.md)** <br>This class represents a declaration, i.e.  |




## Source code
```cpp linenums="1"
//===-- sotoc/src/TargetCodeFragment.h ------------------------------------===//
//
//                     The LLVM Compiler Infrastructure
//
// This file is distributed under the University of Illinois Open Source
// License. See LICENSE.TXT for details.
//
//===----------------------------------------------------------------------===//

#pragma once

#include <string>
#include <vector>

#include "clang/AST/ASTContext.h"
#include "clang/AST/OpenMPClause.h"
#include "clang/AST/PrettyPrinter.h"
#include "clang/AST/StmtOpenMP.h"
#include "clang/Basic/OpenMPKinds.h"

#include "TargetRegionVariable.h"

// forward declaration of clang types
namespace clang {
class SourceLocation;
class SourceRange;
class Decl;
class VarDecl;
class CapturedStmt;
} // namespace clang

class TargetCodeFragment {
public:
  enum TargetCodeFragmentKind {
    TCFK_TargetCodeFragment,
    TCFK_TargetCodeRegion,
    TCFK_TargetCodeDecl,
  };

protected:
  const TargetCodeFragmentKind Kind;

public:
  TargetCodeFragmentKind getKind() const { return Kind; };
  static bool classof(const TargetCodeFragment *TCF) {
    return TCF->getKind() == TCFK_TargetCodeFragment;
  }

  bool NeedsSemicolon;
  clang::OpenMPDirectiveKind TargetCodeKind;
  bool HasExtraBraces;

protected:
  clang::ASTContext &Context;
  clang::PrintingPolicy PP;

public:
  TargetCodeFragment(clang::ASTContext &Context, TargetCodeFragmentKind Kind)
      : Kind(Kind), NeedsSemicolon(false),
        TargetCodeKind(clang::OpenMPDirectiveKind::OMPD_unknown),
        HasExtraBraces(false), Context(Context), PP(Context.getLangOpts()) {
    PP.Indentation = 1;
    PP.SuppressSpecifiers = 0;
    PP.IncludeTagDefinition = 0;
  };

  virtual ~TargetCodeFragment() = 0;

  virtual std::string PrintPretty() = 0;
  virtual clang::SourceRange getRealRange() = 0;
  virtual clang::SourceRange getInnerRange() { return getRealRange(); };
  virtual clang::SourceRange getSpellingRange() = 0;
  clang::OpenMPDirectiveKind getTargetCodeKind() { return TargetCodeKind; };
  const clang::LangOptions &GetLangOpts() { return Context.getLangOpts(); }
  clang::PrintingPolicy getPP() { return PP; };
};

class TargetCodeRegion : public TargetCodeFragment {
public:
  static bool classof(const TargetCodeFragment *TCF) {
    return (TCF->getKind() == TCFK_TargetCodeRegion ||
            TCF->getKind() == TCFK_TargetCodeFragment);
  };

private:
  clang::CapturedStmt *CapturedStmtNode;
  clang::OMPExecutableDirective *TargetDirective;
  clang::FunctionDecl *ParentFunctionDecl;
  std::vector<TargetRegionVariable> CapturedVars;
  std::vector<clang::OMPClause *> OMPClauses;
  std::vector<clang::VarDecl *> OMPClausesParams;
  std::set<clang::VarDecl *> PrivateVars;

public:
  TargetCodeRegion(clang::CapturedStmt *CapturedStmtNode,
                   clang::OMPExecutableDirective *TargetDirective,
                   clang::FunctionDecl *ParentFunctionDecl,
                   clang::ASTContext &Context)
      : TargetCodeFragment(Context, TCFK_TargetCodeRegion),
        CapturedStmtNode(CapturedStmtNode), TargetDirective(TargetDirective),
        ParentFunctionDecl(ParentFunctionDecl){};

  using captured_vars_const_iterator = std::vector<TargetRegionVariable>::const_iterator;
  using captured_vars_const_range = llvm::iterator_range<captured_vars_const_iterator>;
  using private_vars_const_iterator = std::set<clang::VarDecl *>::const_iterator;
  using private_vars_const_range = llvm::iterator_range<private_vars_const_iterator>;
  using ompclauses_params_const_iterator = std::vector<clang::VarDecl *>::const_iterator;
  using ompclauses_params_const_range = llvm::iterator_range<ompclauses_params_const_iterator>;

  void addCapture(const clang::CapturedStmt::Capture *Capture);
  captured_vars_const_iterator getCapturedVarsBegin() {
    return CapturedVars.begin();
  };
  captured_vars_const_iterator getCapturedVarsEnd() {
    return CapturedVars.end();
  };
  captured_vars_const_range capturedVars() {
    return captured_vars_const_range(getCapturedVarsBegin(), getCapturedVarsEnd());
  };
  void addOMPClause(clang::OMPClause *Clause);
  const std::vector<clang::OMPClause *> &getOMPClauses() const {
    return OMPClauses;
  };
  void setPrivateVars(const std::set<clang::VarDecl *> &VarSet) {
    PrivateVars = VarSet;
  };
  private_vars_const_range privateVars() {
    return private_vars_const_range(PrivateVars.cbegin(), PrivateVars.cend());
  };
  ompclauses_params_const_range ompClausesParams() {
    return ompclauses_params_const_range(OMPClausesParams.cbegin(), OMPClausesParams.cend());
  };
  void addOMPClauseParam(clang::VarDecl *Param);
  bool hasCombineConstruct() {
    return TargetCodeKind != clang::OpenMPDirectiveKind::OMPD_target;
  }
  virtual std::string PrintPretty() override;
  clang::SourceRange getRealRange() override;
  clang::SourceRange getInnerRange() override;
  clang::SourceRange getSpellingRange() override;
  clang::SourceLocation getStartLoc();
  clang::SourceLocation getEndLoc();
  const std::string getParentFuncName();
  clang::SourceLocation getTargetDirectiveLocation();
  std::map<clang::VarDecl *, clang::Expr *> CapturedLowerBounds;
};

class TargetCodeDecl : public TargetCodeFragment {
public:
  static bool classof(const TargetCodeFragment *TCF) {
    return (TCF->getKind() == TCFK_TargetCodeDecl ||
            TCF->getKind() == TCFK_TargetCodeFragment);
  };

private:
  clang::Decl *DeclNode;

public:
  TargetCodeDecl(clang::Decl *Node)
      : TargetCodeFragment(Node->getASTContext(), TCFK_TargetCodeDecl),
        DeclNode(Node){};

  virtual std::string PrintPretty() override;
  clang::SourceRange getRealRange() override;
  clang::SourceRange getSpellingRange() override;
};
```



