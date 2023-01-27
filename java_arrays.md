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
