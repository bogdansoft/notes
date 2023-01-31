## Java Classes
#### Class Modifiers
Modifier | Description 
--- | ---
final | The class may not be extended. 
abstract | The class is abstract, may contain abstract methods, and requires a concrete subclass to instantiate.
sealed | The class may only be extended by a specific list of classes.
non-sealed | A subclass of a sealed class permits potentially unnamed subclasses.
static | Used for static nested classes defined within a class. 

Trying to declare a top-level class with protected or private class will lead to a compiler error, though:
```
// ClownFish.java
protected class ClownFish{} // DOES NOT COMPILE
// BlueTang.java
private class BlueTang {} // DOES NOT COMPILE
```
#### Accessing the this Reference
```
public class Flamingo {
 private String color = null;
 public void setColor(String color) {
 color = color;
 }
 public static void main(String... unused) {
 var f = new Flamingo();
 f.setColor("PINK");
 System.out.print(f.color);
 }
}
```
```
public void setColor(String color) {
 this.color = color; // Sets the instance variable with method parameter
 }
```
```
public class Duck {
private String color;
private int height;
private int length;

public void setData(int length, int theHeight) {
length = this.length; // Backwards -- no good!
height = theHeight; // Fine, because a different name
this.color = "white"; // Fine, but this. reference not necessary
 }

 public static void main(String[] args) {
 Duck b = new Duck();
 b.setData(1,2);
 System.out.print(b.length + " " + b.height + " " + b.color);//0 2 white
} }
```
#### Calling the super Reference

```
class Insect {
    protected int numberOfLegs = 4;
    String label = "buggy";
}

 class Beetle extends Insect {
    protected int numberOfLegs = 6;
    short age = 3;

    public void printData() {
        System.out.println(this.label);//buggy
        System.out.println(super.label);//buggy
        System.out.println(this.age);//3
        System.out.println(super.age);//DOES NOT COMPILE
        System.out.println(numberOfLegs);//6
    }
     public static void main(String[] n) {
         new Beetle().printData();
     }
}
```

#### Constructor
```
public class Bunny {
 public bunny() {} // DOES NOT COMPILE
 public void Bunny() {}
 public Bunny(var food) { // DOES NOT COMPILE
}
```
#### Constructor overloading
```
public class Turtle {
 private String name;
 public Turtle() {
 name = "John Doe";
 }
 public Turtle(int age) {}
 public Turtle(long age) {}
 public Turtle(String newName, String... favoriteFoods) {
 name = newName;
 }
}
```
**Every class in Java has a constructor, whether you code one or not. If you don’t include 
any constructors in the class, Java will create one for you without any parameters.**
```
public class Rabbit4 {
 private Rabbit4() {}
}
var r4 = new Rabbit4(); // DOES NOT COMPILE
```
Having only **private constructors** in a class tells the compiler not to 
provide a default no-argument constructor. It also prevents other classes 
from instantiating the class. This is useful when a class has only static
methods or the developer wants to have full control of all calls to create 
new instances of the class.

#### Calling Overloaded Constructors with this()
```
public class Hamster {
 private String color;
 private int weight;
 public Hamster(int weight, String color) { // First constructor
 this.weight = weight;
 this.color = color;
 }
 public Hamster(int weight) { // Second constructor
 this.weight = weight;
 color = "brown";
 }
 public Hamster(int weight) { // Second constructor
 Hamster(weight, "brown"); // DOES NOT COMPILE
 }
 public Hamster(int weight) { // Second constructor
 new Hamster(weight, "brown"); // Compiles, but creates an extra object
 }
 
 //Solution
 public Hamster(int weight) { // Second constructor
 this(weight, "brown");
 }
}
```
#### this vs. this()
Despite using the same keyword, this and this() are very different. The first, this, 
refers to an instance of the class, while the second, this(), refers to a constructor call 
within the class.

