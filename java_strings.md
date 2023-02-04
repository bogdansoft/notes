## Strings, Formats
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

**You need to remember that a string is a sequence of characters and Java counts from 0 when indexed**

#### String methods
##### public int length() 
```
var name = "animals";
System.out.println(name.length()); // 7
```
##### public char charAt(int index)
```
var name = "animals";
System.out.println(name.charAt(0)); // a
System.out.println(name.charAt(6)); // s
System.out.println(name.charAt(7)); // exception
```
##### public int indexOf(int ch)
public int indexOf(int ch, int fromIndex)

public int indexOf(String str)

public int indexOf(String str, int fromIndex)

The following code shows you how to use indexOf():
```
var name = "animals";
System.out.println(name.indexOf('a')); // 0
System.out.println(name.indexOf("al")); // 4
System.out.println(name.indexOf('a', 4)); // 4
System.out.println(name.indexOf("al", 5)); // -1
```
Unlike charAt(), the indexOf()
method doesn’t throw an exception if it can’t find a match, instead returning –1. Because 
indexes start with 0, the caller knows that –1 couldn’t be a valid index. This makes it a 
common value for a method to signify to the caller that no match is found.

##### Substring
```
public String substring(int beginIndex)
public String substring(int beginIndex, int endIndex)
```
```
var name = "animals";
System.out.println(name.substring(3)); // mals
System.out.println(name.substring(name.indexOf('m'))); // mals
System.out.println(name.substring(3, 4)); // m
System.out.println(name.substring(3, 7)); // mals

System.out.println(name.substring(3, 3)); // empty string
System.out.println(name.substring(3, 2)); // exception
System.out.println(name.substring(3, 8)); // exception
```
##### Searching for Substrings
```
public boolean startsWith(String prefix)
public boolean endsWith(String suffix)
public boolean contains(CharSequence charSeq)
```
The following code shows how to use these methods:
```
System.out.println("abc".startsWith("a")); // true
System.out.println("abc".startsWith("A")); // false

System.out.println("abc".endsWith("c")); // true
System.out.println("abc".endsWith("a")); // false

System.out.println("abc".contains("b")); // true
System.out.println("abc".contains("B")); // false
```
##### Replacing Values
```
public String replace(char oldChar, char newChar)
public String replace(CharSequence target, CharSequence replacement)
```
The following code shows how to use these methods:
```
System.out.println("abcabc".replace('a', 'A')); // AbcAbc
System.out.println("abcabc".replace("a", "A")); // AbcAbc
```
##### Removing Whitespace
These methods remove blank space from the beginning and/or end of a String. The strip()
and trim() methods remove whitespace from the beginning and end of a String. 
```
public String strip()//removes whitespace from the beginning and end of a String and supports Unicode 
public String stripLeading()//removes whitespace from the beginning of the String and leaves it at the end
public String stripTrailing()//removes whitespace from the end of the String and leaves it at the beginning
public String trim()//removes whitespace from the beginning and end of a String
```
The following code shows how to use these methods:
```
System.out.println("abc".strip()); // abc
System.out.println("\t a b c\n".strip()); // a b c

String text = " abc\t ";
System.out.println(text.trim().length()); // 3
System.out.println(text.strip().length()); // 3
System.out.println(text.stripLeading().length()); // 5
System.out.println(text.stripTrailing().length());// 4
```
##### Working with Indentation
Now that Java supports text blocks, it is helpful to have methods that deal with indentation. 
```
public String indent(int numberSpaces)
public String stripIndent()
```
The indent() method adds the same number of blank spaces to the beginning of each 
line if you pass a positive number. If you pass a negative number, it tries to remove that 
number of whitespace characters from the beginning of the line. If you pass zero, the indentation will not change.

The stripIndent() method is useful when a String was built with concatenation rather than 
using a text block. It gets rid of all incidental whitespace. This means that all non-blank lines 
are shifted left so the same number of whitespace characters are removed from each line and 
the first character that remains is not blank. Like indent(), \r\n is turned into \n. However, the 
stripIndent() method does not add a trailing line break if it is missing.

**Rules for indent() and stripIndent()**
Method | Indent change | Normalizes existing line breaks| Adds line break at end if missing
--- | --- | --- | ---
indent(n) where n > 0 |Adds n spaces to beginning of each line | Yes | Yes
indent(n) where n == 0 | No change | Yes|  Yes
indent(n) where n < 0 | Removes up to n spaces from each line where the same number of characters is removed from each non-blank line | Yes | Yes
stripIndent() | Removes all leading incidental whitespace | Yes | No

```
10: var block = """
11: a
12:  b
13: c""";
14: var concat = " a\n"
15: + " b\n"
16: + " c";
17: System.out.println(block.length()); // 6
18: System.out.println(concat.length()); // 9
19: System.out.println(block.indent(1).length()); // 10
20: System.out.println(concat.indent(-1).length()); // 7
21: System.out.println(concat.indent(-4).length()); // 6
22: System.out.println(concat.stripIndent().length()); // 6
```

Line 17 counts the six characters in block, which are the three letters, the blank space 
before b, and the \n after a and b.

