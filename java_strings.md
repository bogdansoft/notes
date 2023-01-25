## Strings
```
System.out.println(1 + 2); // 3
System.out.println("a" + "b"); // ab
System.out.println("a" + "b" + 3); // ab3
System.out.println(1 + 2 + "c"); // 3c
System.out.println("c" + 1 + 2); // c12
System.out.println("c" + null); // cnull
```
### Concatination
```
 String s="Sachin"+" Tendulkar";  
 System.out.println(s);//Sachin Tendulkar 
 ```
The Java compiler transforms above code to this:
```
String s=(new StringBuilder()).append("Sachin").append(" Tendulkar).toString();  
```
In Java, String concatenation is implemented through the StringBuilder (or StringBuffer) class and it's append method. String concatenation operator produces a new String by appending the second operand onto the end of the first operand. The String concatenation operator can concatenate not only String but primitive values also.
