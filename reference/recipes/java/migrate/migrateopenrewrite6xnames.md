# Migrate OpenRewrite 6.x names

**org.openrewrite.java.migrate.MigrateOpenRewrite6xNames**  
_Change types and method names from OpenRewrite 6.x to 7._

## Recipe list

* [Change type](../../java/changetype.md)
  * oldFullyQualifiedTypeName: org.openrewrite.java.tree.J.Assign
  * newFullyQualifiedTypeName: org.openrewrite.java.tree.J.Assignment
* [Change type](../../java/changetype.md)
  * oldFullyQualifiedTypeName: org.openrewrite.java.tree.J.AssignOp
  * newFullyQualifiedTypeName: org.openrewrite.java.tree.J.AssignmentOperation
* [Change type](../../java/changetype.md)
  * oldFullyQualifiedTypeName: org.openrewrite.java.tree.J.ClassDecl
  * newFullyQualifiedTypeName: org.openrewrite.java.tree.J.ClassDeclaration
* [Change type](../../java/changetype.md)
  * oldFullyQualifiedTypeName: org.openrewrite.java.tree.J.Ident
  * newFullyQualifiedTypeName: org.openrewrite.java.tree.J.Identifier
* [Change type](../../java/changetype.md)
  * oldFullyQualifiedTypeName: org.openrewrite.java.tree.J.MethodDecl
  * newFullyQualifiedTypeName: org.openrewrite.java.tree.J.MethodDeclaration
* [Change type](../../java/changetype.md)
  * oldFullyQualifiedTypeName: org.openrewrite.java.tree.J.VariableDecls
  * newFullyQualifiedTypeName: org.openrewrite.java.tree.J.VariableDeclarations
* [Change type](../../java/changetype.md)
  * oldFullyQualifiedTypeName: org.openrewrite.java.tree.J.VariableDeclarations.NamedVar
  * newFullyQualifiedTypeName: org.openrewrite.java.tree.J.VariableDeclarations.NamedVariable
* [Change method name](../../java/changemethodname.md)
  * methodPattern: org.openrewrite.java.tree.J.AnnotatedType getTypeExpr(..)
  * newMethodName: getTypeExpression
* [Change method name](../../java/changemethodname.md)
  * methodPattern: org.openrewrite.java.tree.J.AnnotatedType withTypeExpr(..)
  * newMethodName: withTypeExpression
* [Change method name](../../java/changemethodname.md)
  * methodPattern: org.openrewrite.java.tree.J.Annotation getArgs(..)
  * newMethodName: getArguments
* [Change method name](../../java/changemethodname.md)
  * methodPattern: org.openrewrite.java.tree.J.Annotation withArgs(..)
  * newMethodName: withArguments
* [Change method name](../../java/changemethodname.md)
  * methodPattern: org.openrewrite.java.tree.J.CompilationUnit getPackageDecl(..)
  * newMethodName: getPackageDeclaration
* [Change method name](../../java/changemethodname.md)
  * methodPattern: org.openrewrite.java.tree.J.CompilationUnit withPackageDecl(..)
  * newMethodName: withPackageDeclaration
* [Change method name](../../java/changemethodname.md)
  * methodPattern: org.openrewrite.java.tree.J.Identifier getIdent(..)
  * newMethodName: getTypeInformation
* [Change method name](../../java/changemethodname.md)
  * methodPattern: org.openrewrite.java.tree.J.Identifier withIdent(..)
  * newMethodName: withTypeInformation
* [Change method name](../../java/changemethodname.md)
  * methodPattern: org.openrewrite.java.tree.J.InstanceOf getExpr(..)
  * newMethodName: getExpression
* [Change method name](../../java/changemethodname.md)
  * methodPattern: org.openrewrite.java.tree.J.InstanceOf withExpr(..)
  * newMethodName: withExpression
* [Change method name](../../java/changemethodname.md)
  * methodPattern: org.openrewrite.java.tree.J.Lambda.Parameters getParams(..)
  * newMethodName: getParameters
* [Change method name](../../java/changemethodname.md)
  * methodPattern: org.openrewrite.java.tree.J.Lambda.Parameters withParams(..)
  * newMethodName: withParameters
