# TargetCodeDecl



This class represents a declaration, i.e.  [More...](#detailed-description)


`#include <TargetCodeFragment.h>`

Inherits from [TargetCodeFragment](Classes/classTargetCodeFragment.md)

## Public Functions

|                | Name           |
| -------------- | -------------- |
| bool | **[classof](Classes/classTargetCodeDecl.md#function-classof)**(const [TargetCodeFragment](Classes/classTargetCodeFragment.md) * TCF) |
| | **[TargetCodeDecl](Classes/classTargetCodeDecl.md#function-targetcodedecl)**(clang::Decl * Node) |
| virtual std::string | **[PrintPretty](Classes/classTargetCodeDecl.md#function-printpretty)**() override<br>Tries to use Clang's PrettyPrinter when possible (this is currently only for target regions).  |
| virtual clang::SourceRange | **[getRealRange](Classes/classTargetCodeDecl.md#function-getrealrange)**() override<br>Get the source range of the fragment.  |
| virtual clang::SourceRange | **[getSpellingRange](Classes/classTargetCodeDecl.md#function-getspellingrange)**() override<br>Get the spelling source range.  |

## Additional inherited members

**Public Types inherited from [TargetCodeFragment](Classes/classTargetCodeFragment.md)**

|                | Name           |
| -------------- | -------------- |
| enum| **[TargetCodeFragmentKind](Classes/classTargetCodeFragment.md#enum-targetcodefragmentkind)** { TCFK_TargetCodeFragment, TCFK_TargetCodeRegion, TCFK_TargetCodeDecl}<br>Enum for LLVMs RTTI.  |

**Public Functions inherited from [TargetCodeFragment](Classes/classTargetCodeFragment.md)**

|                | Name           |
| -------------- | -------------- |
| [TargetCodeFragmentKind](Classes/classTargetCodeFragment.md#enum-targetcodefragmentkind) | **[getKind](Classes/classTargetCodeFragment.md#function-getkind)**() const<br>Accessor for LLVMs RTTI.  |
| | **[TargetCodeFragment](Classes/classTargetCodeFragment.md#function-targetcodefragment)**(clang::ASTContext & Context, [TargetCodeFragmentKind](Classes/classTargetCodeFragment.md#enum-targetcodefragmentkind) Kind) |
| virtual | **[~TargetCodeFragment](Classes/classTargetCodeFragment.md#function-~targetcodefragment)**() =0 |
| virtual clang::SourceRange | **[getInnerRange](Classes/classTargetCodeFragment.md#function-getinnerrange)**()<br>Gets the 'inner' source range.  |
| clang::OpenMPDirectiveKind | **[getTargetCodeKind](Classes/classTargetCodeFragment.md#function-gettargetcodekind)**()<br>Accessor to TargetCodeKind.  |
| const clang::LangOptions & | **[GetLangOpts](Classes/classTargetCodeFragment.md#function-getlangopts)**()<br>Accessor to lang opts of the current context.  |
| clang::PrintingPolicy | **[getPP](Classes/classTargetCodeFragment.md#function-getpp)**() |

**Public Attributes inherited from [TargetCodeFragment](Classes/classTargetCodeFragment.md)**

|                | Name           |
| -------------- | -------------- |
| bool | **[NeedsSemicolon](Classes/classTargetCodeFragment.md#variable-needssemicolon)** <br>Does the source code generation need to add a semicolon to this fragment.  |
| clang::OpenMPDirectiveKind | **[TargetCodeKind](Classes/classTargetCodeFragment.md#variable-targetcodekind)** <br>What kind of code are we copying.  |
| bool | **[HasExtraBraces](Classes/classTargetCodeFragment.md#variable-hasextrabraces)**  |

**Protected Attributes inherited from [TargetCodeFragment](Classes/classTargetCodeFragment.md)**

|                | Name           |
| -------------- | -------------- |
| const [TargetCodeFragmentKind](Classes/classTargetCodeFragment.md#enum-targetcodefragmentkind) | **[Kind](Classes/classTargetCodeFragment.md#variable-kind)** <br>Variable for LLVMs RTTI.  |
| clang::ASTContext & | **[Context](Classes/classTargetCodeFragment.md#variable-context)**  |
| clang::PrintingPolicy | **[PP](Classes/classTargetCodeFragment.md#variable-pp)**  |


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

**Reimplements**: [TargetCodeFragment::PrintPretty](Classes/classTargetCodeFragment.md#function-printpretty)


### function getRealRange

```cpp
virtual clang::SourceRange getRealRange() override
```

Get the source range of the fragment. 

**Reimplements**: [TargetCodeFragment::getRealRange](Classes/classTargetCodeFragment.md#function-getrealrange)


### function getSpellingRange

```cpp
virtual clang::SourceRange getSpellingRange() override
```

Get the spelling source range. 

**Reimplements**: [TargetCodeFragment::getSpellingRange](Classes/classTargetCodeFragment.md#function-getspellingrange)


That is the range without macro expansions. 


