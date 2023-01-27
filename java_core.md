## Java core

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
## Switch Statement
### Java 7 : Switch Statement
Until Java 7 only integers could be used in switch case and this had been the standard for a long time:
```
int value = 5;
switch (value) {
    case 1:
        System.out.println("One");
        break;
    case 5:
        System.out.println("five");
        break;
    default:
        System.out.println("Unknown");
}
```
### Java 8 : Switch Statement
In Java 8 strings & enum were introduced in case values and switch statements started to evolve
String Switch Case :
```
String day = "Tuesday";
        switch (day) {
            case "Monday":
                System.out.println("Week day");
                break;
            case "Tuesday":
                System.out.println("Week day");
                break;
            case "Wednesday":
                System.out.println("Week day");
                break;
            case "Thursday":
                System.out.println("Week day");
                break;
            case "Friday":
                System.out.println("Week day");
                break;
            case "Saturday":
                System.out.println("Weekend");
                break;
            case "Sunday":
                System.out.println("Weekend");
                break;
            default:
                System.out.println("Unknown");
        }
```
### Enum Switch Case
```
enum DAYS {
    MONDAY, TUESDAY, WEDNESDAY, THURSDAY, FRIDAY, SATURDAY, SUNDAY
}
DAYS days = DAYS.SUNDAY;
switch (days) {
    case MONDAY:
        System.out.println("Weekdays");
        break;
    case TUESDAY:
        System.out.println("Weekdays");
        break;
    case WEDNESDAY:
        System.out.println("Weekdays");
        break;
    case THURSDAY:
        System.out.println("Weekdays");
        break;
    case FRIDAY:
        System.out.println("Weekdays");
        break;
    case SATURDAY:
        System.out.println("Weekends");
        break;
    case SUNDAY:
        System.out.println("Weekends");
        break;
    default:
        System.out.println("Unknown");
}
```
### Java 12 : Switch Statement
Java 12 further enhanced the switch statement and introduced switch expressions as a preview feature.

It introduced a flurry of new features:

+ You can return values from a switch block and hence switch statements became switch expressions
+ You can have multiple values in a case label
+ You can return value from a switch expression through the arrow operator or through the “break” keyword
**Return value through break keyword**
```
return  switch (day) {
    case "Monday":
        break "Weekday";
    case "Tuesday":
        break "Weekday";
    case "Wednesday":
        break "Weekday";
    case "Thursday":
        break "Weekday";
    case "Friday":
        break "Weekday";
    case "Saturday":
        break "Weekend";
    case "Sunday":
        break "Weekend";
    default:
        break "Unknown";
};
```
The word “break” can be used to return the result value.

**This word was replaced by “yield” later in Java 13.**
```
return  switch (day) {
    case "Monday":
        yield  "Weekday";
    case "Tuesday":
        yield "Weekday";
    case "Wednesday":
        yield "Weekday";
    case "Thursday":
        yield "Weekday";
    case "Friday":
        yield "Weekday";
    case "Saturday":
        yield "Weekend";
    case "Sunday":
        yield "Weekend";
    default:
        yield "Unknown";
};
```
Return value through arrow operator :

Further instead of returning values using break keyword , Java 12 introduced arrow operators as a simple alternative:
```
return  switch (day) {
            case "Monday"-> "Week day";
            case "Tuesday"-> "Week day";
            case "Wednesday"->"Week day";
            case "Thursday"->"Week day";
            case "Friday"->"Week day";
            case "Saturday"-> "Weekend";
            case "Sunday"-> "Weekend";
            default->"Unknown";
        };
```
### Multiple case labels :

Also starting Java 12 multiple case values could be provided in a single case statement , So if you observe above example since all 5 case expected here same value so instead of return one by one i can merge or combine multiple case value to single one like below
```
return  switch (day) {
            case "Monday","Tuesday","Wednesday","Thursday","Friday"
-> "Week day";
            case "Saturday", "Sunday" -> "Weekend";
            default->"Unknown";
        };
```
### Java 14 : Switch Statement changes
What ever switch statement & features we discussed so far in java 12 and 13 those are preview features to access that The flag –enable-preview need to set true .
But Java 14 just made all the features permanent from being a preview feature
The flag –enable-preview need not be set starting java 14. & switch statements have evolved into switch expressions!

