# src/TargetCode.h



## Namespaces

| Name           |
| -------------- |
| **[clang](Namespaces/namespaceclang/)**  |

## Classes

|                | Name           |
| -------------- | -------------- |
| class | **[TargetCode](Classes/classTargetCode/)** <br>A collection of all code from the input file that needs to be copied to the target source file.  |

## Types

|                | Name           |
| -------------- | -------------- |
| using std::deque< std::shared_ptr< [TargetCodeFragment](Classes/classTargetCodeFragment/) >> | **[TargetCodeFragmentDeque](Files/TargetCode_8h/#using-targetcodefragmentdeque)**  |

## Attributes

|                | Name           |
| -------------- | -------------- |
| int | **[clauseparam](Files/TargetCode_8h/#variable-clauseparam)**  |

## Types Documentation

### using TargetCodeFragmentDeque

```cpp
using TargetCodeFragmentDeque =  std::deque<std::shared_ptr<TargetCodeFragment>>;
```




## Attributes Documentation

### variable clauseparam

```cpp
int clauseparam;
```



## Source code
```cpp
//===-- sotoc/src/TargetCode.h --------------------------------------------===//
//
//                     The LLVM Compiler Infrastructure
//
// This file is distributed under the University of Illinois Open Source
// License. See LICENSE.TXT for details.
//
//===----------------------------------------------------------------------===//

#pragma once

#include <deque>
#include <memory>
#include <set>
#include <string>

#include "clang/Rewrite/Core/Rewriter.h"

#include "TargetCodeFragment.h"

namespace clang {
class SourceManager;
}

using TargetCodeFragmentDeque = std::deque<std::shared_ptr<TargetCodeFragment>>;

extern int clauseparam;
class TargetCode {

  TargetCodeFragmentDeque CodeFragments;
  std::set<std::string> SystemHeaders;
  clang::Rewriter &TargetCodeRewriter;
  clang::SourceManager &SM;

public:
  TargetCode(clang::Rewriter &TargetCodeRewriter)
      : TargetCodeRewriter(TargetCodeRewriter),
        SM(TargetCodeRewriter.getSourceMgr()){};

  bool addCodeFragment(std::shared_ptr<TargetCodeFragment> Frag,
                       bool PushFront = false);
  bool addCodeFragmentFront(std::shared_ptr<TargetCodeFragment> Fag);
  void generateCode(llvm::raw_ostream &Out);
  TargetCodeFragmentDeque::const_iterator getCodeFragmentsBegin() {
    return CodeFragments.begin();
  }
  TargetCodeFragmentDeque::const_iterator getCodeFragmentsEnd() {
    return CodeFragments.end();
  }
  void addHeader(const std::string &Header) { SystemHeaders.insert(Header); }

private:
  void generateVariableDecl(const TargetRegionVariable &Var,
                            llvm::raw_ostream &Out);
  void generateFunctionPrologue(TargetCodeRegion *TCR, llvm::raw_ostream &Out);
  void generateFunctionEpilogue(TargetCodeRegion *TCR, llvm::raw_ostream &Out);
  std::string generateFunctionName(TargetCodeRegion *TCR);
  void generateArgument(const TargetRegionVariable &Aarg,
                        llvm::raw_ostream &Out);
};
```



