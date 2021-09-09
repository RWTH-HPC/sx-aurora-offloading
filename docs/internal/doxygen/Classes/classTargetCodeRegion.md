# TargetCodeRegion



Represents one target region. 


`#include <TargetCodeFragment.h>`

Inherits from [TargetCodeFragment](../Classes/classTargetCodeFragment.md)

## Public Types

|                | Name           |
| -------------- | -------------- |
| using std::vector< [TargetRegionVariable](../Classes/classTargetRegionVariable.md) >::const_iterator | **[captured_vars_const_iterator](../Classes/classTargetCodeRegion.md#using-captured_vars_const_iterator)**  |
| using llvm::iterator_range< [captured_vars_const_iterator](../Classes/classTargetCodeRegion.md#using-captured_vars_const_iterator) > | **[captured_vars_const_range](../Classes/classTargetCodeRegion.md#using-captured_vars_const_range)**  |
| using std::set< clang::VarDecl * >::const_iterator | **[private_vars_const_iterator](../Classes/classTargetCodeRegion.md#using-private_vars_const_iterator)**  |
| using llvm::iterator_range< [private_vars_const_iterator](../Classes/classTargetCodeRegion.md#using-private_vars_const_iterator) > | **[private_vars_const_range](../Classes/classTargetCodeRegion.md#using-private_vars_const_range)**  |
| using std::vector< clang::VarDecl * >::const_iterator | **[ompclauses_params_const_iterator](../Classes/classTargetCodeRegion.md#using-ompclauses_params_const_iterator)**  |
| using llvm::iterator_range< [ompclauses_params_const_iterator](../Classes/classTargetCodeRegion.md#using-ompclauses_params_const_iterator) > | **[ompclauses_params_const_range](../Classes/classTargetCodeRegion.md#using-ompclauses_params_const_range)**  |

## Public Functions

|                | Name           |
| -------------- | -------------- |
| bool | **[classof](../Classes/classTargetCodeRegion.md#function-classof)**(const [TargetCodeFragment](../Classes/classTargetCodeFragment.md) * TCF) |
| | **[TargetCodeRegion](../Classes/classTargetCodeRegion.md#function-targetcoderegion)**(clang::CapturedStmt * CapturedStmtNode, clang::OMPExecutableDirective * TargetDirective, clang::FunctionDecl * ParentFunctionDecl, clang::ASTContext & Context) |
| void | **[addCapture](../Classes/classTargetCodeRegion.md#function-addcapture)**(const clang::CapturedStmt::Capture * Capture)<br>Add a captured variable of the target region.  |
| [captured_vars_const_iterator](../Classes/classTargetCodeRegion.md#using-captured_vars_const_iterator) | **[getCapturedVarsBegin](../Classes/classTargetCodeRegion.md#function-getcapturedvarsbegin)**() |
| [captured_vars_const_iterator](../Classes/classTargetCodeRegion.md#using-captured_vars_const_iterator) | **[getCapturedVarsEnd](../Classes/classTargetCodeRegion.md#function-getcapturedvarsend)**() |
| [captured_vars_const_range](../Classes/classTargetCodeRegion.md#using-captured_vars_const_range) | **[capturedVars](../Classes/classTargetCodeRegion.md#function-capturedvars)**() |
| void | **[addOMPClause](../Classes/classTargetCodeRegion.md#function-addompclause)**(clang::OMPClause * Clause)<br>Adds a (top level) OpenMP clause for the target region.  |
| const std::vector< clang::OMPClause * > & | **[getOMPClauses](../Classes/classTargetCodeRegion.md#function-getompclauses)**() const |
| void | **[setPrivateVars](../Classes/classTargetCodeRegion.md#function-setprivatevars)**(const std::set< clang::VarDecl * > & VarSet)<br>Sets the private variables of this target region.  |
| [private_vars_const_range](../Classes/classTargetCodeRegion.md#using-private_vars_const_range) | **[privateVars](../Classes/classTargetCodeRegion.md#function-privatevars)**()<br>Returns a range over the private variables of this region.  |
| [ompclauses_params_const_range](../Classes/classTargetCodeRegion.md#using-ompclauses_params_const_range) | **[ompClausesParams](../Classes/classTargetCodeRegion.md#function-ompclausesparams)**()<br>Returns a range over the parameters to the top level OpenMP clauses.  |
| void | **[addOMPClauseParam](../Classes/classTargetCodeRegion.md#function-addompclauseparam)**(clang::VarDecl * Param)<br>Adds a parameter of a top level OpenMP clause to the target regions function as a function parameter.  |
| bool | **[hasCombineConstruct](../Classes/classTargetCodeRegion.md#function-hascombineconstruct)**() |
| virtual std::string | **[PrintPretty](../Classes/classTargetCodeRegion.md#function-printpretty)**() override<br>Do pretty printing in order to resolve Macros.  |
| virtual clang::SourceRange | **[getRealRange](../Classes/classTargetCodeRegion.md#function-getrealrange)**() override<br>Get source range.  |
| virtual clang::SourceRange | **[getInnerRange](../Classes/classTargetCodeRegion.md#function-getinnerrange)**() override<br>Get inner range.  |
| virtual clang::SourceRange | **[getSpellingRange](../Classes/classTargetCodeRegion.md#function-getspellingrange)**() override<br>Get spelling range.  |
| clang::SourceLocation | **[getStartLoc](../Classes/classTargetCodeRegion.md#function-getstartloc)**()<br>Returns a source location at the start of a pragma in the captured statement.  |
| clang::SourceLocation | **[getEndLoc](../Classes/classTargetCodeRegion.md#function-getendloc)**()<br>Get end location.  |
| const std::string | **[getParentFuncName](../Classes/classTargetCodeRegion.md#function-getparentfuncname)**()<br>Returns the name of the function in which the target region is declared.  |
| clang::SourceLocation | **[getTargetDirectiveLocation](../Classes/classTargetCodeRegion.md#function-gettargetdirectivelocation)**()<br>Returns the SourceLocation for the target directive (we need the source location of the first pragma of the target region to compose the name of the function generated for that region)  |

## Public Attributes

|                | Name           |
| -------------- | -------------- |
| std::map< clang::VarDecl *, clang::Expr * > | **[CapturedLowerBounds](../Classes/classTargetCodeRegion.md#variable-capturedlowerbounds)** <br>Lower bounds of mapped array slices (if lower then 0).  |

## Private Attributes

|                | Name           |
| -------------- | -------------- |
| clang::CapturedStmt * | **[CapturedStmtNode](../Classes/classTargetCodeRegion.md#variable-capturedstmtnode)** <br>The AST node for the captured statement of the target region.  |
| clang::OMPExecutableDirective * | **[TargetDirective](../Classes/classTargetCodeRegion.md#variable-targetdirective)** <br>AST node for the target directive.  |
| clang::FunctionDecl * | **[ParentFunctionDecl](../Classes/classTargetCodeRegion.md#variable-parentfunctiondecl)** <br>Declaration of the function this region is declared in.  |
| std::vector< [TargetRegionVariable](../Classes/classTargetRegionVariable.md) > | **[CapturedVars](../Classes/classTargetCodeRegion.md#variable-capturedvars)** <br>All variable captured by this target region.  |
| std::vector< clang::OMPClause * > | **[OMPClauses](../Classes/classTargetCodeRegion.md#variable-ompclauses)** <br>All omp clauses relevant to the execution of the region.  |
| std::vector< clang::VarDecl * > | **[OMPClausesParams](../Classes/classTargetCodeRegion.md#variable-ompclausesparams)** <br>The variables which are parameters for top level OpenMP clauses.  |
| std::set< clang::VarDecl * > | **[PrivateVars](../Classes/classTargetCodeRegion.md#variable-privatevars)** <br>All private variables in a Target Region i.e.  |

## Additional inherited members

**Public Types inherited from [TargetCodeFragment](../Classes/classTargetCodeFragment.md)**

|                | Name           |
| -------------- | -------------- |
| enum| **[TargetCodeFragmentKind](../Classes/classTargetCodeFragment.md#enum-targetcodefragmentkind)** { TCFK_TargetCodeFragment, TCFK_TargetCodeRegion, TCFK_TargetCodeDecl}<br>Enum for LLVMs RTTI.  |

**Public Functions inherited from [TargetCodeFragment](../Classes/classTargetCodeFragment.md)**

|                | Name           |
| -------------- | -------------- |
| [TargetCodeFragmentKind](../Classes/classTargetCodeFragment.md#enum-targetcodefragmentkind) | **[getKind](../Classes/classTargetCodeFragment.md#function-getkind)**() const<br>Accessor for LLVMs RTTI.  |
| | **[TargetCodeFragment](../Classes/classTargetCodeFragment.md#function-targetcodefragment)**(clang::ASTContext & Context, [TargetCodeFragmentKind](../Classes/classTargetCodeFragment.md#enum-targetcodefragmentkind) Kind) |
| virtual | **[~TargetCodeFragment](../Classes/classTargetCodeFragment.md#function-~targetcodefragment)**() =0<br>Destroy the Target Code Fragment:: Target Code Fragment object.  |
| clang::OpenMPDirectiveKind | **[getTargetCodeKind](../Classes/classTargetCodeFragment.md#function-gettargetcodekind)**()<br>Accessor to TargetCodeKind.  |
| const clang::LangOptions & | **[GetLangOpts](../Classes/classTargetCodeFragment.md#function-getlangopts)**()<br>Accessor to lang opts of the current context.  |
| clang::PrintingPolicy | **[getPP](../Classes/classTargetCodeFragment.md#function-getpp)**() |

**Public Attributes inherited from [TargetCodeFragment](../Classes/classTargetCodeFragment.md)**

|                | Name           |
| -------------- | -------------- |
| bool | **[NeedsSemicolon](../Classes/classTargetCodeFragment.md#variable-needssemicolon)** <br>Does the source code generation need to add a semicolon to this fragment.  |
| clang::OpenMPDirectiveKind | **[TargetCodeKind](../Classes/classTargetCodeFragment.md#variable-targetcodekind)** <br>What kind of code are we copying.  |
| bool | **[HasExtraBraces](../Classes/classTargetCodeFragment.md#variable-hasextrabraces)**  |

**Protected Attributes inherited from [TargetCodeFragment](../Classes/classTargetCodeFragment.md)**

|                | Name           |
| -------------- | -------------- |
| const [TargetCodeFragmentKind](../Classes/classTargetCodeFragment.md#enum-targetcodefragmentkind) | **[Kind](../Classes/classTargetCodeFragment.md#variable-kind)** <br>Variable for LLVMs RTTI.  |
| clang::ASTContext & | **[Context](../Classes/classTargetCodeFragment.md#variable-context)**  |
| clang::PrintingPolicy | **[PP](../Classes/classTargetCodeFragment.md#variable-pp)**  |


## Public Types Documentation

### using captured_vars_const_iterator

```cpp linenums="1"
using TargetCodeRegion::captured_vars_const_iterator =  std::vector<TargetRegionVariable>::const_iterator;
```


### using captured_vars_const_range

```cpp linenums="1"
using TargetCodeRegion::captured_vars_const_range =  llvm::iterator_range<captured_vars_const_iterator>;
```


### using private_vars_const_iterator

```cpp linenums="1"
using TargetCodeRegion::private_vars_const_iterator =  std::set<clang::VarDecl *>::const_iterator;
```


### using private_vars_const_range

```cpp linenums="1"
using TargetCodeRegion::private_vars_const_range =  llvm::iterator_range<private_vars_const_iterator>;
```


### using ompclauses_params_const_iterator

```cpp linenums="1"
using TargetCodeRegion::ompclauses_params_const_iterator =  std::vector<clang::VarDecl *>::const_iterator;
```


### using ompclauses_params_const_range

```cpp linenums="1"
using TargetCodeRegion::ompclauses_params_const_range =  llvm::iterator_range<ompclauses_params_const_iterator>;
```


## Public Functions Documentation

### function classof

```cpp linenums="1"
static inline bool classof(
    const TargetCodeFragment * TCF
)
```


### function TargetCodeRegion

```cpp linenums="1"
inline TargetCodeRegion(
    clang::CapturedStmt * CapturedStmtNode,
    clang::OMPExecutableDirective * TargetDirective,
    clang::FunctionDecl * ParentFunctionDecl,
    clang::ASTContext & Context
)
```


### function addCapture

```cpp linenums="1"
void addCapture(
    const clang::CapturedStmt::Capture * Capture
)
```

Add a captured variable of the target region. 

**Parameters**: 

  * **Capture** Captures element 


Add capture.

This will automatically create and save a [TargetRegionVariable](../Classes/classTargetRegionVariable.md) which holds all information to generate parameters for the generated target region function.

This will automatically create and save a [TargetRegionVariable](../Classes/classTargetRegionVariable.md) which holds all information to generate parameters for the generated target region function.


### function getCapturedVarsBegin

```cpp linenums="1"
inline captured_vars_const_iterator getCapturedVarsBegin()
```


### function getCapturedVarsEnd

```cpp linenums="1"
inline captured_vars_const_iterator getCapturedVarsEnd()
```


### function capturedVars

```cpp linenums="1"
inline captured_vars_const_range capturedVars()
```


### function addOMPClause

```cpp linenums="1"
void addOMPClause(
    clang::OMPClause * Clause
)
```

Adds a (top level) OpenMP clause for the target region. 

**Parameters**: 

  * **Clause** OMP Clause 


Add OMP clauses.

These clauses are later used to determine which OpenMP #pragma needs to be generated at the top level of the target region function.

Adds a (top level) OpenMP clause for the target region. These clauses are later used to determine which OpenMP #pragma needs to be generated at the top level of the target region function.


### function getOMPClauses

```cpp linenums="1"
inline const std::vector< clang::OMPClause * > & getOMPClauses() const
```


### function setPrivateVars

```cpp linenums="1"
inline void setPrivateVars(
    const std::set< clang::VarDecl * > & VarSet
)
```

Sets the private variables of this target region. 

### function privateVars

```cpp linenums="1"
inline private_vars_const_range privateVars()
```

Returns a range over the private variables of this region. 

### function ompClausesParams

```cpp linenums="1"
inline ompclauses_params_const_range ompClausesParams()
```

Returns a range over the parameters to the top level OpenMP clauses. 

### function addOMPClauseParam

```cpp linenums="1"
void addOMPClauseParam(
    clang::VarDecl * Param
)
```

Adds a parameter of a top level OpenMP clause to the target regions function as a function parameter. 

**Parameters**: 

  * **Param** Parameter 


Add OMP clause parameters.

Adds OMP clause paramenters to a [TargetCodeRegion](../Classes/classTargetCodeRegion.md)


### function hasCombineConstruct

```cpp linenums="1"
inline bool hasCombineConstruct()
```


### function PrintPretty

```cpp linenums="1"
virtual std::string PrintPretty() override
```

Do pretty printing in order to resolve Macros. 

**Return**: std::string Pretty output 

**Reimplements**: [TargetCodeFragment::PrintPretty](../Classes/classTargetCodeFragment.md#function-printpretty)


### function getRealRange

```cpp linenums="1"
virtual clang::SourceRange getRealRange() override
```

Get source range. 

**Return**: clang::SourceRange 

**Reimplements**: [TargetCodeFragment::getRealRange](../Classes/classTargetCodeFragment.md#function-getrealrange)


### function getInnerRange

```cpp linenums="1"
virtual clang::SourceRange getInnerRange() override
```

Get inner range. 

**Return**: clang::SourceRange 

**Reimplements**: [TargetCodeFragment::getInnerRange](../Classes/classTargetCodeFragment.md#function-getinnerrange)


### function getSpellingRange

```cpp linenums="1"
virtual clang::SourceRange getSpellingRange() override
```

Get spelling range. 

**Return**: clang::SourceRange 

**Reimplements**: [TargetCodeFragment::getSpellingRange](../Classes/classTargetCodeFragment.md#function-getspellingrange)


### function getStartLoc

```cpp linenums="1"
clang::SourceLocation getStartLoc()
```

Returns a source location at the start of a pragma in the captured statement. 

**Return**: clang::SourceLocation Start location 

### function getEndLoc

```cpp linenums="1"
clang::SourceLocation getEndLoc()
```

Get end location. 

**Return**: clang::SourceLocation End location 

### function getParentFuncName

```cpp linenums="1"
const std::string getParentFuncName()
```

Returns the name of the function in which the target region is declared. 

**Return**: const std::string 

### function getTargetDirectiveLocation

```cpp linenums="1"
clang::SourceLocation getTargetDirectiveLocation()
```

Returns the SourceLocation for the target directive (we need the source location of the first pragma of the target region to compose the name of the function generated for that region) 

**Return**: clang::SourceLocation Location 

Get target directive location.

Returns the SourceLocation for the target directive (we need the source location of the first pragma of the target region to compose the name of the function generated for that region)


## Public Attributes Documentation

### variable CapturedLowerBounds

```cpp linenums="1"
std::map< clang::VarDecl *, clang::Expr * > CapturedLowerBounds;
```

Lower bounds of mapped array slices (if lower then 0). 

If the captured variable is an array, of which only a slice is mapped (by a map() clause), the incoming pointer argument will need to be shifted to the right if the lower bound of that slice is not 0. If this is the case, the lower bound is saved into this map. 


## Private Attributes Documentation

### variable CapturedStmtNode

```cpp linenums="1"
clang::CapturedStmt * CapturedStmtNode;
```

The AST node for the captured statement of the target region. 

### variable TargetDirective

```cpp linenums="1"
clang::OMPExecutableDirective * TargetDirective;
```

AST node for the target directive. 

### variable ParentFunctionDecl

```cpp linenums="1"
clang::FunctionDecl * ParentFunctionDecl;
```

Declaration of the function this region is declared in. 

Necessary to compose the function name of this region in the generated code. 


### variable CapturedVars

```cpp linenums="1"
std::vector< TargetRegionVariable > CapturedVars;
```

All variable captured by this target region. 

We will need to generated pointers to them as arguments to the generated functions and copy the variables into scope. 


### variable OMPClauses

```cpp linenums="1"
std::vector< clang::OMPClause * > OMPClauses;
```

All omp clauses relevant to the execution of the region. 

### variable OMPClausesParams

```cpp linenums="1"
std::vector< clang::VarDecl * > OMPClausesParams;
```

The variables which are parameters for top level OpenMP clauses. 

These are not captured but still needs passed as (first private) arguments to the target region. 


### variable PrivateVars

```cpp linenums="1"
std::set< clang::VarDecl * > PrivateVars;
```

All private variables in a Target Region i.e. 

all variables that are not passed as arguments into the region. For these, we need to generate declarations inside the target region. 