### Java 17 : Switch Statement / Expression :
Java 17 LTS is the latest long-term support release for the Java SE platform and it was released on September 15, 2021.

Switch expression features:
- Pattern matching
- Gaurded pattern
- Null cases

The following is a list of all data types supported by switch statements:
+ int and Integer
+ byte and Byte
+ short and Short
+ char and Character
+ String
+ enum values
+ var (if the type resolves to one of the preceding types)

Another rules:
1. All of the branches of a switch expression that do not throw an exception must return 
a consistent data type (if the switch expression returns a value).
2. If the switch expression returns a value, then every branch that isn’t an expression must 
yield a value.
3. A default branch is required unless all cases are covered or no value is returned.

```
int fish = 5;
int length = 12;
var name = switch(fish) {
 case 1 -> "Goldfish";
 case 2 -> {yield "Trout";}
 case 3 -> {
 if(length > 10) yield "Blobfish";
 else yield "Green";
 }
 default -> "Swordfish";
};
```
The yield keyword is equivalent to a return statement within a switch expression and 
is used to avoid ambiguity about whether you meant to exit the block or method around the 
switch expression.
Referring to our second rule for switch expressions, yield statements are not optional if the 
switch statement returns a value.
```
 int fish = 5;
 int length = 12;
 var name = switch(fish) {
 case 1 -> "Goldfish";
 case 2 -> {} // DOES NOT COMPILE
 case 3 -> {
 if(length > 10) yield "Blobfish";
 } // DOES NOT COMPILE
 default -> "Swordfish";
 };
 ```
##### Pattern Matching :
It has introduced a new feature for switch i.e called pattern matching.

You can match patterns in a case label.

In other words you can pass objects in switch condition and this object can be checked for different types in switch case labels.
```
return switch (obj) {
    case Integer i -> "It is an integer";
    case String s -> "It is a string";
    case Employee s -> "It is a Employee";
     default -> "It is none of the known data types";
};
```
In the above example I am passing an object to the switch condition. This was not possible until Java 17. And then this object can be checked for a particular data type and assigned to a variable as well.

For example consider the case :
```
case Integer i- > "It is an integer";
```
The passed object is checked for the type “Integer” and then assigned to the variable “i” if it is an integer. And through the arrow operator the string “It is an integer ” is returned .

##### Gaurded Patterns :
Let’s take this use case.

Inside the case label where I have checked for a “Employee” instance , I want to do an additional check.

Thinking traditionally , you could be doing this after the case statement.

Something like this:
```
case Employee emp:

if(emp.getDept().equals("IT")) {
yield "This is IT Employee";
}
```
But Java 17 has introduced “Guarded Patterns” . You can do this check in the case label itself like below
```
return switch (obj) {
    case Integer i -> "It is an integer";
    case String s -> "It is a string";
    case Employee employee && employee.getDept().equals("IT") -> "IT Employee";
    default -> "It is none of the known data types";
};
```
##### Null Cases :
You could never pass a null value to switch statements prior to Java 17 without a Null pointer exception being thrown.

Java 17 allows you to handle it this way
```
case null -> "It is a null object";
```
### How to use switch?
If you have the above switch expression you will never get Null Pointer exception if the object you pass is null.

1.With arrow labels when a full block is needed:
```
int value = switch (greeting) {
    case "hi" -> {
        System.out.println("I am not just yielding!");
        yield 1;
    }
    case "hello" -> {
        System.out.println("Me too.");
        yield 2;
    }
    default -> {
        System.out.println("OK");
        yield -1;
    }
};
```
2.With traditional blocks:
```
int value = switch (greeting) {
    case "hi":
        System.out.println("I am not just yielding!");
        yield 1;
    case "hello":
        System.out.println("Me too.");
        yield 2;
    default:
        System.out.println("OK");
        yield -1;
};
```
The break with value statement is dropped in favour of a yield statement.