* [Change method name](../../java/changemethodname.md)
  * methodPattern: org.openrewrite.java.tree.J.MethodDeclaration getReturnTypeExpr(..)
  * newMethodName: getReturnTypeExpression
* [Change method name](../../java/changemethodname.md)
  * methodPattern: org.openrewrite.java.tree.J.MethodDeclaration withReturnTypeExpr(..)
  * newMethodName: withReturnTypeExpression
* [Change method name](../../java/changemethodname.md)
  * methodPattern: org.openrewrite.java.tree.J.MethodDeclaration getParams(..)
  * newMethodName: getParameters
* [Change method name](../../java/changemethodname.md)
  * methodPattern: org.openrewrite.java.tree.J.MethodDeclaration withParams(..)
  * newMethodName: withParameters
* [Change method name](../../java/changemethodname.md)
  * methodPattern: org.openrewrite.java.tree.J.MethodInvocation getArgs(..)
  * newMethodName: getArguments
* [Change method name](../../java/changemethodname.md)
  * methodPattern: org.openrewrite.java.tree.J.MethodInvocation withArgs(..)
  * newMethodName: withArguments
* [Change method name](../../java/changemethodname.md)
  * methodPattern: org.openrewrite.java.tree.J.NewArray getTypeExpr(..)
  * newMethodName: getTypeExpression
* [Change method name](../../java/changemethodname.md)
  * methodPattern: org.openrewrite.java.tree.J.NewArray withTypeExpr(..)
  * newMethodName: withTypeExpression
* [Change method name](../../java/changemethodname.md)
  * methodPattern: org.openrewrite.java.tree.J.NewClass getEncl(..)
  * newMethodName: getTypeEnclosing
* [Change method name](../../java/changemethodname.md)
  * methodPattern: org.openrewrite.java.tree.J.NewClass withEncl(..)
  * newMethodName: withTypeEnclosing
* [Change method name](../../java/changemethodname.md)
  * methodPattern: org.openrewrite.java.tree.J.Package getExpr(..)
  * newMethodName: getExpression
* [Change method name](../../java/changemethodname.md)
  * methodPattern: org.openrewrite.java.tree.J.Package withExpr(..)
  * newMethodName: withExpression
* [Change method name](../../java/changemethodname.md)
  * methodPattern: org.openrewrite.java.tree.J.Return getExpr(..)
  * newMethodName: getExpression
* [Change method name](../../java/changemethodname.md)
  * methodPattern: org.openrewrite.java.tree.J.Return withExpr(..)
  * newMethodName: withExpression
* [Change method name](../../java/changemethodname.md)
  * methodPattern: org.openrewrite.java.tree.J.Try.Resource getVariableDecls(..)
  * newMethodName: getVariableDeclarations
* [Change method name](../../java/changemethodname.md)
  * methodPattern: org.openrewrite.java.tree.J.Try.Resource withVariableDecls(..)
  * newMethodName: withVariableDeclarations
* [Change method name](../../java/changemethodname.md)
  * methodPattern: org.openrewrite.java.tree.J.Try.Catch getParam(..)
  * newMethodName: getParameter
* [Change method name](../../java/changemethodname.md)
  * methodPattern: org.openrewrite.java.tree.J.Try.Catch withParam(..)
  * newMethodName: withParameter
* [Change method name](../../java/changemethodname.md)
  * methodPattern: org.openrewrite.java.tree.J.TypeCast getExpr(..)
  * newMethodName: getExpression
* [Change method name](../../java/changemethodname.md)
  * methodPattern: org.openrewrite.java.tree.J.TypeCast withExpr(..)
  * newMethodName: withExpression
* [Change method name](../../java/changemethodname.md)
  * methodPattern: org.openrewrite.java.tree.J.VariableDeclarations getTypeExpr(..)
  * newMethodName: getTypeExpression
* [Change method name](../../java/changemethodname.md)
  * methodPattern: org.openrewrite.java.tree.J.VariableDeclarations withTypeExpr(..)
  * newMethodName: withTypeExpression
