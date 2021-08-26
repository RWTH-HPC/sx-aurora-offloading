# TargetCodeFragment



An abstract base class for all fragments of the original code (except header includes) that need to be copied to our generated source code.  [More...](#detailed-description)


`#include <TargetCodeFragment.h>`

Inherited by [TargetCodeDecl](Classes/classTargetCodeDecl/), [TargetCodeRegion](Classes/classTargetCodeRegion/)

## Public Types

|                | Name           |
| -------------- | -------------- |
| enum| **[TargetCodeFragmentKind](Classes/classTargetCodeFragment/#enum-targetcodefragmentkind)** { TCFK_TargetCodeFragment, TCFK_TargetCodeRegion, TCFK_TargetCodeDecl}<br>Enum for LLVMs RTTI.  |

## Public Functions

|                | Name           |
| -------------- | -------------- |
| [TargetCodeFragmentKind](Classes/classTargetCodeFragment/#enum-targetcodefragmentkind) | **[getKind](Classes/classTargetCodeFragment/#function-getkind)**() const<br>Accessor for LLVMs RTTI.  |
| | **[TargetCodeFragment](Classes/classTargetCodeFragment/#function-targetcodefragment)**(clang::ASTContext & Context, [TargetCodeFragmentKind](Classes/classTargetCodeFragment/#enum-targetcodefragmentkind) Kind) |
| virtual | **[~TargetCodeFragment](Classes/classTargetCodeFragment/#function-~targetcodefragment)**() =0 |
| virtual std::string | **[PrintPretty](Classes/classTargetCodeFragment/#function-printpretty)**() =0<br>Tries to use Clang's PrettyPrinter when possible (this is currently only for target regions).  |
| virtual clang::SourceRange | **[getRealRange](Classes/classTargetCodeFragment/#function-getrealrange)**() =0<br>Get the source range of the fragment.  |
| virtual clang::SourceRange | **[getInnerRange](Classes/classTargetCodeFragment/#function-getinnerrange)**()<br>Gets the 'inner' source range.  |
| virtual clang::SourceRange | **[getSpellingRange](Classes/classTargetCodeFragment/#function-getspellingrange)**() =0<br>Get the spelling source range.  |
| clang::OpenMPDirectiveKind | **[getTargetCodeKind](Classes/classTargetCodeFragment/#function-gettargetcodekind)**()<br>Accessor to TargetCodeKind.  |
| const clang::LangOptions & | **[GetLangOpts](Classes/classTargetCodeFragment/#function-getlangopts)**()<br>Accessor to lang opts of the current context.  |
| clang::PrintingPolicy | **[getPP](Classes/classTargetCodeFragment/#function-getpp)**() |
| bool | **[classof](Classes/classTargetCodeFragment/#function-classof)**(const [TargetCodeFragment](Classes/classTargetCodeFragment/) * TCF) |

## Public Attributes

|                | Name           |
| -------------- | -------------- |
| bool | **[NeedsSemicolon](Classes/classTargetCodeFragment/#variable-needssemicolon)** <br>Does the source code generation need to add a semicolon to this fragment.  |
| clang::OpenMPDirectiveKind | **[TargetCodeKind](Classes/classTargetCodeFragment/#variable-targetcodekind)** <br>What kind of code are we copying.  |
| bool | **[HasExtraBraces](Classes/classTargetCodeFragment/#variable-hasextrabraces)**  |

## Protected Attributes

|                | Name           |
| -------------- | -------------- |
| const [TargetCodeFragmentKind](Classes/classTargetCodeFragment/#enum-targetcodefragmentkind) | **[Kind](Classes/classTargetCodeFragment/#variable-kind)** <br>Variable for LLVMs RTTI.  |
| clang::ASTContext & | **[Context](Classes/classTargetCodeFragment/#variable-context)**  |
| clang::PrintingPolicy | **[PP](Classes/classTargetCodeFragment/#variable-pp)**  |

## Detailed Description

```cpp
class TargetCodeFragment;
```

An abstract base class for all fragments of the original code (except header includes) that need to be copied to our generated source code. 

This includes target regions as well as functions, global variables and types used by target regions (as far as we can detect that) as well as functions and variables that are flagged with the 'omp declare target' pragma. 

## Public Types Documentation

### enum TargetCodeFragmentKind

| Enumerator | Value | Description |
| ---------- | ----- | ----------- |
| TCFK_TargetCodeFragment | |   |
| TCFK_TargetCodeRegion | |   |
| TCFK_TargetCodeDecl | |   |



Enum for LLVMs RTTI. 

## Public Functions Documentation

### function getKind

```cpp
inline TargetCodeFragmentKind getKind() const
```

Accessor for LLVMs RTTI. 

### function TargetCodeFragment

```cpp
inline TargetCodeFragment(
    clang::ASTContext & Context,
    TargetCodeFragmentKind Kind
)
```


### function ~TargetCodeFragment

```cpp
virtual ~TargetCodeFragment() =0
```


### function PrintPretty

```cpp
virtual std::string PrintPretty() =0
```

Tries to use Clang's PrettyPrinter when possible (this is currently only for target regions). 

**Reimplemented by**: [TargetCodeRegion::PrintPretty](Classes/classTargetCodeRegion/#function-printpretty), [TargetCodeDecl::PrintPretty](Classes/classTargetCodeDecl/#function-printpretty)


### function getRealRange

```cpp
virtual clang::SourceRange getRealRange() =0
```

Get the source range of the fragment. 

**Reimplemented by**: [TargetCodeRegion::getRealRange](Classes/classTargetCodeRegion/#function-getrealrange), [TargetCodeDecl::getRealRange](Classes/classTargetCodeDecl/#function-getrealrange)


### function getInnerRange

```cpp
inline virtual clang::SourceRange getInnerRange()
```

Gets the 'inner' source range. 

**Reimplemented by**: [TargetCodeRegion::getInnerRange](Classes/classTargetCodeRegion/#function-getinnerrange)


This can differ for target regions from the source range. 


### function getSpellingRange

```cpp
virtual clang::SourceRange getSpellingRange() =0
```

Get the spelling source range. 

**Reimplemented by**: [TargetCodeRegion::getSpellingRange](Classes/classTargetCodeRegion/#function-getspellingrange), [TargetCodeDecl::getSpellingRange](Classes/classTargetCodeDecl/#function-getspellingrange)


That is the range without macro expansions. 


### function getTargetCodeKind

```cpp
inline clang::OpenMPDirectiveKind getTargetCodeKind()
```

Accessor to TargetCodeKind. 

### function GetLangOpts

```cpp
inline const clang::LangOptions & GetLangOpts()
```

Accessor to lang opts of the current context. 

### function getPP

```cpp
inline clang::PrintingPolicy getPP()
```


### function classof

```cpp
static inline bool classof(
    const TargetCodeFragment * TCF
)
```


## Public Attributes Documentation

### variable NeedsSemicolon

```cpp
bool NeedsSemicolon;
```

Does the source code generation need to add a semicolon to this fragment. 

### variable TargetCodeKind

```cpp
clang::OpenMPDirectiveKind TargetCodeKind;
```

What kind of code are we copying. 

TODO: this can create problems with non annotated function? 


### variable HasExtraBraces

```cpp
bool HasExtraBraces;
```


## Protected Attributes Documentation

### variable Kind

```cpp
const TargetCodeFragmentKind Kind;
```

Variable for LLVMs RTTI. 

### variable Context

```cpp
clang::ASTContext & Context;
```


### variable PP

```cpp
clang::PrintingPolicy PP;
```