### Numeric Promotion Rules
1. If two values have different data types, Java will automatically promote one of the 
values to the larger of the two data types.
2. If one of the values is integral and the other is floating-point, Java will automatically 
promote the integral value to the floating-point value’s data type.
3. Smaller data types, namely, byte, short, and char, are first promoted to int any time 
they’re used with a Java binary arithmetic operator with a variable (as opposed to a 
value), even if neither of the operands is int.Unary operators are excluded from this 
rule. For example, applying ++ to a short value results in a short value
4. After all promotion has occurred and the operands have the same data type, the resulting value will have the same data type as its promoted operands.

```
short a = 11, b = 2;
var c = a * b;
System.out.println(c);
System.out.println(((Object)c).getClass().getSimpleName());
//Output:
22
Integer
```
```
int x = 1;
long y = 33;
var z = x * y;
//Output:
33
Long
```
```
short w = 14;
float x = 13;
double y = 30;
var z = w * x / y;
System.out.println(z);
System.out.println(((Object)z).getClass().getSimpleName());
//Output:
6.066666666666666
Double
```
### Casting Values
```
int fur = (int)5;
int hair = (short) 2;
String type = (String) "Bird";
short tail = (short)(4 + 10);
long feathers = 10(long); // DOES NOT COMPILE
float egg = 2.0 / 9; // DOES NOT COMPILE
int tadpole = (int)5 * 2L; // DOES NOT COMPILE
short frog = 3 - 2.0; // DOES NOT COMPILE

short mouse = 10;
short hamster = 3;
short capybara = (short)(mouse * hamster);
short capybara = (short)mouse * hamster; // DOES NOT COMPILE

System.out.print(null instanceof Object); // false
System.out.print(null instanceof null); // DOES NOT COMPILE

public void openZoo(Number time) {
 if(time instanceof String) // DOES NOT COMPILE
 System.out.print(time);
}
```
& <-- verifies both operands
&& <-- stops evaluating if the first operand evaluates to false since the result will be false

(x != 0) & (1/x > 1) <-- this means evaluate (x != 0) then evaluate (1/x > 1) then do the &. the problem is that for x=0 this will throw an exception.

(x != 0) && (1/x > 1) <-- this means evaluate (x != 0) and only if this is true then evaluate (1/x > 1) so if you have x=0 then this is perfectly safe and won't throw any exception if (x != 0) evaluates to false the whole thing directly evaluates to false without evaluating the (1/x > 1).

EDIT:

exprA | exprB <-- this means evaluate exprA then evaluate exprB then do the |.

exprA || exprB <-- this means evaluate exprA and only if this is false then evaluate exprB and do the ||.

#### && -> result like multplying
#### || -> result like adding

