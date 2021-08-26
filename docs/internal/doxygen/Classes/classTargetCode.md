# TargetCode



A collection of all code from the input file that needs to be copied to the target source file. 


`#include <TargetCode.h>`

## Public Functions

|                | Name           |
| -------------- | -------------- |
| | **[TargetCode](Classes/classTargetCode.md#function-targetcode)**(clang::Rewriter & TargetCodeRewriter) |
| bool | **[addCodeFragment](Classes/classTargetCode.md#function-addcodefragment)**(std::shared_ptr< [TargetCodeFragment](Classes/classTargetCodeFragment.md) > Frag, bool PushFront =false)<br>Add a piece of code from the input file to this collection.  |
| bool | **[addCodeFragmentFront](Classes/classTargetCode.md#function-addcodefragmentfront)**(std::shared_ptr< [TargetCodeFragment](Classes/classTargetCodeFragment.md) > Fag)<br>See [addCodeFragment](Classes/classTargetCode.md#function-addcodefragment).  |
| void | **[generateCode](Classes/classTargetCode.md#function-generatecode)**(llvm::raw_ostream & Out)<br>Generate target code from all fragments and system headers added to this collection.  |
| TargetCodeFragmentDeque::const_iterator | **[getCodeFragmentsBegin](Classes/classTargetCode.md#function-getcodefragmentsbegin)**()<br>Get an iterate over all code fragments in this collection.  |
| TargetCodeFragmentDeque::const_iterator | **[getCodeFragmentsEnd](Classes/classTargetCode.md#function-getcodefragmentsend)**()<br>See [getCodeFragmentsBegin](Classes/classTargetCode.md#function-getcodefragmentsbegin).  |
| void | **[addHeader](Classes/classTargetCode.md#function-addheader)**(const std::string & Header)<br>Add a header file to be included by the target code.  |

## Public Functions Documentation

### function TargetCode

```cpp
inline TargetCode(
    clang::Rewriter & TargetCodeRewriter
)
```


### function addCodeFragment

```cpp
bool addCodeFragment(
    std::shared_ptr< TargetCodeFragment > Frag,
    bool PushFront =false
)
```

Add a piece of code from the input file to this collection. 

This function uses the fragments source location to check wether it was already added and where in the list of code fragments to add it. 


### function addCodeFragmentFront

```cpp
bool addCodeFragmentFront(
    std::shared_ptr< TargetCodeFragment > Fag
)
```

See [addCodeFragment](Classes/classTargetCode.md#function-addcodefragment). 

### function generateCode

```cpp
void generateCode(
    llvm::raw_ostream & Out
)
```

Generate target code from all fragments and system headers added to this collection. 

### function getCodeFragmentsBegin

```cpp
inline TargetCodeFragmentDeque::const_iterator getCodeFragmentsBegin()
```

Get an iterate over all code fragments in this collection. 

### function getCodeFragmentsEnd

```cpp
inline TargetCodeFragmentDeque::const_iterator getCodeFragmentsEnd()
```

See [getCodeFragmentsBegin](Classes/classTargetCode.md#function-getcodefragmentsbegin). 

### function addHeader

```cpp
inline void addHeader(
    const std::string & Header
)
```

Add a header file to be included by the target code. 

