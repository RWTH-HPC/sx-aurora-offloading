# src/OmpPragma.h



## Classes

|                | Name           |
| -------------- | -------------- |
| class | **[OmpPragma](../Classes/classOmpPragma.md)** <br>A helper class to rewrite some "pragma omp" (mostly teams and similar combined constructs), which are not supported by sotoc.  |




## Source code
```cpp linenums="1"
//===-- sotoc/src/OmpPragma.h ---------------------------------------------===//
//
//                     The LLVM Compiler Infrastructure
//
// This file is distributed under the University of Illinois Open Source
// License. See LICENSE.TXT for details.
//
//===----------------------------------------------------------------------===//

#pragma once

#include "clang/AST/OpenMPClause.h"
#include "clang/AST/StmtOpenMP.h"
#include "llvm/ADT/APInt.h"
#include "llvm/Support/raw_ostream.h"

#include "TargetCodeFragment.h"
#include <vector>

class OmpPragma {
  clang::PrintingPolicy PP;
  llvm::ArrayRef<clang::OMPClause *> Clauses;
  clang::OpenMPDirectiveKind Kind;
  unsigned int ClauseParamCounter;

public:
  OmpPragma(TargetCodeRegion *TCR)
      : PP(TCR->getPP()), Clauses(TCR->getOMPClauses()),
        Kind(TCR->getTargetCodeKind()), ClauseParamCounter(0) {};
  OmpPragma(clang::OMPExecutableDirective *Directive, clang::PrintingPolicy PP)
      : PP(PP), Clauses(Directive->clauses()),
        Kind(Directive->getDirectiveKind()), ClauseParamCounter(0) {};
  bool needsStructuredBlock();
  void printReplacement(llvm::raw_ostream &Out);
  void printAddition(llvm::raw_ostream &Out);
  static bool isReplaceable(clang::OMPExecutableDirective *Directive);
  static bool needsAdditionalPragma(clang::OMPExecutableDirective *Directive);
private:
  bool isClausePrintable(clang::OMPClause *Clause);
  void rewriteParam(clang::OMPClause *Clause, std::string *In);
  void addShared(clang::OMPClause *Clause, std::string *In, llvm::raw_ostream &Out);
  void printClauses(llvm::raw_ostream &Out);
};
```