Calling this() has one special rule you need to know. If you choose to call it, the this() call 
must be the first statement in the constructor. The side effect of this is that there can be only 
one call to this() in any constructor.
```
public Hamster(int weight) {
System.out.println("chew");
// Set weight and default color
this(weight, "brown"); // DOES NOT COMPILE
}
```
Rules:
- A class can contain many overloaded constructors, provided the signature for each 
is distinct.
- The compiler inserts a default no-argument constructor if no constructors are declared.
- If a constructor calls this(), then it must be the first line of the constructor.
- Java does not allow cyclic constructor calls.
```
public class Gopher {
 public Gopher(int dugHoles) {
 this(5); // DOES NOT COMPILE
 }
}
```
The compiler is capable of detecting that this constructor is calling itself infinitely. 

#### Calling Parent Constructors with super()

The first statement of every constructor is a call to a parent constructor using super() or 
another constructor in the class using this().
```
public class Animal {
 private int age;
 public Animal(int age) {
 super(); // Refers to constructor in java.lang.Object
 this.age = age;
 }
}
public class Zebra extends Animal {
 public Zebra(int age) {
 super(age); // Refers to constructor in Animal
 }
 public Zebra() {
 this(4); // Refers to constructor in Zebra with int argument
 }
}
```
**super vs. super()**

Like this and this(), super and super() are unrelated in Java. The first, super, is 
used to reference members of the parent class, while the second, super(), calls a parent constructor.

Like calling this(), calling super() can only be used as the first statement of the constructor. 
For example, the following two class definitions will not compile:
```
public class Zoo {
 public Zoo() {
 System.out.println("Zoo created");
 super(); // DOES NOT COMPILE
 }
}
public class Zoo {
 public Zoo() {
 super();
 System.out.println("Zoo created");
 super(); // DOES NOT COMPILE
 }
}
```
#### Understanding Compiler Enhancements
```
public class Donkey {}
public class Donkey {
 public Donkey() {}
}
public class Donkey {
 public Donkey() {
 super();
 }
}
```
#### Default Constructor Tips and Tricks
What happens if we define a 
subclass with no constructors, or a subclass with a constructor that doesn’t include a super()
reference?
```
public class Mammal {
 public Mammal(int age) {}
}
public class Seal extends Mammal {} // DOES NOT COMPILE
public class Elephant extends Mammal {
 public Elephant() {} // DOES NOT COMPILE
}
```
The answer is that neither subclass compiles. Since Mammal defines a constructor, the 
compiler does not insert a no-argument constructor. The compiler will insert a default no argument constructor into Seal, though, but it will be a simple implementation that just 
calls a nonexistent parent default constructor.
```
public class Seal extends Mammal {
 public Seal() {
 super(); // DOES NOT COMPILE
 }
}
```
Likewise, Elephant will not compile for similar reasons. The compiler doesn’t see a call 
to super() or this() as the first line of the constructor so it inserts a call to a nonexistent 
no-argument super() automatically. 
```
public class Elephant extends Mammal {
 public Elephant() {
 super(); // DOES NOT COMPILE
 }
}
```
In these cases, the compiler will not help, and you must create at least one constructor in 
your child class that explicitly calls a parent constructor via the super() command.
```
public class Seal extends Mammal {
 public Seal() {
 super(6); // Explicit call to parent constructor
 }
}
public class Elephant extends Mammal {
 public Elephant() {
 super(4); // Explicit call to parent constructor
 }
}
```
Subclasses may include no-argument constructors even if their parent classes do not. For 
example, the following compiles because Elephant includes a no-argument constructor:
```
public class AfricanElephant extends Elephant {}
```
#### super() Always Refers to the Most Direct Parent
A class may have multiple ancestors via inheritance. In our previous example, 
AfricanElephant is a subclass of Elephant, which in turn is a subclass of Mammal. For 
constructors, though, super() always refers to the most direct parent. In this example, 
calling super() inside the AfricanElephant class always refers to the Elephant class 
and never to the Mammal class.

We conclude this section by adding three constructor rules to your skill set:
- The first line of every constructor is a call to a parent constructor using super() or an 
overloaded constructor using this().
- If the constructor does not contain a this() or super() reference, then the compiler 
automatically inserts super() with no arguments as the first line of the constructor.
- If a constructor calls super(), then it must be the first line of the constructor.

