# SourceTransformAction





Inherits from ASTFrontendAction

## Public Functions

|                | Name           |
| -------------- | -------------- |
| void | **[EndSourceFileAction](../Classes/classSourceTransformAction.md#function-endsourcefileaction)**() override |
| std::unique_ptr< clang::ASTConsumer > | **[CreateASTConsumer](../Classes/classSourceTransformAction.md#function-createastconsumer)**(clang::CompilerInstance & CI, clang::StringRef ) |

## Private Attributes

|                | Name           |
| -------------- | -------------- |
| clang::Rewriter | **[TargetCodeRewriter](../Classes/classSourceTransformAction.md#variable-targetcoderewriter)**  |
| [TargetCode](../Classes/classTargetCode.md) * | **[Code](../Classes/classSourceTransformAction.md#variable-code)**  |

## Public Functions Documentation

### function EndSourceFileAction

```cpp linenums="1"
inline void EndSourceFileAction() override
```


### function CreateASTConsumer

```cpp linenums="1"
inline std::unique_ptr< clang::ASTConsumer > CreateASTConsumer(
    clang::CompilerInstance & CI,
    clang::StringRef
)
```


## Private Attributes Documentation

### variable TargetCodeRewriter

```cpp linenums="1"
clang::Rewriter TargetCodeRewriter;
```


### variable Code

```cpp linenums="1"
TargetCode * Code;
```


