# Classes




* **class [CollectOMPClauseParamsVarsVisitor](Classes/classCollectOMPClauseParamsVarsVisitor/)** 
* **class [CollectOMPClauseParamsVisitor](Classes/classCollectOMPClauseParamsVisitor/)** 
* **struct [DeclInfo](Classes/structDeclInfo/)** <br>Records information to resolve a single declaration, including if its declared in a system header and other declaration that this declaration depends on. 
* **class [DeclResolver](Classes/classDeclResolver/)** <br>Records, orders and finds the dependencies of Decls (TypeDecls or FunctionDecls) 
* **class [DiscoverFunctionsInDeclVisitor](Classes/classDiscoverFunctionsInDeclVisitor/)** <br>Traverses (parts of) the AST to find DeclRefExpr that refer to functions that need to be present for that part of the AST to compile correctly. 
* **class [DiscoverTypesInDeclVisitor](Classes/classDiscoverTypesInDeclVisitor/)** <br>Traverses (parts of) the AST to find DeclRefExpr that refer to types that need to be present for that part of the AST to compile correctly. 
* **class [FindArraySectionVisitor](Classes/classFindArraySectionVisitor/)** 
* **class [FindDeclRefExprVisitor](Classes/classFindDeclRefExprVisitor/)** 
* **class [FindLoopStmtVisitor](Classes/classFindLoopStmtVisitor/)** 
* **class [FindPrivateVariablesVisitor](Classes/classFindPrivateVariablesVisitor/)** 
* **class [FindTargetCodeVisitor](Classes/classFindTargetCodeVisitor/)** <br>Traverses the AST to find target and process target regions and function and variables that are annotated by an 'omp declare target' target pragma. 
* **class [FunctionDeclResolver](Classes/classFunctionDeclResolver/)** <br>Implements [DeclResolver]() for functions used in target regions. 
* **class [OmpPragma](Classes/classOmpPragma/)** <br>A helper class to rewrite some "pragma omp" (mostly teams and similar combined constructs), which are not supported by sotoc. 
* **class [SourceTransformAction](Classes/classSourceTransformAction/)** 
* **class [TargetCode](Classes/classTargetCode/)** <br>A collection of all code from the input file that needs to be copied to the target source file. 
* **class [TargetCodeDecl](Classes/classTargetCodeDecl/)** <br>This class represents a declaration, i.e. 
* **class [TargetCodeFragment](Classes/classTargetCodeFragment/)** <br>An abstract base class for all fragments of the original code (except header includes) that need to be copied to our generated source code. 
* **class [TargetCodeRegion](Classes/classTargetCodeRegion/)** <br>Represents one target region. 
* **class [TargetRegionPrinterHelper](Classes/classTargetRegionPrinterHelper/)** 
* **class [TargetRegionTransformer](Classes/classTargetRegionTransformer/)** 
* **class [TargetRegionVariable](Classes/classTargetRegionVariable/)** <br>Represents a variable captured by a target region. 
    * **class [shape_const_kind_iterator](Classes/classTargetRegionVariable_1_1shape__const__kind__iterator/)** <br>Iterator which acts as a filter over std::vector<TargetRegionVariableShape>::const_iterator (the base_iter) which only passes on [TargetRegionVariableShape](Classes/classTargetRegionVariableShape/) of the kind specified in [Kind](). 
* **class [TargetRegionVariableShape](Classes/classTargetRegionVariableShape/)** <br>Describes the shape, i.e. 
* **class [TypeDeclResolver](Classes/classTypeDeclResolver/)** <br>Implements [DeclResolver]() for types (typedefs, structs enums) used in target regions. 
* **namespace [clang](Namespaces/namespaceclang/)** 
* **namespace [clang::tooling](Namespaces/namespaceclang_1_1tooling/)** 
* **namespace [llvm](Namespaces/namespacellvm/)** 




