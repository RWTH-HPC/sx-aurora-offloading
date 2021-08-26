# Classes




* **class [CollectOMPClauseParamsVarsVisitor](Classes/classCollectOMPClauseParamsVarsVisitor.md)** 
* **class [CollectOMPClauseParamsVisitor](Classes/classCollectOMPClauseParamsVisitor.md)** 
* **struct [DeclInfo](Classes/structDeclInfo.md)** <br>Records information to resolve a single declaration, including if its declared in a system header and other declaration that this declaration depends on. 
* **class [DeclResolver](Classes/classDeclResolver.md)** <br>Records, orders and finds the dependencies of Decls (TypeDecls or FunctionDecls) 
* **class [DiscoverFunctionsInDeclVisitor](Classes/classDiscoverFunctionsInDeclVisitor.md)** <br>Traverses (parts of) the AST to find DeclRefExpr that refer to functions that need to be present for that part of the AST to compile correctly. 
* **class [DiscoverTypesInDeclVisitor](Classes/classDiscoverTypesInDeclVisitor.md)** <br>Traverses (parts of) the AST to find DeclRefExpr that refer to types that need to be present for that part of the AST to compile correctly. 
* **class [FindArraySectionVisitor](Classes/classFindArraySectionVisitor.md)** 
* **class [FindDeclRefExprVisitor](Classes/classFindDeclRefExprVisitor.md)** 
* **class [FindLoopStmtVisitor](Classes/classFindLoopStmtVisitor.md)** 
* **class [FindPrivateVariablesVisitor](Classes/classFindPrivateVariablesVisitor.md)** 
* **class [FindTargetCodeVisitor](Classes/classFindTargetCodeVisitor.md)** <br>Traverses the AST to find target and process target regions and function and variables that are annotated by an 'omp declare target' target pragma. 
* **class [FunctionDeclResolver](Classes/classFunctionDeclResolver.md)** <br>Implements [DeclResolver]() for functions used in target regions. 
* **class [OmpPragma](Classes/classOmpPragma.md)** <br>A helper class to rewrite some "pragma omp" (mostly teams and similar combined constructs), which are not supported by sotoc. 
* **class [SourceTransformAction](Classes/classSourceTransformAction.md)** 
* **class [TargetCode](Classes/classTargetCode.md)** <br>A collection of all code from the input file that needs to be copied to the target source file. 
* **class [TargetCodeDecl](Classes/classTargetCodeDecl.md)** <br>This class represents a declaration, i.e. 
* **class [TargetCodeFragment](Classes/classTargetCodeFragment.md)** <br>An abstract base class for all fragments of the original code (except header includes) that need to be copied to our generated source code. 
* **class [TargetCodeRegion](Classes/classTargetCodeRegion.md)** <br>Represents one target region. 
* **class [TargetRegionPrinterHelper](Classes/classTargetRegionPrinterHelper.md)** 
* **class [TargetRegionTransformer](Classes/classTargetRegionTransformer.md)** 
* **class [TargetRegionVariable](Classes/classTargetRegionVariable.md)** <br>Represents a variable captured by a target region. 
    * **class [shape_const_kind_iterator](Classes/classTargetRegionVariable_1_1shape__const__kind__iterator.md)** <br>Iterator which acts as a filter over std::vector<TargetRegionVariableShape>::const_iterator (the base_iter) which only passes on [TargetRegionVariableShape](Classes/classTargetRegionVariableShape.md) of the kind specified in [Kind](). 
* **class [TargetRegionVariableShape](Classes/classTargetRegionVariableShape.md)** <br>Describes the shape, i.e. 
* **class [TypeDeclResolver](Classes/classTypeDeclResolver.md)** <br>Implements [DeclResolver]() for types (typedefs, structs enums) used in target regions. 
* **namespace [clang](Namespaces/namespaceclang.md)** 
* **namespace [clang::tooling](Namespaces/namespaceclang_1_1tooling.md)** 
* **namespace [llvm](Namespaces/namespacellvm.md)** 




