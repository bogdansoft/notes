#### Runtime exceptions( Unchecked exceptions)

Unchecked exception | Description
--- | ---
ArithmeticException | Thrown when code attempts to divide by zero.
ArrayIndexOutOfBoundsException | Thrown when code uses illegal index to access array.
ClassCastException | Thrown when attempt is made to cast object to class of which it is not an instance.
NullPointerException | Thrown when there is a null reference where an object is required.
IllegalArgumentException | Thrown by programmer to indicate that method has been passed illegal or inappropriate argument.
NumberFormatException(Subclass of IllegalArgumentException) | Thrown when attempt is made to convert String to numeric type but String doesn’t have appropriate format.

#### Checked Exceptions
Checked exception | Description
--- | ---
FileNotFoundException (Subclass of IOException) | Thrown programmatically when code tries to reference file that does not exist.
IOException | Thrown programmatically when problem reading or writing file.
NotSerializableException (Subclass of IOException) | Thrown programmatically when attempting to serialize or deserialize nonserializable class.
ParseException | Indicates problem parsing input.
SQLException | Thrown when error related to accessing database.

####  Errors
Error | Description
--- | ---
ExceptionInInitializerError | Thrown when static initializer throws exception and doesn’t handle it
StackOverflowError | Thrown when method calls itself too many times (called infinite recursion because method typically calls itself without end)
NoClassDefFoundError | Thrown when class that code uses is available at compile time but not runtime
```
public void visitSnakes() {
 try {
 } catch (IllegalArgumentException e) {
 } catch (NumberFormatException e) { // DOES NOT COMPILE
 }
}
```
Since NumberFormatException is a subclass, it will always be caught by the first catch block, 
making the second catch block unreachable code that does not compile. Likewise, for the 
exam, you need to know that FileNotFoundException is a subclass of IOException and 
cannot be used in a similar manner.
```
public void visitManatees() {
 try {
 } catch (NumberFormatException e1) {
 System.out.println(e1);
 } catch (IllegalArgumentException e2) {
 System.out.println(e1); // DOES NOT COMPILE
 }
}
```
