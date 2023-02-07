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

####  Access control with modules
Level | Within module code | Outside module
--- | --- | ---
private | Available only within class | No access
Package | Available only within package | No access
protected | Available only within package or to subclasses | Accessible to subclasses only if package is exported
public | Available to all classes | Accessible only if package is exported

####  Reviewing directives
Directive | Description
--- | ---
exports package; exports package to module; | Makes package available outside module
requires module; requires transitive module; | Specifies another module as dependency
opens package; opens package to module; | Allows package to be used with reflection
provides serviceInterface with implName; | Makes service available
uses serviceInterface; | References service