* [Change method name](../../java/changemethodname.md)
  * methodPattern: org.openrewrite.java.tree.J.VariableDeclarations getVars(..)
  * newMethodName: getVariables
* [Change method name](../../java/changemethodname.md)
  * methodPattern: org.openrewrite.java.tree.J.VariableDeclarations withVars(..)
  * newMethodName: withVariables
* [Change type](../../java/changetype.md)
  * oldFullyQualifiedTypeName: org.openrewrite.java.tree.Coordinates.Assign
  * newFullyQualifiedTypeName: org.openrewrite.java.tree.Coordinates.Assignment
* [Change type](../../java/changetype.md)
  * oldFullyQualifiedTypeName: org.openrewrite.java.tree.Coordinates.AssignOp
  * newFullyQualifiedTypeName: org.openrewrite.java.tree.Coordinates.AssignmentOperation
* [Change type](../../java/changetype.md)
  * oldFullyQualifiedTypeName: org.openrewrite.java.tree.Coordinates.ClassDecl
  * newFullyQualifiedTypeName: org.openrewrite.java.tree.Coordinates.ClassDeclaration
* [Change type](../../java/changetype.md)
  * oldFullyQualifiedTypeName: org.openrewrite.java.tree.Coordinates.Ident
  * newFullyQualifiedTypeName: org.openrewrite.java.tree.Coordinates.Identifier
* [Change type](../../java/changetype.md)
  * oldFullyQualifiedTypeName: org.openrewrite.java.tree.Coordinates.MethodDecl
  * newFullyQualifiedTypeName: org.openrewrite.java.tree.Coordinates.MethodDeclaration
* [Change type](../../java/changetype.md)
  * oldFullyQualifiedTypeName: org.openrewrite.java.tree.Coordinates.VariableDecls
  * newFullyQualifiedTypeName: org.openrewrite.java.tree.Coordinates.VariableDeclarations
* [Change type](../../java/changetype.md)
  * oldFullyQualifiedTypeName: org.openrewrite.java.tree.Coordinates.VariableDeclarations.NamedVar
  * newFullyQualifiedTypeName: org.openrewrite.java.tree.Coordinates.VariableDeclarations.NamedVariable
* [Change method name](../../java/changemethodname.md)
  * methodPattern: org.openrewrite.java.JavaVisitor visitAssign(..)
  * newMethodName: visitAssignment
* [Change method name](../../java/changemethodname.md)
  * methodPattern: org.openrewrite.java.JavaVisitor visitAssignOp(..)
  * newMethodName: visitAssignmentOperation
* [Change method name](../../java/changemethodname.md)
  * methodPattern: org.openrewrite.java.JavaVisitor visitClassDecl(..)
  * newMethodName: visitClassDeclaration
* [Change method name](../../java/changemethodname.md)
  * methodPattern: org.openrewrite.java.JavaVisitor visitMethod(..)
  * newMethodName: visitMethodDeclaration
* [Change method name](../../java/changemethodname.md)
  * methodPattern: org.openrewrite.java.JavaVisitor visitMultiVariable(..)
  * newMethodName: visitVariableDeclarations
* [Change method name](../../java/changemethodname.md)
  * methodPattern: org.openrewrite.java.tree.JRightPadded getElem(..)
  * newMethodName: getElement
* [Change method name](../../java/changemethodname.md)
  * methodPattern: org.openrewrite.java.tree.JRightPadded withElem(..)
  * newMethodName: withElement
* [Change method name](../../java/changemethodname.md)
  * methodPattern: org.openrewrite.java.tree.JLeftPadded getElem(..)
  * newMethodName: getElement
* [Change method name](../../java/changemethodname.md)
  * methodPattern: org.openrewrite.java.tree.JLeftPadded withElem(..)
  * newMethodName: withElement
* [Change method name](../../java/changemethodname.md)
  * methodPattern: org.openrewrite.java.tree.JContainer getElems(..)
  * newMethodName: getElements
* [Change method name](../../java/changemethodname.md)
  * methodPattern: org.openrewrite.java.tree.JContainer withElems(..)
  * newMethodName: withElements