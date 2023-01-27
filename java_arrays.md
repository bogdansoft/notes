## Arrays
```
int[] moreNumbers = {42, 55, 99};
```
This approach is called an **anonymous array**. It is anonymous because you don’t specify 
the type and size.
Finally, you can type the [] before or after the name, and adding a space is optional. This 
means that all five of these statements do the exact same thing:
```
int[] numAnimals;
int [] numAnimals2;
int []numAnimals3;
int numAnimals4[];
int numAnimals5 [];
```
#### Multiple “Arrays” in Declarations
```
int[] ids, types;//int[],int[]
```
The correct answer is two variables of type int[]. This seems logical enough. After all, 
int a, b; created two int variables. What about this example?
```
 int ids[], types;//int[],int
 ```
All we did was move the brackets, but it changed the behavior. This time we get one variable 
of type int[] and one variable of type int. 

### Searching
Scenario | Result
--- | ---
Target element found in sorted array | Index of match
Target element not found in sorted array | Negative value showing one smaller than the negative of the index, where a match needs to be inserted to preserve sorted order
Unsorted array | A surprise; this result is undefined

```
int[] numbers = {2,4,6,8};
System.out.println(Arrays.binarySearch(numbers, 2)); // 0
System.out.println(Arrays.binarySearch(numbers, 4)); // 1
System.out.println(Arrays.binarySearch(numbers, 1)); // -1
System.out.println(Arrays.binarySearch(numbers, 3)); // -2
System.out.println(Arrays.binarySearch(numbers, 9)); // -5
```
```
int[] numbers = new int[] {3,2,1};//unsorted
System.out.println(Arrays.binarySearch(numbers, 2));
System.out.println(Arrays.binarySearch(numbers, 3));
```
### Comparing
#### Using compare()
+ A negative number means the first array is smaller than the second.
+ A zero means the arrays are equal.
+ A positive number means the first array is larger than the second.
Here’s an example:
```
System.out.println(Arrays.compare(new int[] {1}, new int[] {2}));//-1
```
