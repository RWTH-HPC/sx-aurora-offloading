# src/main.cpp

This file implements sotoc, a clang to to enable outlining of OpenMP target region, which can be used by different compiler. 

## Namespaces

| Name           |
| -------------- |
| **[clang::tooling](Namespaces/namespaceclang_1_1tooling.md)**  |
| **[llvm](Namespaces/namespacellvm.md)**  |

## Classes

|                | Name           |
| -------------- | -------------- |
| class | **[TargetRegionTransformer](Classes/classTargetRegionTransformer.md)**  |
| class | **[SourceTransformAction](Classes/classSourceTransformAction.md)**  |

## Functions

|                | Name           |
| -------------- | -------------- |
| llvm::cl::OptionCategory | **[SotocCategory](Files/main_8cpp.md#function-sotoccategory)**("sotoc options" ) |
| llvm::cl::extrahelp | **[MoreHelp](Files/main_8cpp.md#function-morehelp)**("\nExtracts code in OpenMP target regions from source file and ""generates target function code" ) |
| int | **[main](Files/main_8cpp.md#function-main)**(int argc, const char ** argv) |

## Attributes

|                | Name           |
| -------------- | -------------- |
| int | **[SotocDebugLevel](Files/main_8cpp.md#variable-sotocdebuglevel)**  |


## Functions Documentation

### function SotocCategory

```cpp
static llvm::cl::OptionCategory SotocCategory(
    "sotoc options" 
)
```


### function MoreHelp

```cpp
static llvm::cl::extrahelp MoreHelp(
    "\nExtracts code in OpenMP target regions from source file and ""generates target function code" 
)
```


### function main

```cpp
int main(
    int argc,
    const char ** argv
)
```



## Attributes Documentation

### variable SotocDebugLevel

```cpp
int SotocDebugLevel = 0;
```



## Source code
```cpp
//===-- sotoc/src/main.cpp ------------------------------------------------===//
//
//                     The LLVM Compiler Infrastructure
//
// This file is distributed under the University of Illinois Open Source
// License. See LICENSE.TXT for details.
//
//===----------------------------------------------------------------------===//
//===----------------------------------------------------------------------===//

#include <cstdlib>
#include <memory>
#include <sstream>
#include <string>

#include "clang/Frontend/FrontendActions.h"
#include "clang/Tooling/CommonOptionsParser.h"
#include "clang/Tooling/Tooling.h"
// Declares llvm::cl::extrahelp.
#include "clang/AST/ASTConsumer.h"
#include "clang/AST/ASTContext.h"
#include "clang/AST/RecursiveASTVisitor.h"
#include "clang/Basic/SourceManager.h"
#include "clang/Frontend/CompilerInstance.h"
#include "clang/Rewrite/Core/Rewriter.h"
#include "llvm/Support/CommandLine.h"
#include "llvm/Support/Process.h"
#include "llvm/Support/raw_ostream.h"

#include "Debug.h"
#include "DeclResolver.h"
#include "TargetCode.h"
#include "TargetCodeFragment.h"
#include "Visitors.h"

using namespace clang::tooling;
using namespace llvm;

class TargetRegionTransformer : public clang::ASTConsumer {
  TargetCode &Code;
  clang::Rewriter &TargetCodeRewriter;

public:
  TargetRegionTransformer(TargetCode &Code, clang::Rewriter &TargetCodeRewriter)
      : Code(Code), TargetCodeRewriter(TargetCodeRewriter) {}

  void HandleTranslationUnit(clang::ASTContext &Context) final {
    // create space to store information types and functions
    TypeDeclResolver Types;
    // Functinos are... special because they can reference new types
    FunctionDeclResolver Functions(Types);

    // read target code information from AST into TargetCode
    FindTargetCodeVisitor FindCodeVisitor(Code, Types, Functions, Context);
    FindCodeVisitor.TraverseDecl(Context.getTranslationUnitDecl());
    Functions.orderAndAddFragments(Code);
    Types.orderAndAddFragments(Code);
  }
};

class SourceTransformAction : public clang::ASTFrontendAction {
  clang::Rewriter TargetCodeRewriter;
  TargetCode *Code;

public:
  void EndSourceFileAction() override {
    // std::error_code error_code;
    // llvm::raw_fd_ostream outFile("output.txt", error_code,
    // llvm::sys::fs::F_Append);
    DEBUGP("Generating Code");
    Code->generateCode(llvm::outs());
    // outFile.close();
    delete Code;
  }

  std::unique_ptr<clang::ASTConsumer>
  CreateASTConsumer(clang::CompilerInstance &CI, clang::StringRef) final {
    TargetCodeRewriter.setSourceMgr(CI.getSourceManager(), CI.getLangOpts());
    // TargetCode holds all necessary information about source locations of
    // target regions to extract that code
    Code = new TargetCode(TargetCodeRewriter);
    return std::unique_ptr<clang::ASTConsumer>(
        new TargetRegionTransformer(*Code, TargetCodeRewriter));
  }
};

int SotocDebugLevel = 0;

static llvm::cl::OptionCategory SotocCategory("sotoc options");
static llvm::cl::extrahelp
    MoreHelp("\nExtracts code in OpenMP target regions from source file and "
             "generates target function code");

int main(int argc, const char **argv) {
  auto option = clang::tooling::CommonOptionsParser::create(argc, argv, SotocCategory);
  if (!option) {
    return -1;
  }
  clang::tooling::ClangTool tool(option->getCompilations(),
                                 option->getSourcePathList());

#ifdef SOTOC_DEBUG
  SotocDebugLevel =
      std::atoi(sys::Process::GetEnv("SOTOC_DEBUG").getValueOr("0").c_str());
#endif

  DEBUGP("Starting source transformation tool");

  return tool.run(
      clang::tooling::newFrontendActionFactory<SourceTransformAction>().get());
}
```



