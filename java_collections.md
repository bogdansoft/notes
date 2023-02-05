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
