#### DRY - Don't Repeat Yourself 
+ Avoid Duplication in Comments of code
+ Avoid DATA/logic-based duplication
+ Avoid Algorithm duplication

#### KISS Principle - Keep it Simple, Stupid 

Few ways by which a programmer can reduce complexity:
+ The variable names in a program should serve their purpose well. They should be able to define the variable properly
+ Method name should also be in line with the purpose for which the method is employed
+ As mentioned in an earlier example in the DRY principle, comments in the method should be used only when your program is not able to define the method completely
+ Classes should be designed in a way to own a single responsibility
+ Delete redundant processes and algorithms as explained during the DRY process

#### YAGNI - You Aren’t Gonna Need It

A few situations where a programmer should consider following YAGNI are:

+ If you are asked to do validation of email and password fields through a program, there is no need to add coding to validate the name field also. You may never need it.
+ If a programmer is asked to link different databases of cancer patients of a hospital with a health application, the developer should not consider the hospitals which are already closed. They may never open, and the patient database must have already moved to active hospitals.
+ Some programmers may create abstractions even when they are having just one well-defined case in anticipation of the addition of cases. So, they write unnecessary codes and make assumptions about further cases. This should be avoided.
+ Use of If-else logic even if the “else” part is always going to be negative in all the test scenarios encountered.

#### SOLID Principle
1)Single Responsibility Principle (SRP)
2)Open/Closed Principle (OCP)
3) Liskov Substitution Principle (LSP)
4) Interface Segregation Principle (ISP)
5) Dependency Inversion Principle (DIP)
