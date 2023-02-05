## Collections
#### Counting Elements for List
The isEmpty() and size() methods look at how many elements are in the Collection. The 
method signatures are as follows:
```
public boolean isEmpty()
public int size()
The following shows how to use these methods:
Collection<String> birds = new ArrayList<>();
System.out.println(birds.isEmpty()); // true
System.out.println(birds.size()); // 0
```
#### Clearing the Collection
The clear() method provides an easy way to discard all elements of the Collection. The method 
signature is as follows:
```
public void clear()
```
The following shows how to use this method:
```
Collection<String> birds = new ArrayList<>();
birds.add("hawk"); // [hawk]
birds.add("hawk"); // [hawk, hawk]
System.out.println(birds.isEmpty()); // false
System.out.println(birds.size()); // 2
birds.clear(); // []
```
#### Check Contents
The contains() method checks whether a certain value is in the Collection. The method 
signature is as follows:
```
public boolean contains(Object object)
```
The following shows how to use this method:
```
Collection<String> birds = new ArrayList<>();
birds.add("hawk"); // [hawk]
System.out.println(birds.contains("hawk")); // true
System.out.println(birds.contains("robin")); // false
```
#### Removing
```
public boolean remove(Object object)
public boolean removeIf(Predicate<? super E> filter)
```
#### Iterating
```
public void forEach(Consumer<? super T> action)
```
#### Factory methods to create a List
Method | Description | Can add elements? | Can replace elements? | Can delete elements?
--- | --- | --- | --- | ---
Arrays.asList(varargs) | Returns fixed size list backed by an array | No | Yes | No
List.of(varargs) | Returns immutable list | No | No | No
List.copyOf(collection) | Returns immutable list with copy of original collection’s values | No | No | No

####  List methods
Method | Description
--- | ---
public boolean add(E element) | Adds element to end (available on all Collection APIs).
public void add(int index, E element) | Adds element at index and moves the rest toward the end.
public E get(int index) | Returns element at index.
public E remove(int index) | Removes element at index and moves the rest toward the front.
public default void replaceAll(UnaryOperator<E> op) | Replaces each element in list with result of operator.
public E set(int index, E e) | Replaces element at index and returns original. Throws IndexOutOfBoundsException if index is invalid.
public default void sort(Comparator<? super E> c) | Sorts list. We cover this later in the chapter in the “Sorting Data” section.

#### Converting from List to an Array
```
List<String> list = new ArrayList<>();
list.add("hawk");
list.add("robin");
Object[] objectArray = list.toArray();
String[] stringArray = list.toArray(new String[0]);
list.clear();
System.out.println(objectArray.length); // 2
System.out.println(stringArray.length); // 2
```
#### Working with Set Methods
```
Set<Character> letters = Set.of('z', 'o', 'o');
Set<Character> copy = Set.copyOf(letters);
```
**The main benefit of a LinkedList is that it implements both the List and Deque
interfaces. The trade-off is that it isn’t as efficient as a “pure” queue. You can use the 
ArrayDeque class if you don’t need the List methods.**

#### Queue methods
Functionality | Methods
--- | ---
Add to back | public boolean add(E e)
public boolean offer(E e)
Read from front | public E element()
public E peek()
Get and remove from front | public E remove() 
public E poll()
