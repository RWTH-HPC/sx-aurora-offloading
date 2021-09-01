# TargetRegionTransformer





Inherits from ASTConsumer

## Public Functions

|                | Name           |
| -------------- | -------------- |
| | **[TargetRegionTransformer](../Classes/classTargetRegionTransformer.md#function-targetregiontransformer)**([TargetCode](../Classes/classTargetCode.md) & Code, clang::Rewriter & TargetCodeRewriter) |
| void | **[HandleTranslationUnit](../Classes/classTargetRegionTransformer.md#function-handletranslationunit)**(clang::ASTContext & Context) |

## Private Attributes

|                | Name           |
| -------------- | -------------- |
| [TargetCode](../Classes/classTargetCode.md) & | **[Code](../Classes/classTargetRegionTransformer.md#variable-code)**  |
| clang::Rewriter & | **[TargetCodeRewriter](../Classes/classTargetRegionTransformer.md#variable-targetcoderewriter)**  |

## Public Functions Documentation

### function TargetRegionTransformer

```cpp linenums="1"
inline TargetRegionTransformer(
    TargetCode & Code,
    clang::Rewriter & TargetCodeRewriter
)
```


### function HandleTranslationUnit

```cpp linenums="1"
inline void HandleTranslationUnit(
    clang::ASTContext & Context
)
```


## Private Attributes Documentation

### variable Code

```cpp linenums="1"
TargetCode & Code;
```


### variable TargetCodeRewriter

```cpp linenums="1"
clang::Rewriter & TargetCodeRewriter;
```