#### Initializing Classes

One of the most important rules with class initialization is that it happens at most once 
for each class. The class may also never be loaded if it is not used in the program. We summarize the order of initialization for a class as follows:
**Initialize Class X**
+ If there is a superclass Y of X, then initialize class Y first.
+ Process all static variable declarations in the order in which they appear in the class.
+ Process all static initializers in the order in which they appear in the class.
Taking a look at an example, what does the following program print?
```
public class Animal {
 static { System.out.print("A"); }
}
public class Hippo extends Animal {
 public static void main(String[] grass) {
 System.out.print("C");
 new Hippo();
 new Hippo();
 new Hippo();
 }
 static { System.out.print("B"); }
}//ABC
```
It prints ABC exactly once. Since the main() method is inside the Hippo class, the class 
will be initialized first, starting with the superclass and printing AB. Afterward, the main()
method is executed, printing C. Even though the main() method creates three instances, the 
class is loaded only once.

#### Why the Hippo Program Printed C After AB
In the previous example, the Hippo class was initialized before the main() method was 
executed. This happened because our main() method was inside the class being executed, 
so it had to be loaded on startup. What if you instead called Hippo inside another program?
```
public class HippoFriend {
 public static void main(String[] grass) {
 System.out.print("C");
 new Hippo();
 }
}
```
Assuming the class isn’t referenced anywhere else, this program will likely print CAB, with 
the Hippo class not being loaded until it is needed inside the main() method. We say 
likely because the rules for when classes are loaded are determined by the JVM at runtime. 
For the exam, you just need to know that a class must be initialized before it is referenced 
or used. Also, the class containing the program entry point, aka the main() method, is 
loaded before the main() method is executed.

#### Initializing final Fields
```
class A {

    private final boolean a;
    private final boolean b;

    public A(boolean a) {
        this.a = a;//DOES NOT COMPILE
    }

    public A(boolean a, boolean b) {
        this.a = a;
        this.b = b;
    }
}
```
You can initialize b to default false. All the final variable should be initialized in constructors.
```
 public A(boolean a){
     this.a = a;
     this.b = false;
 }
```
Or should call other constructors which would initialize them.
```
 public A(boolean a){
     this(a, false);
 }

 public A(boolean a, boolean b){
     this.a = a;
     this.b = b;
 }
 ```
**Initialize Instance of X**
1. Initialize class X if it has not been previously initialized.
2. If there is a superclass Y of X, then initialize the instance of Y first.
3. Process all instance variable declarations in the order in which they appear in the class.
4. Process all instance initializers in the order in which they appear in the class.
5. Initialize the constructor, including any overloaded constructors referenced with this().

Important rules you should know:
- A class is initialized at most once by the JVM before it is referenced or used.
- All static final variables must be assigned a value exactly once, either when they 
are declared or in a static initializer.
- All final fields must be assigned a value exactly once, either when they are declared, in an 
instance initializer, or in a constructor.
- Non-final static and instance variables defined without a value are assigned a 
default value based on their type.
- Order of initialization is as follows: variable declarations, then initializers, and finally 
constructors.

#### Overriding a Method
```
public class Marsupial {
 public double getAverageWeight() {
 return 50;
 }
}
public class Kangaroo extends Marsupial {
 public double getAverageWeight() {
 return super.getAverageWeight()+20;
 }
  public double getAverageWeight() {
 return getAverageWeight()+20;// StackOverflowError
 }
 public static void main(String[] args) {
 System.out.println(new Marsupial().getAverageWeight()); // 50.0
 System.out.println(new Kangaroo().getAverageWeight()); // 70.0
 }
}
```
To override a method, you must follow a number of rules. The compiler performs the following checks when you override a method:
1. The method in the child class must have the same signature as the method in the 
parent class.
2. The method in the child class must be at least as accessible as the method in the 
parent class.
3. The method in the child class may not declare a checked exception that is new or 
broader than the class of any exception declared in the parent class method.
4. If the method returns a value, it must be the same or a subtype of the method in the parent class, known as covariant return types.
