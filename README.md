# xjc-global-bindings
Reproduce issues with globalBindings and xjc. Global bindings are not applied when there is a schema include, and an annotation.

# Example with naming collision
Two elements with the same name, except a trailing underscore, which should be handled by `<jxb:globalBindings underscoreBinding="asCharInWord" />`.
The main xsd file contains both include and annotation..

```xjc -b bindings.xjb naming-collision-example/main.xsd```

Output:
```
parsing a schema...
compiling a schema...
[ERROR] A class/interface with the same name "generated.Employee" is already in use. Use a class customization to resolve this conflict.
  line 3 of file:/home/cristoffer/github/xjc-global-bindings/naming-collision-example/included.xsd

[ERROR] (Relevant to above error) another "Employee" is generated from here.
  line 13 of file:/home/cristoffer/github/xjc-global-bindings/naming-collision-example/included.xsd

[ERROR] Two declarations cause a collision in the ObjectFactory class.
  line 3 of file:/home/cristoffer/github/xjc-global-bindings/naming-collision-example/included.xsd

[ERROR] (Related to above error) This is the other declaration.
  line 13 of file:/home/cristoffer/github/xjc-global-bindings/naming-collision-example/included.xsd

Failed to produce code.
```

# Working example with no annotation in main.xsd

```xjc -b bindings.xjb no-include-works-example/main.xsd```


Output:
```
parsing a schema...
compiling a schema...
generated/Employee.java
generated/Employee_.java
generated/ObjectFactory.java
```

# Working example with no include in main.xsd

```xjc -b bindings.xjb no-include-works-example/main.xsd```

Output:
```
parsing a schema...
compiling a schema...
generated/Employee.java
generated/Employee_.java
generated/ObjectFactory.java
```

# XJC version
```
xjc -version
xjc 2.2.8-b130911.1802
```

# Java version
```
java -version                                        
java version "1.8.0_92"
Java(TM) SE Runtime Environment (build 1.8.0_92-b14)
Java HotSpot(TM) 64-Bit Server VM (build 25.92-b14, mixed mode)
```
