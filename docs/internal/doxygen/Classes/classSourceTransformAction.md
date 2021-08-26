# SourceTransformAction





Inherits from ASTFrontendAction

## Public Functions

|                | Name           |
| -------------- | -------------- |
| void | **[EndSourceFileAction](Classes/classSourceTransformAction/#function-endsourcefileaction)**() override |
| std::unique_ptr< clang::ASTConsumer > | **[CreateASTConsumer](Classes/classSourceTransformAction/#function-createastconsumer)**(clang::CompilerInstance & CI, clang::StringRef ) |

## Public Functions Documentation

### function EndSourceFileAction

```cpp
inline void EndSourceFileAction() override
```


### function CreateASTConsumer

```cpp
inline std::unique_ptr< clang::ASTConsumer > CreateASTConsumer(
    clang::CompilerInstance & CI,
    clang::StringRef 
)
```