![Logic operators table](https://github.com/bogdansoft/notes/blob/main/images/logic%20operators.png)

### Shortening Code with Pattern Matching
```
//before Java 16
void compareIntegers(Number number) {
 if(number instanceof Integer) {
 Integer data = (Integer)number;
System.out.print(data.compareTo(5));
 }
}

//with Java 16
void compareIntegers(Number number) {
 if(number instanceof Integer data) {
 System.out.print(data.compareTo(5));
 }
}
```
### Reassigning Pattern Variables
While possible, it is a bad practice to reassign a pattern variable since doing so can lead to 
ambiguity about what is and is not in scope.
```
 if(number instanceof Integer data) {
 data = 10;
 }
 ```
The reassignment can be prevented with a final modifier, but it is better not to reassign 
the variable at all.
```
 if(number instanceof final Integer data) {
 data = 10; // DOES NOT COMPILE
 }
 ```
### Pattern Variables and Expressions
Pattern matching includes expressions that can be used to filter data out, such as in the following example:
```
void printIntegersGreaterThan5(Number number) {
 if(number instanceof Integer data && data.compareTo(5)>0)
 System.out.print(data);
}
```
### Subtypes
The type of the pattern variable must be a subtype of the variable on the left side of the 
expression. It also cannot be the same type. This rule does not exist for traditional instanceof
operator expressions, though. Consider the following two uses of the instanceof operator:
```
Integer value = 123;
if(value instanceof Integer) {}
if(value instanceof Integer data) {} // DOES NOT COMPILE
```
But:
```
Number value = 123;
 if(value instanceof List) {}
 if(value instanceof List data) {}
```
### Flow Scoping
The compiler applies flow scoping when working with pattern matching. Flow scoping
means the variable is only in scope when the compiler can definitively determine its type. 
Flow scoping is unlike any other type of scoping in that it is not strictly hierarchical like instance, class, or local scoping. It is determined by the compiler based on the branching and 
flow of the program.
Given this information, can you see why the following does not compile?
```
void printIntegersOrNumbersGreaterThan5(Number number) {
 if(number instanceof Integer data || data.compareTo(5)>0)//NOT COMPILE
 System.out.print(data);
}
```
But:
```
void printIntegersOrNumbersGreaterThan5(Number number) {
 if(number instanceof Integer data && data.compareTo(5)>0)//COMPILE
 System.out.print(data);
}
```
### Difference between Return, Continue and Break statements
**break**:- These transfer statement bypass the correct flow of execution to outside of the current loop by skipping on the remaining iteration
```
class test
{
    public static void main(String []args)
    {
        for(int i=0;i<10;i++)
        {
            if(i==5)break;
             System.out.println(i);
        }
        System.out.println("hello");
    }
} 

//output will be 
0
1
2
3
4
hello
```
**continue** :-These transfer Statement will bypass the flow of execution to starting point of the loop inorder to continue with next iteration by skipping all the remaining instructions .
```
class test
{
    public static void main(String []args)
    {
        for(int i=0;i<10;i++)
        {
            if(i==5)continue;
            System.out.println(i);
        }
    }
} 

//output will be:
0
1
2
3
4
6
7
8
9 
```
**return** :- At any time in a method the return statement can be used to cause execution to branch back to the caller of the method. Thus, the return statement immediately terminates the method in which it is executed. The following example illustrates this point. Here, return causes execution to return to the Java run-time system, since it is the run-time system that calls main( ).
```
class test
{
    public static void main(String []args)
    {
        for(int i=0;i<10;i++)
        {
            if(i==5)  return;
            System.out.println(i);
        }
        System.out.println("hello");
    }
} 

//output will be :
0
1
2
3
4
```
### Calculating with Math APIs

#### Rounding Numbers
```
public static long round(double num)
public static int round(float num)
```
There are two overloaded methods to ensure that there is enough room to store a 
rounded double if needed. The following shows how to use this method:
```
long low = Math.round(123.45); // 123
long high = Math.round(123.50); // 124
int fromFloat = Math.round(123.45f); // 123
```
```
public static double ceil(double num)
public static double floor(double num)
```
The following shows how to use these methods:
```
double c = Math.ceil(3.14); // 4.0
double f = Math.floor(3.14); // 3.0
```
#### Calculating Exponents
```
public static double pow(double number, double exponent)
```
The following shows how to use this method:
```
double squared = Math.pow(5, 2); // 25.0
```
#### Generating Random Numbers
The random() method returns a value greater than or equal to 0 and less than 1. The method 
signature is as follows:
```
public static double random()
```
The following shows how to use this method:
```
double num = Math.random();
```
Since it is a random number, we can’t know the result in advance. However, we can rule 
out certain numbers. For example, it can’t be negative because that’s less than 0. It can’t be 
1.0 because that’s not less than 1.

### Working with Dates and Times
```
import java.time.*; // import time classes
```
+ LocalDate Contains just a date—no time and no time zone. A good example of LocalDate is your birthday this year. It is your birthday for a full day, regardless of what time it is.
+ LocalTime Contains just a time—no date and no time zone. A good example of 
LocalTime is midnight. It is midnight at the same time every day.
+ LocalDateTime Contains both a date and time but no time zone. A good example of 
LocalDateTime is “the stroke of midnight on New Year’s Eve.” Midnight on January 2 
isn’t nearly as special, making the date relatively unimportant, and clearly an hour after 
midnight isn’t as special either.
+ ZonedDateTime Contains a date, time, and time zone. A good example of 
ZonedDateTime is “a conference call at 9:00 a.m. EST.” If you live in California, 
you’ll have to get up really early since the call is at 6:00 a.m. local time!

You obtain date and time instances using a static method:
```
System.out.println(LocalDate.now());//2021–10–25
System.out.println(LocalTime.now());//09:13:07.768
System.out.println(LocalDateTime.now());//2021–10–25T09:13:07.768
System.out.println(ZonedDateTime.now());//2021–10–25T09:13:07.769–05:00[America/New_York]
```
**Greenwich Mean Time** is a time zone in Europe that is used as time zone zero when discussing offsets. You might have also heard of Coordinated Universal Time, which is a time 
zone standard. It is abbreviated as **UTC**, as a compromise between the English and French 
names. (That’s not a typo. UTC isn’t actually the proper acronym in either language!) UTC 
uses the same time zone zero as GMT.
```
var time1 = LocalTime.of(6, 15); // hour and minute
var time2 = LocalTime.of(6, 15, 30); // + seconds
var time3 = LocalTime.of(6, 15, 30, 200); // + nanoseconds
var d = new LocalDate(); // DOES NOT COMPILE
```

Methods in LocalDate, LocalTime, LocalDateTime, and ZonedDateTime

Methods | Can call on LocalDate? | Can call on LocalTime? | Can call on LocalDateTime or ZonedDateTime?
 --- | --- | --- | ---
plusYears(),minusYears() | Yes | No | Yes
plusMonths(),minusMonths() | Yes | No | Yes
plusWeeks(),minusWeeks() | Yes | No | Yes
plusDays(),minusDays() | Yes | No | Yes
plusHours(),minusHours() | No | Yes | Yes
plusMinutes(),minusMinutes() | No | Yes | Yes
plusSeconds(),minusSeconds() | No | Yes | Yes
plusNanos(),minusNanos() | No | Yes | Yes

#### Working with Periods
LocalDate and LocalDateTime have a method to convert themselves 
into long values, equivalent to the number of milliseconds that have 
passed since January 1, 1970, referred to as the epoch. What’s special 
about this date? That’s what Unix started using for date standards, so 
Java reused it.
```
var annually = Period.ofYears(1); // every 1 year
var quarterly = Period.ofMonths(3); // every 3 months
var everyThreeWeeks = Period.ofWeeks(3); // every 3 weeks
var everyOtherDay = Period.ofDays(2); // every 2 days
var everyYearAndAWeek = Period.of(1, 0, 7); // every year and 7 days
```
#### Working with Durations
You’ve probably noticed by now that a Period is a day or more of time. There is also 
Duration, which is intended for smaller units of time. For Duration, you can specify the 
number of days, hours, minutes, seconds, or nanoseconds. And yes, you could pass 365 days 
to make a year, but you really shouldn’t—that’s what Period is for.
Conveniently, Duration works roughly the same way as Period, except it is used with 
objects that have time. Duration is output beginning with PT, which you can think of as a 
period of time. A Duration is stored in hours, minutes, and seconds. The number of seconds 
includes fractional seconds.
We can create a Duration using a number of different granularities:
```
var daily = Duration.ofDays(1); // PT24H
var hourly = Duration.ofHours(1); // PT1H
var everyMinute = Duration.ofMinutes(1); // PT1M
var everyTenSeconds = Duration.ofSeconds(10); // PT10S
var everyMilli = Duration.ofMillis(1); // PT0.001S
var everyNano = Duration.ofNanos(1); // PT0.000000001S
```

Duration includes another more generic factory method. It takes a number and a 
TemporalUnit. The idea is, say, something like “5 seconds.” However, TemporalUnit is an 
interface. At the moment, there is only one implementation named ChronoUnit.
The previous example could be rewritten like this:
```
var daily = Duration.of(1, ChronoUnit.DAYS);
var hourly = Duration.of(1, ChronoUnit.HOURS);
var everyMinute = Duration.of(1, ChronoUnit.MINUTES);
var everyTenSeconds = Duration.of(10, ChronoUnit.SECONDS);
var everyMilli = Duration.of(1, ChronoUnit.MILLIS);
var everyNano = Duration.of(1, ChronoUnit.NANOS);
```
ChronoUnit also includes some convenient units such as ChronoUnit.HALF_DAYS to 
represent 12 hours.
