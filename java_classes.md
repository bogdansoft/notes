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
To override a method, you must follow a number of rules. The compiler performs the following checks when you override a method:
1. The method in the child class must have the same signature as the method in the 
parent class.
2. The method in the child class must be at least as accessible as the method in the 
parent class.
3. The method in the child class may not declare a checked exception that is new or 
broader than the class of any exception declared in the parent class method.
4. If the method returns a value, it must be the same or a subtype of the method in the parent class, known as covariant return types.

The Dog’s move() method is called the **overriding method.**
The Animal’s move() method is called the **overridden method.**

#### Rule #1:Only inherited methods can be overridden.

#### Rule #2:Final and static methods cannot be overridden.

#### Rule #3: The overriding method must have same argument list or it is an overload instead.
 
#### Rule #4: The overriding method must have same return type (or subtype).
 
#### Rule #5: The overriding method must not have more restrictive access modifier.
 
#### Rule #6: The overriding method must not throw new or broader checked exceptions.
In other words, the overriding method may throw fewer or narrower checked exceptions, or any unchecked exceptions.
Consider the following superclass - Animal:
```
public class Animal {
 
    protected void move() throws IOException {
        // animal moving code...
    }
}
```
The following subclass - Dog, correctly overrides the move() method because the FileNotFoundException is a subclass of the FileIOException:
```
public class Dog extends Animal {
 
    protected void move() throws FileNotFoundException {
        // Dog moving code...
    }
}
```
The following example shows an illegal overriding attempt because the InterruptedException is a new and checked exception:
```
public class Dog extends Animal {
 
    protected void move() throws IOException, InterruptedException {
        // Dog moving code...
    }
}
```
However, the following example is a legal overriding, because the IllegalArgumentException is an unchecked exception:
```
public class Dog extends Animal {
 
    protected void move() throws IOException, IllegalArgumentException {
        // Dog moving code...
    }
}
```
And in the example below, the Dog class won’t compile because its move() method throws Exception which is superclass (broader) of the IOException:
```
public class Dog extends Animal {
 
    protected void move() throws Exception {
        // Dog moving code...
    }
}
```
#### Rule #7:Use the super keyword to invoke the overridden method from a subclass.

#### Rule #8:Constructors cannot be overridden.

#### Rule #9: Abstract methods must be overridden by the first concrete (non-abstract) subclass.

#### Rule #10: A static method in a subclass may hide another static one in a superclass, and that’s called hiding.
Consider the following example:
```
public class Animal {
 
    static void sleep() {
        System.out.println("Animal sleeps");
    }
 

public class Dog extends Animal {
 
    static void sleep() {
        System.out.println("Dog sleeps");
    }
}
```
Here, the sleep() method of the Dog class is said to hide the sleep() method of the Animal class. When a static method of the superclass is hidden, it requires the subclass to use a fully qualified class name of the superclass to invoke the hidden method, as shown in the doSomething() method of the Dog class below:
```
public class Dog extends Animal {
 
    static void sleep() {
        System.out.println("Dog sleeps");
    }
 
    void doSomething() {
        sleep();    // this calls the hiding method
 
        // because the Animal's sleep() is hidden, it requires to use
        // a fully qualified class name to access it.
        Animal.sleep();
    }
}
```
Note that the rules of overriding are still applied for the hiding method.

#### Rule #11: The synchronized modifier has no effect on the rules of overriding.
The synchronized modifier relates to the acquiring and releasing of a monitor object in multi-threaded context, therefore it has totally no effect on the rules of overriding. That means a synchronized method can override a non-synchronized one and vice versa.
 
#### Rule #12: The strictfp modifier has no effect on the rules of overriding.
That means the presence or absence of the strictfp modifier has absolutely no effect on the rules of overriding: it’s possible that a FP-strict method can override a non-FP-strict one and vice-versa.

#### Creating Constructors in Abstract Classes
```
abstract class Mammal {
 abstract CharSequence chew();
 public Mammal() {
 System.out.println(chew()); // this line compile
 }
}
public class Platypus extends Mammal {
 String chew() { return "yummy!"; }
 public static void main(String[] args) {
 new Platypus();
 }
}
```
 Abstract classes are initialized with constructors in the same 
way as non-abstract classes. For example, if an abstract class does not provide a constructor, 
the compiler will automatically insert a default no-argument constructor.
The primary difference between a constructor in an abstract class and a non-abstract class 
is that a constructor in an abstract class can be called only when it is being initialized by a 
non-abstract subclass. This makes sense, as abstract classes cannot be instantiated.

#### Declaring an Immutable Class

1. Mark the class as final or make all of the constructors private.
2. Mark all the instance variables private and final.
3. Don’t define any setter methods.
4. Don’t allow referenced mutable objects to be modified.
5. Use a constructor to set all properties of the object, making a copy if needed.

### Interfaces
#### Inserting Implicit Modifiers

+ Interfaces are implicitly abstract.
+ Interface variables are implicitly public, static, and final.
+ Interface methods without a body are implicitly abstract.
+ Interface methods without the private modifier are implicitly public

#### Conflicting Modifiers
```
public interface Dance {
 private int count = 4; // DOES NOT COMPILE
 protected void step(); // DOES NOT COMPILE
}
```
Neither of these interface member declarations compiles, as the compiler will apply the 
public modifier to both, resulting in a conflict.

#### Differences between Interfaces and Abstract Classes
Even though abstract classes and interfaces are both considered abstract types, only interfaces make use of implicit modifiers. How do the play() methods differ in the following two 
definitions?
```
abstract class Husky { // abstract required in class declaration
 abstract void play(); // abstract required in method declaration
}
interface Poodle { // abstract optional in interface declaration
 void play(); // abstract optional in method declaration
}
```
