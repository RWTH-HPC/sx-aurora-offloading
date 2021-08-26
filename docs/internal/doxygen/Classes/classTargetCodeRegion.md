# TargetCodeRegion



Represents one target region. 


`#include <TargetCodeFragment.h>`

Inherits from [TargetCodeFragment](Classes/classTargetCodeFragment/)

## Public Types

|                | Name           |
| -------------- | -------------- |
| using std::vector< [TargetRegionVariable](Classes/classTargetRegionVariable/) >::const_iterator | **[captured_vars_const_iterator](Classes/classTargetCodeRegion/#using-captured_vars_const_iterator)**  |
| using llvm::iterator_range< [captured_vars_const_iterator](Classes/classTargetCodeRegion/#using-captured_vars_const_iterator) > | **[captured_vars_const_range](Classes/classTargetCodeRegion/#using-captured_vars_const_range)**  |
| using std::set< clang::VarDecl * >::const_iterator | **[private_vars_const_iterator](Classes/classTargetCodeRegion/#using-private_vars_const_iterator)**  |
| using llvm::iterator_range< [private_vars_const_iterator](Classes/classTargetCodeRegion/#using-private_vars_const_iterator) > | **[private_vars_const_range](Classes/classTargetCodeRegion/#using-private_vars_const_range)**  |
| using std::vector< clang::VarDecl * >::const_iterator | **[ompclauses_params_const_iterator](Classes/classTargetCodeRegion/#using-ompclauses_params_const_iterator)**  |
| using llvm::iterator_range< [ompclauses_params_const_iterator](Classes/classTargetCodeRegion/#using-ompclauses_params_const_iterator) > | **[ompclauses_params_const_range](Classes/classTargetCodeRegion/#using-ompclauses_params_const_range)**  |

## Public Functions

|                | Name           |
| -------------- | -------------- |
| bool | **[classof](Classes/classTargetCodeRegion/#function-classof)**(const [TargetCodeFragment](Classes/classTargetCodeFragment/) * TCF) |
| | **[TargetCodeRegion](Classes/classTargetCodeRegion/#function-targetcoderegion)**(clang::CapturedStmt * CapturedStmtNode, clang::OMPExecutableDirective * TargetDirective, clang::FunctionDecl * ParentFunctionDecl, clang::ASTContext & Context) |
| void | **[addCapture](Classes/classTargetCodeRegion/#function-addcapture)**(const clang::CapturedStmt::Capture * Capture)<br>Add a captured variable of the target region.  |
| [captured_vars_const_iterator](Classes/classTargetCodeRegion/#using-captured_vars_const_iterator) | **[getCapturedVarsBegin](Classes/classTargetCodeRegion/#function-getcapturedvarsbegin)**() |
| [captured_vars_const_iterator](Classes/classTargetCodeRegion/#using-captured_vars_const_iterator) | **[getCapturedVarsEnd](Classes/classTargetCodeRegion/#function-getcapturedvarsend)**() |
| [captured_vars_const_range](Classes/classTargetCodeRegion/#using-captured_vars_const_range) | **[capturedVars](Classes/classTargetCodeRegion/#function-capturedvars)**() |
| void | **[addOMPClause](Classes/classTargetCodeRegion/#function-addompclause)**(clang::OMPClause * Clause)<br>Adds a (top level) OpenMP clause for the target region.  |
| const std::vector< clang::OMPClause * > & | **[getOMPClauses](Classes/classTargetCodeRegion/#function-getompclauses)**() const |
| void | **[setPrivateVars](Classes/classTargetCodeRegion/#function-setprivatevars)**(const std::set< clang::VarDecl * > & VarSet)<br>Sets the private variables of this target region.  |
| [private_vars_const_range](Classes/classTargetCodeRegion/#using-private_vars_const_range) | **[privateVars](Classes/classTargetCodeRegion/#function-privatevars)**()<br>Returns a range over the private variables of this region.  |
| [ompclauses_params_const_range](Classes/classTargetCodeRegion/#using-ompclauses_params_const_range) | **[ompClausesParams](Classes/classTargetCodeRegion/#function-ompclausesparams)**()<br>Returns a range over the parameters to the top level OpenMP clauses.  |
| void | **[addOMPClauseParam](Classes/classTargetCodeRegion/#function-addompclauseparam)**(clang::VarDecl * Param)<br>Adds a parameter of a top level OpenMP clause to the target regions function as a function parameter.  |
| bool | **[hasCombineConstruct](Classes/classTargetCodeRegion/#function-hascombineconstruct)**() |
| virtual std::string | **[PrintPretty](Classes/classTargetCodeRegion/#function-printpretty)**() override<br>Tries to use Clang's PrettyPrinter when possible (this is currently only for target regions).  |
| virtual clang::SourceRange | **[getRealRange](Classes/classTargetCodeRegion/#function-getrealrange)**() override<br>Get the source range of the fragment.  |
| virtual clang::SourceRange | **[getInnerRange](Classes/classTargetCodeRegion/#function-getinnerrange)**() override<br>Gets the 'inner' source range.  |
| virtual clang::SourceRange | **[getSpellingRange](Classes/classTargetCodeRegion/#function-getspellingrange)**() override<br>Get the spelling source range.  |
| clang::SourceLocation | **[getStartLoc](Classes/classTargetCodeRegion/#function-getstartloc)**()<br>Returns a source location at the start of a pragma in the captured statment.  |
| clang::SourceLocation | **[getEndLoc](Classes/classTargetCodeRegion/#function-getendloc)**() |
| const std::string | **[getParentFuncName](Classes/classTargetCodeRegion/#function-getparentfuncname)**()<br>Returns the name of the function in which the target region is declared.  |
| clang::SourceLocation | **[getTargetDirectiveLocation](Classes/classTargetCodeRegion/#function-gettargetdirectivelocation)**()<br>Returns the SourceLocation for the target directive (we need the source location of the first pragma of the target region to compose the name of the function generated for that region)  |

## Public Attributes

|                | Name           |
| -------------- | -------------- |
| std::map< clang::VarDecl *, clang::Expr * > | **[CapturedLowerBounds](Classes/classTargetCodeRegion/#variable-capturedlowerbounds)** <br>Lower bounds of mapped array slices (if lower then 0).  |

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


## Public Types Documentation

### using captured_vars_const_iterator

```cpp
using TargetCodeRegion::captured_vars_const_iterator =  std::vector<TargetRegionVariable>::const_iterator;
```


### using captured_vars_const_range

```cpp
using TargetCodeRegion::captured_vars_const_range =  llvm::iterator_range<captured_vars_const_iterator>;
```


### using private_vars_const_iterator

```cpp
using TargetCodeRegion::private_vars_const_iterator =  std::set<clang::VarDecl *>::const_iterator;
```


### using private_vars_const_range

```cpp
using TargetCodeRegion::private_vars_const_range =  llvm::iterator_range<private_vars_const_iterator>;
```


### using ompclauses_params_const_iterator

```cpp
using TargetCodeRegion::ompclauses_params_const_iterator =  std::vector<clang::VarDecl *>::const_iterator;
```


### using ompclauses_params_const_range

```cpp
using TargetCodeRegion::ompclauses_params_const_range =  llvm::iterator_range<ompclauses_params_const_iterator>;
```


## Public Functions Documentation

### function classof

```cpp
static inline bool classof(
    const TargetCodeFragment * TCF
)
```


### function TargetCodeRegion

```cpp
inline TargetCodeRegion(
    clang::CapturedStmt * CapturedStmtNode,
    clang::OMPExecutableDirective * TargetDirective,
    clang::FunctionDecl * ParentFunctionDecl,
    clang::ASTContext & Context
)
```


### function addCapture

```cpp
void addCapture(
    const clang::CapturedStmt::Capture * Capture
)
```

Add a captured variable of the target region. 

This will automatically create and save a [TargetRegionVariable](Classes/classTargetRegionVariable/) which holds all information to generate parameters for the generated target region function. 


### function getCapturedVarsBegin

```cpp
inline captured_vars_const_iterator getCapturedVarsBegin()
```


### function getCapturedVarsEnd

```cpp
inline captured_vars_const_iterator getCapturedVarsEnd()
```


### function capturedVars

```cpp
inline captured_vars_const_range capturedVars()
```


### function addOMPClause

```cpp
void addOMPClause(
    clang::OMPClause * Clause
)
```

Adds a (top level) OpenMP clause for the target region. 

These clauses are later used to determine which OpenMP #pragma needs to be generated at the top level of the target region function. 


### function getOMPClauses

```cpp
inline const std::vector< clang::OMPClause * > & getOMPClauses() const
```


### function setPrivateVars

```cpp
inline void setPrivateVars(
    const std::set< clang::VarDecl * > & VarSet
)
```

Sets the private variables of this target region. 

### function privateVars

```cpp
inline private_vars_const_range privateVars()
```

Returns a range over the private variables of this region. 

### function ompClausesParams

```cpp
inline ompclauses_params_const_range ompClausesParams()
```

Returns a range over the parameters to the top level OpenMP clauses. 

### function addOMPClauseParam

```cpp
void addOMPClauseParam(
    clang::VarDecl * Param
)
```

Adds a parameter of a top level OpenMP clause to the target regions function as a function parameter. 

### function hasCombineConstruct

```cpp
inline bool hasCombineConstruct()
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


### function getInnerRange

```cpp
virtual clang::SourceRange getInnerRange() override
```

Gets the 'inner' source range. 

**Reimplements**: [TargetCodeFragment::getInnerRange](Classes/classTargetCodeFragment/#function-getinnerrange)


This can differ for target regions from the source range. 


### function getSpellingRange

```cpp
virtual clang::SourceRange getSpellingRange() override
```

Get the spelling source range. 

**Reimplements**: [TargetCodeFragment::getSpellingRange](Classes/classTargetCodeFragment/#function-getspellingrange)


That is the range without macro expansions. 


### function getStartLoc

```cpp
clang::SourceLocation getStartLoc()
```

Returns a source location at the start of a pragma in the captured statment. 

### function getEndLoc

```cpp
clang::SourceLocation getEndLoc()
```


### function getParentFuncName

```cpp
const std::string getParentFuncName()
```

Returns the name of the function in which the target region is declared. 

### function getTargetDirectiveLocation

```cpp
clang::SourceLocation getTargetDirectiveLocation()
```

Returns the SourceLocation for the target directive (we need the source location of the first pragma of the target region to compose the name of the function generated for that region) 

## Public Attributes Documentation

### variable CapturedLowerBounds

```cpp
std::map< clang::VarDecl *, clang::Expr * > CapturedLowerBounds;
```

Lower bounds of mapped array slices (if lower then 0). 

If the captured variable is an array, of which only a slice is mapped (by a map() clause), the incoming pointer argument will need to be shifted to the right if the lower bound of that slice is not 0. If this is the case, the lower bound is saved into this map. 


