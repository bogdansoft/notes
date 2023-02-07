## Java Modules
```
module $NAME {
    // for each dependency:
    requires $MODULE;

    // for each API package:
    exports $PACKAGE

    // for each package intended for reflection:
    opens $PACKAGE;

    // for each used service:
    uses $TYPE;

    // for each provided service:
    provides $TYPE with $CLASS;
}
```
#### Exported Types
We’ve been talking about exporting a package. But what does that mean, exactly? All 
public classes, interfaces, enums, and records are exported. Further, any public and 
protected fields and methods in those files are visible.
Fields and methods that are private are not visible because they are not accessible 
outside the class. Similarly, package fields and methods are not visible because they are not 
accessible outside the package.
