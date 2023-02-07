## Lambdas and Functional Interfaces and Streams

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
count toward the single abstract method test. On the other hand, the following implementation of Dive is a functional interface:
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

####  Common functional interfaces
Functional interface | Return type | Method name | # of parameters
--- | --- | --- | ---
Supplier<T> | T | get() | 0
Consumer<T> | void | accept(T)|  1 (T)
BiConsumer<T, U> | void | accept(T,U) | 2 (T, U)
Predicate<T> | boolean | test(T) | 1 (T)
BiPredicate<T, U> | boolean | test(T,U) | 2 (T, U)
Function<T, R> | R | apply(T) | 1 (T)
BiFunction<T, U, R> | R | apply(T,U) | 2 (T, U)
UnaryOperator<T> | T | apply(T) | 1 (T)
BinaryOperator<T> | T | apply(T,T) | 2 (T, T)

 ####  Convenience methods
Interface instance | Method return type | Method name | Method parameters
 --- | --- | --- | ---
Consumer | Consumer | andThen() | Consumer
Function | Function | andThen() | Function
Function | Function | compose() | Function
Predicate | Predicate | and() | Predicate
Predicate | Predicate | negate() | —
Predicate | Predicate | or() | Predicate

 #### Parameter List Formats
You have three formats for specifying parameter types within a lambda: without types, with 
types, and with var. The compiler requires all parameters in the lambda to use the same 
format.
 ```
5: (var x, y) -> "Hello" // DOES NOT COMPILE
6: (var x, Integer y) -> true // DOES NOT COMPILE
7: (String x, var y, Integer z) -> true // DOES NOT COMPILE
8: (Integer x, y) -> "goodbye" // DOES NOT COMPILE
```
Lines 5 needs to remove var from x or add it to y. Next, lines 6 and 7 need to use the type 
or var consistently. Finally, line 8 needs to remove Integer from x or add a type to y.

 ## Optional
#### Common Optional instance methods
Method | When Optional is empty | When Optional contains value
 --- | --- | ---
get() | Throws exception | Returns value
ifPresent(Consumer c) | Does nothing | Calls Consumer with value
isPresent() | Returns false | Returns true
orElse(T other) | Returns other parameter | Returns value
orElseGet(Supplier s) | Returns result of calling Supplier | Returns value
orElseThrow() | Throws NoSuchElementException | Returns value
orElseThrow(Supplier s) | Throws exception created by calling Supplier | Returns value

 ####  Optional types for primitives
Option | OptionalDouble | OptionalInt | OptionalLong
 --- | --- | --- | ---
Getting as primitive | getAsDouble() | getAsInt() | getAsLong()
orElseGet() parameter type | DoubleSupplier | IntSupplier | LongSupplier
Return type of max() and min() | OptionalDouble | OptionalInt | OptionalLong
Return type of sum() | double | int | long
Return type of average() | OptionalDouble | OptionalDouble | OptionalDouble
 
 ## Streams
 ####  Creating a source
Method | Finite or infinite? | Notes
 --- | --- | ---
Stream.empty() | Finite | Creates Stream with zero elements.
Stream.of(varargs) | Finite | Creates Stream with elements listed.
coll.stream() | Finite | Creates Stream from Collection.
coll.parallelStream() | Finite | Creates Stream from Collection where the stream can run in parallel.
Stream.generate(supplier) | Infinite | Creates Stream by calling Supplier for each element upon request.
Stream.iterate(seed,unaryOperator) | Infinite | Creates Stream by using seed for first element and then calling UnaryOperator for each subsequent element upon request.
Stream.iterate(seed,predicate, unaryOperator) | Finite or infinite | Creates Stream by using seed for first element and then calling UnaryOperator for each subsequent element upon request. Stops if Predicate returns false

 #### Grouping, Partitioning, and Mapping
 ```
var ohMy = Stream.of("lions", "tigers", "bears");
Map<Integer, List<String>> map = ohMy.collect(Collectors.groupingBy(String::length));
System.out.println(map);//{5=[lions, bears], 6=[tigers]}
```
```
var ohMy = Stream.of("lions", "tigers", "bears");
Map<Integer, Set<String>> map = ohMy.collect(
 Collectors.groupingBy(
 String::length,
 Collectors.toSet()));
System.out.println(map); // {5=[lions, bears], 6=[tigers]}
```
