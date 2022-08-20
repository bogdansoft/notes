## Java notes

#### Properties of method overloading in Java

1) Overloaded methods are bonded using static binding in Java. Which occurs during compile time i.e. when you compile a Java program. During the compilation 
   process, the compiler bind method calls to the actual method.

2) Overloaded methods are fast because they are bonded during compile time and no check or binding is required during runtime.

3) Most important rule of method overloading in Java is that two overloaded methods must have a different signature. 

Here is an example of what does method signature means in Java:
A number of arguments to a method are part of the method signature.
Type of argument to a method is also part of the method signature
Order of argument also forms part of the method signature provided they are of a different type.
The return type of method is not part of the method signature in Java.

Method Overloading Example in Java
Here is a list of methods and there is a corresponding overloaded method with the reason that How they are overloaded :

Original method :
```
public void  show(String message){
      System.out.println(message);
}
```

Overloaded method: number of arguments is different
```
public void  show(String message, boolean show){
      System.out.println(message);
}
```

Overloaded method: type of argument is different
```
public void  show(Integer message){
      System.out.println(message);
}
```

Not an Overloaded method: the only return type is different
```
public boolean show(String message){
      System.out.println(message);
      return false;
}
```
