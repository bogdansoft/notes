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
