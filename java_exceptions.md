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
NotSerializableException (Subclass of IOException) | Thrown programmatically when attempting to serialize or deserialize nonserializable class.
ParseException | Indicates problem parsing input.
SQLException | Thrown when error related to accessing database.
