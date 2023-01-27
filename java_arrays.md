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
System.out.println(Arrays.compare(new int[] {1}, new String[] {"a"})); // DOES NOT COMPILE
```
Now that you know how to compare a single value, let’s look at how to compare arrays 
of different lengths:
- If both arrays are the same length and have the same values in each spot in the same 
order, return zero.
- If all the elements are the same but the second array has extra elements at the end, 
return a negative number.
- If all the elements are the same, but the first array has extra elements at the end, return a 
positive number.
- If the first element that differs is smaller in the first array, return a negative number.
- If the first element that differs is larger in the first array, return a positive number.

Finally, what does smaller mean? Here are some more rules that apply here and to 
compareTo():
- null is smaller than any other value.
- For numbers, normal numeric order applies.
- For strings, one is smaller if it is a prefix of another.
- For strings/characters, numbers are smaller than letters.
- For strings/characters, uppercase is smaller than lowercase.

#### Using mismatch()
If the arrays are equal, mismatch() returns -1. Otherwise, it returns the first index where they differ.
```
System.out.println(Arrays.mismatch(new int[] {1}, new int[] {1}));//-1
System.out.println(Arrays.mismatch(new String[] {"a"}, new String[] {"A"}));//0
System.out.println(Arrays.mismatch(new int[] {1, 2}, new int[] {1}));//1
```
Method | When arrays contain the same data | When arrays are different
--- | --- | ---
equals() | true | false
compare() | 0 | Positive or negative number
mismatch() | -1 | Zero or positive index

### Multidimensional Array
```
int[][] vars1; // 2D array
int vars2 [][]; // 2D array
int[] vars3[]; // 2D array
int[] vars4 [], space [][]; // a 2D AND a 3D array
```
```
var twoD = new int[3][2];
for(int i = 0; i < twoD.length; i++) {
 for(int j = 0; j < twoD[i].length; j++)
 System.out.print(twoD[i][j] + " "); // print element
 System.out.println(); // time for a new row
}
```
