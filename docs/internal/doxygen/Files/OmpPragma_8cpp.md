# src/OmpPragma.cpp

This file implements the class [OmpPragma](../Classes/classOmpPragma.md), which is used to generate repla- cement pragmas for teams and team combined constructs. 

## Attributes

|                | Name           |
| -------------- | -------------- |
| int | **[ClauseParamCounter](../Files/OmpPragma_8cpp.md#variable-clauseparamcounter)**  |



## Attributes Documentation

### variable ClauseParamCounter

```cpp
int ClauseParamCounter = -1;
```



## Source code
```cpp
//===-- sotoc/src/TargetCode ------------------------ ---------------------===//
//
//                     The LLVM Compiler Infrastructure
//
// This file is distributed under the University of Illinois Open Source
// License. See LICENSE.TXT for details.
//
//===----------------------------------------------------------------------===//
//===----------------------------------------------------------------------===//

#include "clang/AST/PrettyPrinter.h"
#include <ctype.h>

#include "OmpPragma.h"

int ClauseParamCounter = -1;

void OmpPragma::printReplacement(llvm::raw_ostream &Out) {

  switch (Kind) {
  case clang::OpenMPDirectiveKind::OMPD_target_parallel: {
    Out << "  #pragma omp parallel ";
    break;
  }
  case clang::OpenMPDirectiveKind::OMPD_teams_distribute_parallel_for:
  case clang::OpenMPDirectiveKind::OMPD_target_parallel_for: {
    Out << "  #pragma omp parallel for ";
    break;
  }
  case clang::OpenMPDirectiveKind::OMPD_teams_distribute_parallel_for_simd:
  case clang::OpenMPDirectiveKind::OMPD_target_parallel_for_simd: {
    Out << "  #pragma _NEC ivdep\n  #pragma omp parallel for simd ";
    break;
  }
  case clang::OpenMPDirectiveKind::OMPD_distribute_simd:
  case clang::OpenMPDirectiveKind::OMPD_teams_distribute_simd:
  case clang::OpenMPDirectiveKind::OMPD_target_teams_distribute_simd:
  case clang::OpenMPDirectiveKind::OMPD_target_simd: {
    Out << "  #pragma _NEC ivdep\n  #pragma omp simd ";
    break;
  }
  case clang::OpenMPDirectiveKind::OMPD_target_teams_distribute_parallel_for: {
    Out << "  #pragma omp parallel for ";
    break;
  }
  case clang::OpenMPDirectiveKind::
      OMPD_target_teams_distribute_parallel_for_simd: {
    Out << "  #pragma _NEC ivdep\n  #pragma omp parallel for simd ";
    break;
  }
  default:
    return;
  }
  printClauses(Out);
}

void OmpPragma::printAddition(llvm::raw_ostream &Out) {
  Out << "  #pragma _NEC ivdep ";
}

bool OmpPragma::isReplaceable(clang::OMPExecutableDirective *Directive) {
  if (llvm::isa<clang::OMPTeamsDirective>(Directive) ||
      llvm::isa<clang::OMPTeamsDistributeDirective>(Directive) ||
      llvm::isa<clang::OMPTeamsDistributeSimdDirective>(Directive) ||
      llvm::isa<clang::OMPTeamsDistributeParallelForDirective>(Directive) ||
      llvm::isa<clang::OMPTeamsDistributeParallelForSimdDirective>(Directive) ||
      llvm::isa<clang::OMPDistributeDirective>(Directive)) {
    return true;
  }
  return false;
}

bool OmpPragma::needsAdditionalPragma(clang::OMPExecutableDirective *Directive) {
  if (llvm::isa<clang::OMPForSimdDirective>(Directive) ||
      llvm::isa<clang::OMPParallelForSimdDirective>(Directive) ||
      llvm::isa<clang::OMPSimdDirective>(Directive) ||
      llvm::isa<clang::OMPTaskLoopSimdDirective>(Directive)) {
    return true;
  }
  return false;
}

bool OmpPragma::isClausePrintable(clang::OMPClause *Clause) {
  switch (Kind) {
  case clang::OpenMPDirectiveKind::OMPD_target: {
    switch (Clause->getClauseKind()) {
    // case clang::OpenMPClauseKind::OMPC_if:
    // case clang::OpenMPClauseKind::OMPC_device:
    // case clang::OpenMPClauseKind::OMPC_map:
    case clang::OpenMPClauseKind::OMPC_private:
    // case clang::OpenMPClauseKind::OMPC_nowait:
    // case clang::OpenMPClauseKind::OMPC_depend:
    // case clang::OpenMPClauseKind::OMPC_defaultmap:
    case clang::OpenMPClauseKind::OMPC_firstprivate:
      // case clang::OpenMPClauseKind::OMPC_is_device_ptr:
      // case clang::OpenMPClauseKind::OMPC_reduction:
      return true;
    default:
      return false;
    }
  }
  /*case clang::OpenMPDirectiveKind::OMPD_target_teams: {
    switch (Clause->getClauseKind()) {
    // case clang::OpenMPClauseKind::OMPC_map:
    case clang::OpenMPClauseKind::OMPC_default:
    case clang::OpenMPClauseKind::OMPC_private:
    case clang::OpenMPClauseKind::OMPC_firstprivate:
    case clang::OpenMPClauseKind::OMPC_shared:
    case clang::OpenMPClauseKind::OMPC_reduction:
    case clang::OpenMPClauseKind::OMPC_num_teams:
    case clang::OpenMPClauseKind::OMPC_thread_limit:
      return true;
    default:
      return false;
    }
  }*/
  case clang::OpenMPDirectiveKind::OMPD_target_parallel: {
    switch (Clause->getClauseKind()) {
    // case clang::OpenMPClauseKind::OMPC_map:
    case clang::OpenMPClauseKind::OMPC_num_threads:
    case clang::OpenMPClauseKind::OMPC_default:
    case clang::OpenMPClauseKind::OMPC_proc_bind:
    case clang::OpenMPClauseKind::OMPC_private:
    case clang::OpenMPClauseKind::OMPC_firstprivate:
    case clang::OpenMPClauseKind::OMPC_shared:
      // case clang::OpenMPClauseKind::OMPC_reduction:
      return true;
    default:
      return false;
    case clang::OpenMPClauseKind::OMPC_if:
      clang::OMPIfClause* IC = llvm::dyn_cast_or_null<clang::OMPIfClause>(Clause);
      if ((IC->getNameModifier()) == clang::OpenMPDirectiveKind::OMPD_target) {
        return false;
      } else {
        return true;
      }
    }
  }
  case clang::OpenMPDirectiveKind::OMPD_target_parallel_for: {
    switch (Clause->getClauseKind()) {
    // case clang::OpenMPClauseKind::OMPC_map:
    case clang::OpenMPClauseKind::OMPC_num_threads:
    case clang::OpenMPClauseKind::OMPC_default:
    case clang::OpenMPClauseKind::OMPC_proc_bind:
    case clang::OpenMPClauseKind::OMPC_private:
    case clang::OpenMPClauseKind::OMPC_firstprivate:
    case clang::OpenMPClauseKind::OMPC_shared:
    case clang::OpenMPClauseKind::OMPC_reduction:
    case clang::OpenMPClauseKind::OMPC_lastprivate:
    case clang::OpenMPClauseKind::OMPC_collapse:
    case clang::OpenMPClauseKind::OMPC_schedule:
    case clang::OpenMPClauseKind::OMPC_ordered:
    case clang::OpenMPClauseKind::OMPC_linear:
      return true;
    default:
      return false;
    case clang::OpenMPClauseKind::OMPC_if:
      clang::OMPIfClause* IC = llvm::dyn_cast_or_null<clang::OMPIfClause>(Clause);
      if ((IC->getNameModifier()) == clang::OpenMPDirectiveKind::OMPD_target) {
        return false;
      } else {
        return true;
      }
    }
  }
  case clang::OpenMPDirectiveKind::OMPD_target_parallel_for_simd: {
    switch (Clause->getClauseKind()) {
    // case clang::OpenMPClauseKind::OMPC_map:
    case clang::OpenMPClauseKind::OMPC_num_threads:
    case clang::OpenMPClauseKind::OMPC_default:
    case clang::OpenMPClauseKind::OMPC_proc_bind:
    case clang::OpenMPClauseKind::OMPC_private:
    case clang::OpenMPClauseKind::OMPC_firstprivate:
    case clang::OpenMPClauseKind::OMPC_shared:
    case clang::OpenMPClauseKind::OMPC_reduction:
    case clang::OpenMPClauseKind::OMPC_lastprivate:
    case clang::OpenMPClauseKind::OMPC_collapse:
    case clang::OpenMPClauseKind::OMPC_schedule:
    case clang::OpenMPClauseKind::OMPC_safelen:
    case clang::OpenMPClauseKind::OMPC_simdlen:
    case clang::OpenMPClauseKind::OMPC_linear:
    case clang::OpenMPClauseKind::OMPC_aligned:
    case clang::OpenMPClauseKind::OMPC_ordered:
      return true;
    default:
      return false;
    case clang::OpenMPClauseKind::OMPC_if:
      clang::OMPIfClause* IC = llvm::dyn_cast_or_null<clang::OMPIfClause>(Clause);
      if ((IC->getNameModifier()) == clang::OpenMPDirectiveKind::OMPD_target) {
        return false;
      } else {
        return true;
      }
    }
  }
  case clang::OpenMPDirectiveKind::OMPD_target_simd: {
    switch (Clause->getClauseKind()) {
    // case clang::OpenMPClauseKind::OMPC_map:
    case clang::OpenMPClauseKind::OMPC_private:
    case clang::OpenMPClauseKind::OMPC_lastprivate:
    case clang::OpenMPClauseKind::OMPC_linear:
    case clang::OpenMPClauseKind::OMPC_aligned:
    case clang::OpenMPClauseKind::OMPC_safelen:
    case clang::OpenMPClauseKind::OMPC_simdlen:
    case clang::OpenMPClauseKind::OMPC_collapse:
    case clang::OpenMPClauseKind::OMPC_reduction:
      return true;
    default:
      return false;
    }
  }
  case clang::OpenMPDirectiveKind::OMPD_target_teams_distribute: {
    switch (Clause->getClauseKind()) {
    // case clang::OpenMPClauseKind::OMPC_map:
    case clang::OpenMPClauseKind::OMPC_default:
    case clang::OpenMPClauseKind::OMPC_private:
    case clang::OpenMPClauseKind::OMPC_firstprivate:
    case clang::OpenMPClauseKind::OMPC_shared:
    case clang::OpenMPClauseKind::OMPC_reduction:
    // case clang::OpenMPClauseKind::OMPC_thread_limit:
    case clang::OpenMPClauseKind::OMPC_lastprivate:
    case clang::OpenMPClauseKind::OMPC_collapse:
    case clang::OpenMPClauseKind::OMPC_dist_schedule:
      return true;
    default:
      return false;
    }
  }
  case clang::OpenMPDirectiveKind::OMPD_teams_distribute_parallel_for:
  case clang::OpenMPDirectiveKind::OMPD_target_teams_distribute_parallel_for: {
    switch (Clause->getClauseKind()) {
    // case clang::OpenMPClauseKind::OMPC_map:
    case clang::OpenMPClauseKind::OMPC_firstprivate:
    case clang::OpenMPClauseKind::OMPC_lastprivate:
    case clang::OpenMPClauseKind::OMPC_collapse:
    case clang::OpenMPClauseKind::OMPC_dist_schedule:
    case clang::OpenMPClauseKind::OMPC_num_threads:
    case clang::OpenMPClauseKind::OMPC_default:
    case clang::OpenMPClauseKind::OMPC_proc_bind:
    case clang::OpenMPClauseKind::OMPC_private:
    case clang::OpenMPClauseKind::OMPC_shared:
    case clang::OpenMPClauseKind::OMPC_reduction:
    case clang::OpenMPClauseKind::OMPC_schedule:
    // case clang::OpenMPClauseKind::OMPC_thread_limit:
      return true;
    default:
      return false;
    case clang::OpenMPClauseKind::OMPC_if:
      clang::OMPIfClause* IC = llvm::dyn_cast_or_null<clang::OMPIfClause>(Clause);
      if ((IC->getNameModifier()) == clang::OpenMPDirectiveKind::OMPD_target) {
        return false;
      } else {
        return true;
      }
   }
  }
  case clang::OpenMPDirectiveKind::OMPD_teams_distribute_parallel_for_simd:
  case clang::OpenMPDirectiveKind::
      OMPD_target_teams_distribute_parallel_for_simd: {
    switch (Clause->getClauseKind()) {
    // case clang::OpenMPClauseKind::OMPC_map:
    case clang::OpenMPClauseKind::OMPC_firstprivate:
    case clang::OpenMPClauseKind::OMPC_lastprivate:
    case clang::OpenMPClauseKind::OMPC_collapse:
    case clang::OpenMPClauseKind::OMPC_dist_schedule:
    case clang::OpenMPClauseKind::OMPC_num_threads:
    case clang::OpenMPClauseKind::OMPC_default:
    case clang::OpenMPClauseKind::OMPC_proc_bind:
    case clang::OpenMPClauseKind::OMPC_private:
    case clang::OpenMPClauseKind::OMPC_shared:
    case clang::OpenMPClauseKind::OMPC_reduction:
    case clang::OpenMPClauseKind::OMPC_schedule:
    case clang::OpenMPClauseKind::OMPC_linear:
    case clang::OpenMPClauseKind::OMPC_aligned:
    case clang::OpenMPClauseKind::OMPC_safelen:
    case clang::OpenMPClauseKind::OMPC_simdlen:
    // case clang::OpenMPClauseKind::OMPC_thread_limit:
      return true;
    default:
      return false;
    case clang::OpenMPClauseKind::OMPC_if:
      clang::OMPIfClause* IC = llvm::dyn_cast_or_null<clang::OMPIfClause>(Clause);
      if ((IC->getNameModifier()) == clang::OpenMPDirectiveKind::OMPD_target) {
        return false;
      } else {
        return true;
      }
    }
  }
  case clang::OpenMPDirectiveKind::OMPD_teams_distribute_simd:
  case clang::OpenMPDirectiveKind::OMPD_target_teams_distribute_simd: {
    switch (Clause->getClauseKind()) {
    // case clang::OpenMPClauseKind::OMPC_map:
    case clang::OpenMPClauseKind::OMPC_default:
    case clang::OpenMPClauseKind::OMPC_private:
    case clang::OpenMPClauseKind::OMPC_firstprivate:
    case clang::OpenMPClauseKind::OMPC_shared:
    case clang::OpenMPClauseKind::OMPC_reduction:
    // case clang::OpenMPClauseKind::OMPC_thread_limit:
    case clang::OpenMPClauseKind::OMPC_lastprivate:
    case clang::OpenMPClauseKind::OMPC_collapse:
    case clang::OpenMPClauseKind::OMPC_dist_schedule:
    case clang::OpenMPClauseKind::OMPC_linear:
    case clang::OpenMPClauseKind::OMPC_aligned:
    case clang::OpenMPClauseKind::OMPC_safelen:
    case clang::OpenMPClauseKind::OMPC_simdlen:
      return true;
    default:
      return false;
    case clang::OpenMPClauseKind::OMPC_if:
      clang::OMPIfClause* IC = llvm::dyn_cast_or_null<clang::OMPIfClause>(Clause);
      if ((IC->getNameModifier()) == clang::OpenMPDirectiveKind::OMPD_target) {
        return false;
      } else {
        return true;
      }
    }
  }
  default:
    break;
  }
  return false;
}

void OmpPragma::printClauses(llvm::raw_ostream &Out) {
  std::string InString;
  llvm::raw_string_ostream In(InString);
  clang::OMPClausePrinter Printer(In, PP);

  for (auto C : Clauses) {
    // Only print clauses that are both printable (for us) and are actually in
    // the users code (is explicit)
    if (isClausePrintable(C) && !C->isImplicit()) {
      Printer.Visit(C);

      In.str();
      size_t inp = InString.find("(")+1;
      size_t paramlength = InString.length()-inp-1;
      std::string param = InString.substr(inp,paramlength);
      InString.erase(inp,paramlength);

      rewriteParam(C, &param);
      Out << InString.insert(inp,param) << " ";
//      addShared(C, &param, Out);
      InString.clear();
    }
  }
}

void OmpPragma::rewriteParam(clang::OMPClause *Clause,std::string *In) {

if (Clause->getClauseKind() == clang::OpenMPClauseKind::OMPC_num_threads) {
  bool isNumerical = true;

  for (auto i : *In) {
    if (!isdigit(i)) {
    isNumerical = false;
    }
  }

  if (!isNumerical) {
    *In = "__sotoc_clause_param_" + std::to_string(ClauseParamCounter);
    ClauseParamCounter++;
  }
}/* else if (Clause->getClauseKind() == clang::OpenMPClauseKind::OMPC_shared) {
  std::string RedString;
  std::string DefaultString;
  llvm::raw_string_ostream Red(RedString);
  llvm::raw_string_ostream Default(DefaultString);
  clang::OMPClausePrinter RedPrinter(Red, PP);
  clang::OMPClausePrinter DefaultPrinter(Default, PP);
  
  for (auto CD: Clauses) {
    if (CD->getClauseKind() == clang::OpenMPClauseKind::OMPC_default) {
      DefaultPrinter.Visit(CD);
      Default.str();
      size_t defaultp = DefaultString.find("(")+1;
      size_t paramlength_default = DefaultString.length()-defaultp-1;
      std::string param_default = DefaultString.substr(defaultp,paramlength_default);
      if (!param_default.compare(std::string("none"))) {
        for (auto CR: Clauses) {
          if (CR->getClauseKind() == clang::OpenMPClauseKind::OMPC_reduction){
        RedPrinter.Visit(CR);
            Red.str();
            size_t redp = RedString.find(":")+1;
            size_t paramlength_red = RedString.length()-redp-1;
            std::string param_red = RedString.substr(redp,paramlength_red);
    
        In->append("," + param_red);
        return;
          }
   //     }
   //   }
   // }
  }
}*/
}

void OmpPragma::addShared(clang::OMPClause *Clause, std::string *In, llvm::raw_ostream &Out) {
if (Clause->getClauseKind() == clang::OpenMPClauseKind::OMPC_reduction) {
  for (auto CS: Clauses) {
    if (CS->getClauseKind() == clang::OpenMPClauseKind::OMPC_shared){
      return;
    }
  }
  size_t sharedp = In->find(":")+1;
  size_t length = In->length()-sharedp-1;
  Out << "shared(" << In->substr(sharedp,length) << ")";
}
}

bool OmpPragma::needsStructuredBlock() {
  switch (Kind) {
  case clang::OpenMPDirectiveKind::OMPD_target_parallel:
  case clang::OpenMPDirectiveKind::OMPD_target_simd:
  case clang::OpenMPDirectiveKind::OMPD_target_teams_distribute_simd:
    return true;
  default:
    return false;
  }
}
```