##### Translating Escapes
```
public String translateEscapes()
```
The following code shows how to use these methods:
```
var str = "1\\t2";
System.out.println(str); // 1\t2
System.out.println(str.translateEscapes()); // 1 2
```
The first line prints the literal string \t because the backslash is escaped. The second 
line prints an actual tab since we translated the escape. This method can be used for escape 
sequences such as \t (tab), \n (new line), \s (space), \" (double quote), and \' (single quote.

### Formatting Values

```
public static String format(String format, Object args...)
public static String format(Locale loc, String format, Object args...)
public String formatted(Object args...)
```
The following code shows how to use these methods:
```
var name = "Kate";
var orderId = 5;
// All print: Hello Kate, order 5 is ready
System.out.println("Hello "+name+", order "+orderId+" is ready");
System.out.println(String.format("Hello %s, order %d is ready", 
 name, orderId));
System.out.println("Hello %s, order %d is ready"
 .formatted(name, orderId));
 ```
In the format() and formatted() operations, the parameters are inserted and formatted via symbols in the order that they are provided in the vararg. 

#### Common formatting symbols
Symbol | Description
--- | ---
%s | Applies to any type, commonly String values
%d | Applies to integer values like int and long
%f | Applies to floating-point values like float and double
%n | Inserts a line break using the system-dependent line separator

```
var name = "James";
var score = 90.25;
var total = 100;
System.out.println("%s:%n Score: %f out of %d".formatted(name, score, total));
```
This prints the following:
```
James:
   Score: 90.250000 out of 100
```
Mixing data types may cause exceptions at runtime. For example, the following throws 
an exception because a floating-point number is used when an integer value is expected:
```
var str = "Food: %d tons".formatted(2.0); // IllegalFormatConversionException
```
### StringBuilder
```
StringBuilder sb1 = new StringBuilder();
StringBuilder sb2 = new StringBuilder("animal");
StringBuilder sb3 = new StringBuilder(10);//capacity
```
append()
```
var sb = new StringBuilder().append(1).append('c');
sb.append("-").append(true);
System.out.println(sb); // 1c-true
```
### Inserting Data
```
public StringBuilder insert(int offset, String str)
```
Pay attention to the offset in these examples. It is the index where we want to insert the 
requested parameter.
```
var sb = new StringBuilder("animals");
sb.insert(7, "-"); // sb = animals
sb.insert(0, "-"); // sb = -animals
sb.insert(4, "-"); // sb = -ani-mals
System.out.println(sb);
```

#### Deleting Contents
```
public StringBuilder delete(int startIndex, int endIndex)
public StringBuilder deleteCharAt(int index)
```
```
var sb = new StringBuilder("abcdef");
sb.delete(1, 3); // sb = adef
sb.deleteCharAt(5); // exception
```
The delete() method is more flexible than some others when it comes to array indexes. 
If you specify a second parameter that is past the end of the StringBuilder, Java will just 
assume you meant the end. That means this code is legal:
```
var sb = new StringBuilder("abcdef");
sb.delete(1, 100); // sb = a
```
#### Replacing Portions 
```
public StringBuilder replace(int startIndex, int endIndex, String newString)
```
The following code shows how to use this method:
```
var builder = new StringBuilder("pigeon dirty");
builder.replace(3, 6, "sty");
System.out.println(builder); // pigsty dirty
```
First, Java deletes the characters starting with index 3 and ending right before index 6. 
This gives us pig dirty. Then Java inserts the value "sty" in that position.
In this example, the number of characters removed and inserted are the same. However, 
there is no reason they have to be.
```
var builder = new StringBuilder("pigeon dirty");
builder.replace(3, 100, "");
System.out.println(builder);//pig
```
#### Reversing
```
public StringBuilder reverse()
```
```
var sb = new StringBuilder("ABC");
sb.reverse();
System.out.println(sb);//CBA
```
**Often StringBuilder is used internally for performance purposes**, but the end result 
needs to be a String. For example, maybe it needs to be passed to another method that is 
expecting a String.

#### Comparing equals() and ==
Consider the following code that uses == with objects:
```
var one = new StringBuilder();
var two = new StringBuilder();
var three = one.append("a");
System.out.println(one == two); // false
System.out.println(one == three); // true
```
```
var name = "a";
var builder = new StringBuilder("a");
System.out.println(name == builder); // DOES NOT COMPILE
```
#### Intern method
```
var x = "Hello World";
var y = new String("Hello World");
System.out.println(x == y); // false
```
You can also do the opposite and tell Java to use the string pool. The intern() method will 
use an object in the string pool if one is present.
```
public String intern()
```
If the literal is not yet in the string pool, Java will add it at this time.
```
var name = "Hello World";
var name2 = new String("Hello World").intern();
System.out.println(name == name2); // true
```

#### Formatting Values
```
public final String format(double number)
public final String format(long number)
```
```
double d = 12345.678;
System.out.println(new DecimalFormat("###,###,###.00").format(d));//12,345.68
System.out.println(new DecimalFormat("000,000,000.00000").format(d));//000,012,345.67800
System.out.println(new DecimalFormat("Your Balance $#,###,###.##").format(d));//Your Balance $12,345.68
```
#### DecimalFormat symbols
Symbol | Meaning | Examples
--- | --- | ---
# | Omit position if no digit exists for it. | $2.2
0 | Put 0 in position if no digit exists for it. | $002.20
