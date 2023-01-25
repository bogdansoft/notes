## Strings
```
System.out.println(1 + 2); // 3
System.out.println("a" + "b"); // ab
System.out.println("a" + "b" + 3); // ab3
System.out.println(1 + 2 + "c"); // 3c
System.out.println("c" + 1 + 2); // c12
System.out.println("c" + null); // cnull
```
### Concatenation
```
 String s="Sachin"+" Tendulkar";  
 System.out.println(s);//Sachin Tendulkar 
 ```
The Java compiler transforms above code to this:
```
String s=(new StringBuilder()).append("Sachin").append(" Tendulkar).toString();  
```
In Java, String concatenation is implemented through the StringBuilder (or StringBuffer) class and it's append method. String concatenation operator produces a new String by appending the second operand onto the end of the first operand. The String concatenation operator can concatenate not only String but primitive values also.
```
String str = "knowledge";
```
This, as usual, creates a string containing “knowledge” and assigns it to reference str. Simple enough? Let us perform some more functions:
```
// assigns a new reference to the 
// same string "knowledge"
String s = str;     
```
Let’s see how the below statement works:
```
  str = str.concat(" base");
```
This appends a string ” base” to str. But wait, how is this possible, since String objects are immutable? Well to your surprise, it is.

When the above statement is executed, the VM takes the value of String str, i.e. “knowledge” and appends ” base”, giving us the value “knowledge base”. Now, since Strings are immutable, the VM can’t assign this value to str, so it creates a new String object, gives it a value “knowledge base”, and gives it reference str.

An important point to note here is that, while the String object is immutable, its reference variable is not. So that’s why, in the above example, the reference was made to refer to a newly formed String object.
