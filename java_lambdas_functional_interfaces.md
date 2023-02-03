## Lambdas and Functional Interfaces

#### Assigning Lambdas to var
```
var invalid = (Animal a) -> a.canHop(); // DOES NOT COMPILE
```
var assumes the type based on the context as well. There’s not enough context here! Neither the lambda nor var have enough information to determine what type of 
functional interface should be used.
Is the Soar class a functional interface?
```
@FunctionalInterface//DOES NOT COMPILE
public interface Soar {
 abstract String toString();
}
```
It is not. Since toString() is a public method implemented in Object, it does not 
count toward the single abstract method test. On the other hand, the following implementation of Dive is a functional interface:
```
@FunctionalInterface//COMPILE
public interface Dive {
 String toString();
 public boolean equals(Object o);
 public abstract int hashCode();
 public void dive();
}
```
The dive() method is the single abstract method, while the others are not counted since they are public methods defined in the Object class.
