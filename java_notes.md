## Java notes

### Method overloading in Java

Method overloading in Java is an object-oriented programming concept that allows a programmer to declare two methods of the same name but with different method signatures, like a change in the argument list or a change in the type of argument

Properties of method overloading in Java:
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

#### What is Static and Dynamic binding in Java with Example

1) Static binding in Java occurs during Compile time while Dynamic binding occurs during Runtime.

2) private, final and static methods and variables use static binding and are bonded by the compiler while virtual methods are bonded during runtime based upon runtime object.

3) Static binding uses Type(Class in Java)  information for binding while Dynamic binding uses Object to resolve to bind.

3) Overloaded methods are bonded using static binding while overridden methods are bonded using dynamic binding at runtime. Here is an example that will help you to understand both static and dynamic binding in Java.

##### Static Binding Example in Java
Here is an example of static binding in java, which will clear

 things on how overloaded methods in java are bonded during compile time using Type information.
```java
public class StaticBindingTest {
 
    public static void main(String args[])  {
       Collection c = new HashSet();
       StaticBindingTest et = new StaticBindingTest();
       et.sort(c);
     
    }
   
    //overloaded method takes Collection argument
    public Collection sort(Collection c){
        System.out.println("Inside Collection sort method");
        return c;
    }
 
   
   //another overloaded method which takes HashSet argument which is sub class
    public Collection sort(HashSet hs){
        System.out.println("Inside HashSet sort method");
        return hs;
    }  
}

Output:
Inside Collection sort method
```

In the above example of static binding in Java, we have an overloaded sort() method, one of which accepts Collection and the other accept HashSet. we have called sort() method with HashSet as an object but referenced with type Collection and when we run method with the collection as argument type gets called because it was bonded on compile-time based on the type of variable (Static binding)  which was collection.

##### Example of Dynamic Binding in Java
In the last section, we have seen example of static binding which clears things that static binding occurs on compile-time, and Type information is used to resolve methods. In this section, we will see an example of dynamic binding in java which occurs during run time and instead of Type or Class information, Object is used to resolve method calls.
```java
public class DynamicBindingTest {

    public static void main(String args[]) {
        Vehicle vehicle = new Car(); //here Type is vehicle but object will be Car
        vehicle.start();       //Car's start called because start() is overridden method
    }
}

class Vehicle {

    public void start() {
        System.out.println("Inside start method of Vehicle");
    }
}

class Car extends Vehicle {

    @Override
    public void start() {
        System.out.println("Inside start method of Car");
    }
}

Output:
Inside start method of Car
```
In this example of Dynamic Binding, we have used the concept of method overriding. Car extends Vehicle and overrides its start() method and when we call start() method from a reference variable of type Vehicle, it doesn't call start() method from Vehicle class instead it calls start() method from Car subclass because object referenced by Vehicle type is a Car object. 

This resolution happens only at runtime because objects are only created during runtime and are called dynamic binding in Java. Dynamic binding is slower than static binding because it occurs in runtime and spends some time to find out the actual method to be called.

That's all on the difference between static and dynamic binding in java. The bottom line is static binding is a compile-time operation while the dynamic binding is a runtime. one uses Type and the other uses Object to bind. static, private, and final methods and variables are resolved using static binding which makes their execution fast because no time is wasted to find the correct method during runtime.

### Class Loader

A typical enterprise Java application may comprise thousands of source and dependency classes. To handle all of them in a proper way JVM introduces a special mechanism called class loader. It is a part of JRE responsible for dynamic loading classes into memory. Understanding class loading allows to control this process and helps to avoid some types of exceptions.

First of all, let's recall that java code goes through 2 stages: a compilation from source code to byte code (.java -> .class) and a byte code interpretation. The task of a class loader is finding the needed class through .class files from a disc and loading a representing object into the RAM. However, classes are not loaded in bulk mode on the application startup. A class loader loads them on-demand during an interpretation starting with a class containing the main method.

A class loader concept is represented by java.lang.ClassLoader abstract class. There are 3 standard ClassLoader implementations:

Bootstrap loads JDK internal classes e.g. java.util package.

Extension/Platform loads classes from JDK extensions.

Application/System loads classes from application classpath.

One may ask what comes first if classes are loaded by a class loader and the ClassLoader itself is a class. To answer the question let's consider a sequence of these ClassLoaders invocations. First, JRE creates the Bootstrap ClassLoader which loads core classes. Then, Extension ClassLoader is created with Bootstrap as a parent. It loads classes for extensions if such exist. Finally, the Application ClassLoader is created with Extension as a parent. It is responsible for loading application classes from a classpath. Each class loaded in memory is identified by a fully-qualified class name and ClassLoader that loaded this class. Moreover, Class has a method getClassLoader that returns the class loader which loads the given class.

Take a look at the example:
```java
import java.sql.SQLData;
import java.util.ArrayList;

public class Main {
    public static void main(String[] args) {
        ClassLoader listClassLoader = ArrayList.class.getClassLoader();
        ClassLoader sqlClassLoader = SQLData.class.getClassLoader();
        ClassLoader mainClassLoader = Main.class.getClassLoader();

        System.out.println(listClassLoader); // null
        System.out.println(sqlClassLoader.getName()); // platform
        System.out.println(mainClassLoader.getName()); // app
    }
}
```

When the class loader receives a request for loading a class, it follows certain steps in order to resolve the class. Default behavior defined by JVM specification:

1. Check if the class has already been loaded
2. If not, delegate the request to a parent
3. If the parent class returns nothing, it attempts to find the class in its own classpath



Default logic can be overridden in custom class loaders. So web container class loaders will look for classes in the local classpath and only in case the class is not found will delegate resolving to a parent.

Example
Let's consider an application that consists of 2 classes. Although it does nothing, it is a good example of a class loader explanation.
```
public class A {
    public static void main(String[] args) {
        B b = new B();
    }
}
public class B {
}
```
Launch the program by command:
```
java A
```
Let's go through key points of class loading during code execution:
1. Bootstrap ClassLoader is invoked by JRE on the start java process. It loads java internal packages.
2. Extension ClassLoader is invoked but loads nothing.
3. Application ClassLoader is invoked and loads class A.
4. When the constructor of class B is invoked ClassLoader of class A (Application ClassLoader) is invoked to load class B and delegates loading to Extension        ClassLoader.
5. Extension ClassLoader is invoked and delegates loading to Bootstrap ClassLoader.
6. Bootstrap ClassLoader is invoked and tries to resolve the class, but finds nothing and returns control to Extension ClassLoader.
7. Extension ClassLoader finds nothing as well and returns control to Application ClassLoader.
8. Application ClassLoader resolves the class and loads it into memory.

When something goes wrong

Let's have a quick glance at problems related to class loaders. The common root cause comes because runtime dependencies may differ from compile-time ones. For instance, a project may be compiled successfully, but some classes were not added to the classpath. In that case, a class loader cannot find a class. That leads to ClassNotFoundException or NoClassDefFoundError. Another kind of exception happens because a project was compiled with one version of a class, but the classpath includes a different one. In that case NoSuchMethodError or NoSuchFieldError are thrown.
