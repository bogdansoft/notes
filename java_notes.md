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

### In the following code, how many of the imports do you think are redundant?
```
import java.lang.System;
import java.lang.*;
import java.util.Random;
import java.util.*;

public class NumberPicker {
public static void main(String[] args) {
Random r = new Random();
System.out.println(r.nextInt(10));
}}
```
The answer is that three of the imports are redundant. Lines 1 and 2 are redundant **because everything in java.lang is automatically imported**. Line 4 is also redundant in this example because Random is already imported from java.util.Random.

```
import java.util.*;
package structure; // DOES NOT COMPILE
String name; // DOES NOT COMPILE
public class Meerkat { } // DOES NOT COMPILE
```

### Primitive types
Keyword | Type | Min value | Max value | Default value | Example
--- | --- | --- | --- | --- | --- 
boolean | true or false | n/a | n/a | false | true
byte | 8-bit integral value | -128 | 127 | 0 | 123
short | 16-bit integral value | -32,768 | 32,767 | 0 | 123
int | 32-bit integral value | -2,147,483,648 | 2,147,483,647 | 0 | 123
long | 64-bit integral value | -2^63 | 2^63-1 | 0L|  123L
float | 32-bit floating-point value | n/a | n/a | 0.0f | 123.45f
double | 64-bit floating-point value | n/a | n/a | 0.0 | 123.456
char | 16-bit Unicode value | 0 | 65,535 | \u0000 | 'a'

```
double notAtStart = _1000.00; // DOES NOT COMPILE
double notAtEnd = 1000.00_; // DOES NOT COMPILE
double notByDecimal = 1000_.00; // DOES NOT COMPILE
double annoyingButLegal = 1_00_0.0_0; // Ugly, but compiles
double reallyUgly = 1__________2; // Also compiles
```
### Defining Text Blocks
```
String block = """doe"""; // DOES NOT COMPILE
String block = """
 doe \
 deer"""; // doe deer
```
The output is doe deer since the \ tells Java not to add a new line before deer.
```
String block = """
 doe \n
 deer
 """;
```
Output:
```
doe 

deer
```
### There are only four rules to remember for legal identifiers:
* Identifiers must begin with a letter, a currency symbol, or a _ symbol. Currency symbols 
include dollar ($), yuan (¥), euro (€), and so on.
* Identifiers can include numbers but not start with them.
* A single underscore _ is not allowed as an identifier.
* You cannot use the same name as a Java reserved word. 
true, false, and null are literal values, so they can’t be variable names.
```
long okidentifier;
float $OK2Identifier;
boolean _alsoOK1d3ntifi3r;
char __SStillOkbutKnotsonice$;
//These examples are not legal:
int 3DPointClass; // identifiers cannot begin with a number
byte hollywood@vine; // @ is not a letter, digit, $ or _
String *$coffee; // * is not a letter, digit, $ or _
double public; // public is a reserved word
short _; // a single underscore is not allowed
```
### Declaring Multiple Variables
```
int num, String value; // DOES NOT COMPILE
double d1, double d2; // DOES NOT COMPILE
int i1; int i2; // DOES NOT COMPILE
int i3; i4; // DOES NOT COMPILE

boolean b1, b2; //COMPILE
String s1 = "1", s2; //COMPILE
```
### Uninitialized Local Variables
Local variables do not have a default value and must be initialized before use. Furthermore, 
the compiler will report an error if you try to read an uninitialized value. For example, the 
following code generates a compiler error:
```
4: public int notValid() {
5: int y = 10;
6: int x;
7: int reply = x + y; // DOES NOT COMPILE
8: return reply;
9: }
```
The y variable is initialized to 10. By contrast, x is not initialized before it is used in the 
expression on line 7, and the compiler generates an error. The compiler is smart enough to 
recognize variables that have been initialized after their declaration but before they are used. 
Here’s an example:
```
public int valid() {
 int y = 10;
 int x; // x is declared here
 x = 3; // x is initialized here
 int z; // z is declared here but never initialized or used
 int reply = x + y;
 return reply;
 }
 ```
### Local variable type inference(var)
You can only use this feature for 
local variables
```
public class VarKeyword {
 var tricky = "Hello"; // DOES NOT COMPILE
 
 public void whatTypeAmI() {
 var name = "Hello"; //COMPILE
 var size = 7; //COMPILE
 }
 
 public void reassignment() {
   var number = 7;
   number = 4;
   number = "five"; // DOES NOT COMPILE
 }
 
 public void breakingDeclaration() {
  var silly
   = 1;
 }
 
 public void twoTypes() {
   int a, var b = 3; // DOES NOT COMPILE
   var n = null; // DOES NOT COMPILE
 }
 
 public int addition(var a, var b) { // DOES NOT COMPILE
 return a + b;
}
}
```
**var is not a reserved word and allowed to be used as an identifier**. It is considered a reserved type name. A reserved type name means it 
cannot be used to define a type, such as a class, interface, or enum. Do you think this is legal?
```
package var;
public class Var {
 public void var() {
 var var = "var";
 }
 public void Var() {
 Var var = new Var();
 }
}
```
Believe it or not, this code does compile. Java is case sensitive, so Var doesn’t introduce 
any conflicts as a class name. Naming a local variable var is legal. Please don’t write code 
that looks like this at your job! But understanding why it works will help get you ready for 
any tricky exam questions the exam creators could throw at you.
###  Rules on scope:
- Local variables: In scope from declaration to the end of the block
- Method parameters: In scope for the duration of the method
- Instance variables: In scope from declaration until the object is eligible for garbage 
collection
- Class variables: In scope from declaration until the program ends
