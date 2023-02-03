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
#### Applying a Multi-catch Block
```
catch(Exception1 e | Exception2 e | Exception3 e) // DOES NOT COMPILE
catch(Exception1 e1 | Exception2 e2 | Exception3 e3) // DOES NOT COMPILE
catch(Exception1 | Exception2 | Exception3 e)

try {
 throw new IOException();
} catch (FileNotFoundException | IOException p) {} // DOES NOT COMPILE since FileNotFoundException is a subclass of IOException
```
Specifying related exceptions in the multi-catch is redundant, and the compiler gives a 
message such as this:
```
The exception FileNotFoundException is already caught by the alternative IOException
```
```
try { // DOES NOT COMPILE catch and finally blocks are in the wrong order
fall();
} finally {
System.out.println("all better");
} catch (Exception e) {
System.out.println("get up");
}
try { // DOES NOT COMPILE there must be a catch or finally block
fall();
}
try {
 // Protected code
} catch (exception_type identifier) {
 // Exception handler
} finally {
 
 // finally block
}
```
The finally block always executes, whether or not an exception occurs.
```
try {
fall();
} finally {
System.out.println("all better");
}
```
#### Introducing Try-with-Resources
Let’s take a look at a method that opens a file, reads the data, and closes it:
```
public void readFile(String file) {
FileInputStream is = null;
try {
is = new FileInputStream("myfile.txt");
// Read file data
} catch (IOException e) {
 e.printStackTrace();
 } finally {
 if(is != null) {
 try {
 is.close();
 } catch (IOException e2) {
 e2.printStackTrace();
 }
 }
 }
```
 Let’s take a look at our same example using a try-with-resources statement:
```
public void readFile(String file) {
try (FileInputStream is = new FileInputStream("myfile.txt")) {
// Read file data
} catch (IOException e) {
e.printStackTrace();
}
 }
```

Behind the scenes, the compiler replaces a try-with-resources block with a try and finally
block. We refer to this “hidden” finally block as an implicit finally block since it is created 
and used by the compiler automatically. You can still create a programmer-defined finally
block when using a try-with-resources statement; just be aware that the implicit one will be 
called first.
}
**Inheriting AutoCloseable requires implementing a compatible close() method**
```
interface AutoCloseable {
 public void close() throws Exception;
}
```
