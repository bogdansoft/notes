## Lambdas and Functional Interfaces

#### Assigning Lambdas to var
```
var invalid = (Animal a) -> a.canHop(); // DOES NOT COMPILE
```
var assumes the type based on the context as well. There’s not enough context here! Neither the lambda nor var have enough information to determine what type of 
functional interface should be used.
