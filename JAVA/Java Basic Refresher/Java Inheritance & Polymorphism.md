# Java Inheritance & Polymorphism

- [Inheritance](#inheritance)
  * [Some Rules of Inheritance](#some-rules-of-inheritance)
- [Polymorphism](#polymorphism)
  * [Overloading Functions](#overloading-functions)

## Inheritance

- **Inheritance** is an important part of Object Oriented Programming
- it supports an ability to **reuse existing features and functionality**
- provides **flexibility**
- if there is a class that already has some of the desired functionality, there is no need to rewrite the same functionality in a new class => just inherit the class that already has the functionality
- in Java, inheritance is implemented using the `extends` keyword
  - defined in the class header
  - multiple inheritance is supported



### Some Rules of Inheritance

- **subclass**: a class that is derived from another class (=extended class / child class)
- **superclass**: the class from which the subclass is derived (=base class / parent class)
- every class has **one and only direct superclass** (single inheritance)
  - except for Object. <u>Object has no superclass</u>
- if there is no explicit superclass, **every class is implicitly a subclass of Object**
- a subclass inherits all the members(fields, methods, nested classes) from its superclass
  - a subclass can override methods that it inherits
- you can prevent a class from being subclassed by using the `final` keyword (same for a method)
- an abstract class can only be subclassed



## Polymorphism

- **Polymorphism** allows for a class to inherit from another class AND at the same time <u>have its own unique properties and methods</u>



### Overloading Functions

- a class can have more than one function **with the same name**, provided that the **parameters are different**
- at runtime, Java runs the called function whose parameters match