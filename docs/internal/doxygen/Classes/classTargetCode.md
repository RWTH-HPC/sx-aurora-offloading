# TargetCode



A collection of all code from the input file that needs to be copied to the target source file.


`#include <TargetCode.h>`

## Public Functions

|                | Name           |
| -------------- | -------------- |
| | **[TargetCode](../Classes/classTargetCode.md#function-targetcode)**(clang::Rewriter & TargetCodeRewriter) |
| bool | **[addCodeFragment](../Classes/classTargetCode.md#function-addcodefragment)**(std::shared_ptr< [TargetCodeFragment](../Classes/classTargetCodeFragment.md) > Frag, bool PushFront =false)<br>Add a piece of code from the input file to this collection.  |
| bool | **[addCodeFragmentFront](../Classes/classTargetCode.md#function-addcodefragmentfront)**(std::shared_ptr< [TargetCodeFragment](../Classes/classTargetCodeFragment.md) > Fag)<br>See [addCodeFragment](../Classes/classTargetCode.md#function-addcodefragment).  |
| void | **[generateCode](../Classes/classTargetCode.md#function-generatecode)**(llvm::raw_ostream & Out)<br>Generate target code from all fragments and system headers added to this collection.  |
| TargetCodeFragmentDeque::const_iterator | **[getCodeFragmentsBegin](../Classes/classTargetCode.md#function-getcodefragmentsbegin)**()<br>Get an iterate over all code fragments in this collection.  |
| TargetCodeFragmentDeque::const_iterator | **[getCodeFragmentsEnd](../Classes/classTargetCode.md#function-getcodefragmentsend)**()<br>See [getCodeFragmentsBegin](../Classes/classTargetCode.md#function-getcodefragmentsbegin).  |
| void | **[addHeader](../Classes/classTargetCode.md#function-addheader)**(const std::string & Header)<br>Add a header file to be included by the target code.  |

## Private Functions

|                | Name           |
| -------------- | -------------- |
| void | **[generateVariableDecl](../Classes/classTargetCode.md#function-generatevariabledecl)**(const [TargetRegionVariable](../Classes/classTargetRegionVariable.md) & Var, llvm::raw_ostream & Out)<br>Generate the variable declaration of a transferred variable.  |
| void | **[generateFunctionPrologue](../Classes/classTargetCode.md#function-generatefunctionprologue)**([TargetCodeRegion](../Classes/classTargetCodeRegion.md) * TCR, llvm::raw_ostream & Out)<br>Generates a function prologue for a target region.  |
| void | **[generateFunctionEpilogue](../Classes/classTargetCode.md#function-generatefunctionepilogue)**([TargetCodeRegion](../Classes/classTargetCodeRegion.md) * TCR, llvm::raw_ostream & Out)<br>Generates a function epilogue for a target region.  |
| std::string | **[generateFunctionName](../Classes/classTargetCode.md#function-generatefunctionname)**([TargetCodeRegion](../Classes/classTargetCodeRegion.md) * TCR)<br>Generate a function name for a target region.  |
| void | **[generateArgument](../Classes/classTargetCode.md#function-generateargument)**(const [TargetRegionVariable](../Classes/classTargetRegionVariable.md) & Aarg, llvm::raw_ostream & Out) |

## Private Attributes

|                | Name           |
| -------------- | -------------- |
| [TargetCodeFragmentDeque](../Files/TargetCode_8h.md#using-targetcodefragmentdeque) | **[CodeFragments](../Classes/classTargetCode.md#variable-codefragments)** <br>Collection of all code locations that need to be copied.  |
| std::set< std::string > | **[SystemHeaders](../Classes/classTargetCode.md#variable-systemheaders)** <br>Header files which will also be present on the target.  |
| clang::Rewriter & | **[TargetCodeRewriter](../Classes/classTargetCode.md#variable-targetcoderewriter)**  |
| clang::SourceManager & | **[SM](../Classes/classTargetCode.md#variable-sm)**  |

## Public Functions Documentation

### function TargetCode

```cpp linenums="1"
inline TargetCode(
    clang::Rewriter & TargetCodeRewriter
)
```


### function addCodeFragment

```cpp linenums="1"
bool addCodeFragment(
    std::shared_ptr< TargetCodeFragment > Frag,
    bool PushFront =false
)
```

Add a piece of code from the input file to this collection.

This function uses the fragments source location to check wether it was already added and where in the list of code fragments to add it.


### function addCodeFragmentFront

```cpp linenums="1"
bool addCodeFragmentFront(
    std::shared_ptr< TargetCodeFragment > Fag
)
```

See [addCodeFragment](../Classes/classTargetCode.md#function-addcodefragment).

### function generateCode

```cpp linenums="1"
void generateCode(
    llvm::raw_ostream & Out
)
```

Generate target code from all fragments and system headers added to this collection.

### function getCodeFragmentsBegin

```cpp linenums="1"
inline TargetCodeFragmentDeque::const_iterator getCodeFragmentsBegin()
```

Get an iterate over all code fragments in this collection.

### function getCodeFragmentsEnd

```cpp linenums="1"
inline TargetCodeFragmentDeque::const_iterator getCodeFragmentsEnd()
```

See [getCodeFragmentsBegin](../Classes/classTargetCode.md#function-getcodefragmentsbegin).

### function addHeader

```cpp linenums="1"
inline void addHeader(
    const std::string & Header
)
```

Add a header file to be included by the target code.

## Private Functions Documentation

### function generateVariableDecl

```cpp linenums="1"
void generateVariableDecl(
    const TargetRegionVariable & Var,
    llvm::raw_ostream & Out
)
```

Generate the variable declaration of a transferred variable.

**Parameters**:

  * **Var** The variable for which to print the declaration
  * **Out** The output stream to which to write the variable declaration


Generate the variable declaration (including setting the variable to the proper value) of a transferred variable and print it to the specified output stream.


### function generateFunctionPrologue

```cpp linenums="1"
void generateFunctionPrologue(
    TargetCodeRegion * TCR,
    llvm::raw_ostream & Out
)
```

Generates a function prologue for a target region.

This prologue consists of a function declaration and code to copy local variables into scope.


### function generateFunctionEpilogue

```cpp linenums="1"
void generateFunctionEpilogue(
    TargetCodeRegion * TCR,
    llvm::raw_ostream & Out
)
```

Generates a function epilogue for a target region.

This prologue consists of a code to copy variables from the local scope back.


### function generateFunctionName

```cpp linenums="1"
std::string generateFunctionName(
    TargetCodeRegion * TCR
)
```

Generate a function name for a target region.

### function generateArgument

```cpp linenums="1"
void generateArgument(
    const TargetRegionVariable & Aarg,
    llvm::raw_ostream & Out
)
```


## Private Attributes Documentation

### variable CodeFragments

```cpp linenums="1"
TargetCodeFragmentDeque CodeFragments;
```

Collection of all code locations that need to be copied.

### variable SystemHeaders

```cpp linenums="1"
std::set< std::string > SystemHeaders;
```

Header files which will also be present on the target.

Instead of copying the code declarations in them, we can simply add #include directives for these headers to the target code.


### variable TargetCodeRewriter

```cpp linenums="1"
clang::Rewriter & TargetCodeRewriter;
```


### variable SM

```cpp linenums="1"
clang::SourceManager & SM;
```


