# TargetCodeDecl



This class represents a declaration, i.e.  [More...](#detailed-description)


`#include <TargetCodeFragment.h>`

Inherits from [TargetCodeFragment](Classes/classTargetCodeFragment/)

## Public Functions

|                | Name           |
| -------------- | -------------- |
| bool | **[classof](Classes/classTargetCodeDecl/#function-classof)**(const [TargetCodeFragment](Classes/classTargetCodeFragment/) * TCF) |
| | **[TargetCodeDecl](Classes/classTargetCodeDecl/#function-targetcodedecl)**(clang::Decl * Node) |
| virtual std::string | **[PrintPretty](Classes/classTargetCodeDecl/#function-printpretty)**() override<br>Tries to use Clang's PrettyPrinter when possible (this is currently only for target regions).  |
| virtual clang::SourceRange | **[getRealRange](Classes/classTargetCodeDecl/#function-getrealrange)**() override<br>Get the source range of the fragment.  |
| virtual clang::SourceRange | **[getSpellingRange](Classes/classTargetCodeDecl/#function-getspellingrange)**() override<br>Get the spelling source range.  |

## Additional inherited members

**Public Types inherited from [TargetCodeFragment](Classes/classTargetCodeFragment/)**

|                | Name           |
| -------------- | -------------- |
| enum| **[TargetCodeFragmentKind](Classes/classTargetCodeFragment/#enum-targetcodefragmentkind)** { TCFK_TargetCodeFragment, TCFK_TargetCodeRegion, TCFK_TargetCodeDecl}<br>Enum for LLVMs RTTI.  |

**Public Functions inherited from [TargetCodeFragment](Classes/classTargetCodeFragment/)**

|                | Name           |
| -------------- | -------------- |
| [TargetCodeFragmentKind](Classes/classTargetCodeFragment/#enum-targetcodefragmentkind) | **[getKind](Classes/classTargetCodeFragment/#function-getkind)**() const<br>Accessor for LLVMs RTTI.  |
| | **[TargetCodeFragment](Classes/classTargetCodeFragment/#function-targetcodefragment)**(clang::ASTContext & Context, [TargetCodeFragmentKind](Classes/classTargetCodeFragment/#enum-targetcodefragmentkind) Kind) |
| virtual | **[~TargetCodeFragment](Classes/classTargetCodeFragment/#function-~targetcodefragment)**() =0 |
| virtual clang::SourceRange | **[getInnerRange](Classes/classTargetCodeFragment/#function-getinnerrange)**()<br>Gets the 'inner' source range.  |
| clang::OpenMPDirectiveKind | **[getTargetCodeKind](Classes/classTargetCodeFragment/#function-gettargetcodekind)**()<br>Accessor to TargetCodeKind.  |
| const clang::LangOptions & | **[GetLangOpts](Classes/classTargetCodeFragment/#function-getlangopts)**()<br>Accessor to lang opts of the current context.  |
| clang::PrintingPolicy | **[getPP](Classes/classTargetCodeFragment/#function-getpp)**() |

**Public Attributes inherited from [TargetCodeFragment](Classes/classTargetCodeFragment/)**

|                | Name           |
| -------------- | -------------- |
| bool | **[NeedsSemicolon](Classes/classTargetCodeFragment/#variable-needssemicolon)** <br>Does the source code generation need to add a semicolon to this fragment.  |
| clang::OpenMPDirectiveKind | **[TargetCodeKind](Classes/classTargetCodeFragment/#variable-targetcodekind)** <br>What kind of code are we copying.  |
| bool | **[HasExtraBraces](Classes/classTargetCodeFragment/#variable-hasextrabraces)**  |

**Protected Attributes inherited from [TargetCodeFragment](Classes/classTargetCodeFragment/)**

|                | Name           |
| -------------- | -------------- |
| const [TargetCodeFragmentKind](Classes/classTargetCodeFragment/#enum-targetcodefragmentkind) | **[Kind](Classes/classTargetCodeFragment/#variable-kind)** <br>Variable for LLVMs RTTI.  |
| clang::ASTContext & | **[Context](Classes/classTargetCodeFragment/#variable-context)**  |
| clang::PrintingPolicy | **[PP](Classes/classTargetCodeFragment/#variable-pp)**  |


## Detailed Description

```cpp
class TargetCodeDecl;
```

This class represents a declaration, i.e. 

a function, global varialbe, or type declaration that need to be copied from the input source code to the generated source code. 

## Public Functions Documentation

### function classof

```cpp
static inline bool classof(
    const TargetCodeFragment * TCF
)
```


### function TargetCodeDecl

```cpp
inline TargetCodeDecl(
    clang::Decl * Node
)
```


### function PrintPretty

```cpp
virtual std::string PrintPretty() override
```

Tries to use Clang's PrettyPrinter when possible (this is currently only for target regions). 

**Reimplements**: [TargetCodeFragment::PrintPretty](Classes/classTargetCodeFragment/#function-printpretty)


### function getRealRange

```cpp
virtual clang::SourceRange getRealRange() override
```

Get the source range of the fragment. 

**Reimplements**: [TargetCodeFragment::getRealRange](Classes/classTargetCodeFragment/#function-getrealrange)


### function getSpellingRange

```cpp
virtual clang::SourceRange getSpellingRange() override
```

Get the spelling source range. 

**Reimplements**: [TargetCodeFragment::getSpellingRange](Classes/classTargetCodeFragment/#function-getspellingrange)


That is the range without macro expansions. 


