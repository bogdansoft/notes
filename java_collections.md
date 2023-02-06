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
Add to back | public boolean add(E e) public boolean offer(E e)
Read from front | public E element() public E peek()
Get and remove from front | public E remove()  public E poll()

####  Deque methods
Functionality | Methods
--- | ---
Add to front | public void addFirst(E e) public boolean offerFirst(E e)
Add to back | public void addLast(E e) public boolean offerLast(E e)
Read from front | public E getFirst() public E peekFirst()
Read from back | public E getLast() public E peekLast()
Get and remove from front | public E removeFirst() public E pollFirst()
Get and remove from back | public E removeLast() public E pollLast()

####  Using a Deque as a stack
Functionality | Methods
--- | ---
Add to the front/top | public void push(E e)
Remove from the front/top | public E pop()
Get first element | public E peek()

#### Using the Map Interface
```
Map.of("key1", "value1", "key2", "value2");
Map.ofEntries(
 Map.entry("key1", "value1"),
 Map.entry("key2", "value2"));
Map.copyOf(map);
```
####  Map methods
Method | Description
--- | ---
public void clear() | Removes all keys and values from map.
public boolean containsKey(Object key) | Returns whether key is in map.
public boolean containsValue(Object value) | Returns whether value is in map.
public Set<Map.Entry<K,V>> entrySet() | Returns Set of key/value pairs.
public void forEach(BiConsumer<K key, V value>) | Loops through each key/value pair.
public V get(Object key) | Returns value mapped by key or null if none is mapped.
public V getOrDefault(Object key, V defaultValue) | Returns value mapped by key or default value if none is mapped.
public boolean isEmpty() | Returns whether map is empty.
public Set<K> keySet() | Returns set of all keys.
public V merge(K key, V value, Function(<V, V, V> func)) | Sets value if key not set. Runs function if key is set, to determine new value. Removes if value is null.
public V put(K key, V value) | Adds or replaces key/value pair. Returns previous value or null.
public V putIfAbsent(K key, V value) | Adds value if key not present and returns null. Otherwise, returns existing value.
public V remove(Object key) | Removes and returns value mapped to key. Returns null if none.
public V replace(K key, V value) | Replaces value for given key if key is set. Returns original value or null if none.
public void replaceAll(BiFunction<K, V, V> func) | Replaces each value with results of function.
public int size() | Returns number of entries (key/value pairs) in map.
public Collection<V> values() | Returns Collection of all values.

#### Putting if Absent
The putIfAbsent() method sets a value in the map but skips it if the value is already set to a 
non-null value.
```
Map<String, String> favorites = new HashMap<>();
favorites.put("Jenny", "Bus Tour");
favorites.put("Tom", null);
favorites.putIfAbsent("Jenny", "Tram");
favorites.putIfAbsent("Sam", "Tram");
favorites.putIfAbsent("Tom", "Tram");
System.out.println(favorites); // {Tom=Tram, Jenny=Bus Tour, Sam=Tram}
```
#### Merging Data
The merge() method adds logic of what to choose. Suppose we want to choose the ride with 
the longest name. We can write code to express this by passing a mapping function to the 
merge() method:
```
BiFunction<String, String, String> function = (v1, v2) -> v1.length() > v2.length() ? v1 : v2;
Map<String, String> map = new HashMap<>();
map.put("Jenny", "Bus Tour");
map.put("Tom", "Tram");

var jenny = map.merge("Jenny", "Skyride", function);
var tom = map.merge("Tom", "Skyride", function);

map.forEach((key, value) -> System.out.println(key + " " + value));//Tom Skyride Jenny BusTour
System.out.println(jenny);//Bus Tour
System.out.println(tom);//Skyride
```

Notice that the mapping function isn’t called. If it were, we’d have a 
NullPointerException. The mapping function is used only when there are two actual 
values to decide between.

####  Behavior of the merge() method
If the requested key | And mapping function returns | Then:
--- | --- | ---
Has a null value in map | N/A(mapping function not called) | Update key’s value in map with value parameter 
Has a non-null value in map | null | Remove key from map
Has a non-null value in map | A non-null value | Set key to mapping function result
Is not in map | N/A(mapping function not called) | Add key with value parameter to map directly without calling mapping function

### Comparing Collection Types
####  Java Collections Framework types
Type | Can contain duplicate elements? | Elements always ordered? | Has keys and values? | Must add/remove in specific order?
--- | --- | --- | --- | ---
List | Yes | Yes(by index) | No | No
Map | Yes(for values) | No | Yes | No
Queue | Yes | Yes(retrieved in defined order) | No | Yes
Set | No | No|  No|  No

#### Collection attributes
Type | Interface | Sorted? | Calls hashCode? | Calls compareTo?
--- | --- | --- | --- | ---
ArrayDeque | Deque | No | No | No
ArrayList | List | No | No | No
HashMap | Map | No | Yes | No
HashSet | Set | No | Yes | No
LinkedList | List, Deque | No | No | No
TreeMap | Map | Yes | No | Yes
TreeSet | Set | Yes | No | Yes

### Sorting Data
**When working with a String, remember that numbers sort before 
letters, and uppercase letters sort before lowercase letters.**

#### Creating a Comparable Class
The Comparable interface has only one method. In fact, this is the entire interface:
```
public interface Comparable<T> {
 int compareTo(T o);
}
```
```
import java.util.*;
public class Duck implements Comparable<Duck> {
 private String name;
 public Duck(String name) {
 this.name = name;
 }
 public String toString() { // use readable output
 return name;
 }
public int compareTo(Duck d) {
 return name.compareTo(d.name); // sorts ascendingly by name
 }
 public static void main(String[] args) {
 var ducks = new ArrayList<Duck>();
 ducks.add(new Duck("Quack"));
 ducks.add(new Duck("Puddles"));
 Collections.sort(ducks); // sort by name
 System.out.println(ducks); // [Puddles, Quack]
}}
```
```
public class Main {
    public static void main(String[] args) {
        Product first = new Product(1, "kiwi");
        Product second = new Product(2, "apple");
        System.out.println(first.compareTo(second));//10

        Comparator<Product> byId = Comparator.comparingInt(Product::getId);
        var list = new ArrayList<>(Arrays.asList(second, first));
        list.forEach(System.out::println);
        //2 apple
        //1 kiwi

        Collections.sort(list, byId);
        list.forEach(System.out::println);
        //1 kiwi
        //2 apple
    }
}

class Product implements Comparable<Product> {
    private Integer id;
    private String name;

    public Product(Integer id, String name) {
        this.id = id;
        this.name = name;
    }

    public Integer getId() {
        return id;
    }

    public void setId(Integer id) {
        this.id = id;
    }

    public String getName() {
        return name;
    }

    public void setName(String name) {
        this.name = name;
    }

    @Override
    public int hashCode() {
        return super.hashCode();
    }

    @Override
    public boolean equals(Object obj) {
        return super.equals(obj);
    }

    @Override
    public int compareTo(Product o) {
        return this.name.compareTo(o.name);
    }

    @Override
    public String toString() {
        return id + " " + name;
    }
}
```

#### Comparison of Comparable and Comparator
Difference | Comparable | Comparator
--- | --- | ---
Package name | java.lang | java.util 
Interface must be implemented by class comparing? | Yes | No
Method name in interface | compareTo() | compare()
Number of parameters | 1 | 2
Common to declare using a lambda | No | Yes
