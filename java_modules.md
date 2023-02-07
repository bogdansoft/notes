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
