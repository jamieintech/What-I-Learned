# *Java* Basic Refresher

A quick runthrough of basic Java features



- [A brief background of Java](#a-brief-background-of-java)
  * [JVM](#jvm)
- [Java Classes and Objects](#java-classes-and-objects)
  * [Modeling/Abstracting an object](#modeling-abstracting-an-object)
  * [Data Types](#data-types)
  * [Functions](#functions)
  * [Visibility](#visibility)
  * [Moving the model to code](#moving-the-model-to-code)
- [Instances, Constructors, Main Functions and Multiple Classes](#instances--constructors--main-functions-and-multiple-classes)
  * [Instantiation](#instantiation)
  * [Constructor](#constructor)
  * [Main Function](#main-function)
  * [Concatenation](#concatenation)
  * [Instantiate Multiple Classes](#instantiate-multiple-classes)



# A brief background of Java

- Developed at Sun Microsystems, now part of Oracle, in the early 1990s
- Sun needed a language that could run on different hardwares, including boards for devices such as appliances (ex. microwaves, dish washers, TV, etc..)
- Java was developed as an alternative to C and C++ in a way which a single Java application(a set of Java source code) could be compiled and run on any type of hardware
- OOP language



## JVM

- JVM = a computer program that can run Java bytecode = virtual machine
- can run Java source code developed anywhere
- **JVM makes Java a truly hardware and operating environment neutral** (=doesn't matter what hardware/OS you're on to run Java source codes)
  - the byte code is always the same, regardless of hardware
  - JVM on the hardware will execute the Java byte code to run the application
    - same Java code can be run on mobile devices, PC, etc..



# Java Classes and Objects

- Java allows developers to abstract real-world objects
- Objects in a Java application can interact with one another
- Class = abstracted java object = models object behaviors and properties



## Modeling/Abstracting an object

- define/identify the properties or methods and attributes of the object = what features does this object have?
- understand how your class(the object you defined) behave
- start small



## Data Types

- Primitives: int, short, long, float, boolean, void, etc.
- Non-primitives: String, Date, etc.



## Functions

- blocks of code in a class that drive object behavior = how objects behave
- do something: set a value, update a value, etc.
- can accept parameters
- can return a value



## Visibility

- data types and functions have visibility
- defining how the object will interact and share data
- **private**: only available to members of the class
- **public**: available to members of the class and members outside the class



## Moving the model to code

example: **Car** object

| Car                                                          |
| :----------------------------------------------------------- |
| **private String** make<br />**private String** model<br />**private int** year<br /><br />**public String** setMake**(String)**<br />**public String** getMake<br />**public String** setModel**(String)**<br />**public String** getModel |

```java
// Car object to code
public class Car {
	private String make;
	private String model;
	private int year;
	
	public String setCarMake(String make) {
		this.make = make;
		return make;
	}
	public String getCarMake() {
		return make;
	}
	public String setCarModel(String model) {
		this.model = model;
		return model;
	}
	public String getCarModel() {
		return model;
	}
	public static void main(String[] args) {
		System.out.println("Car Java application");
	}
}
```



# Instances, Constructors, Main Functions and Multiple Classes



## Instantiation

- class is like a blueprint => it models an object but does not execute
- it's the object that executes
- **when an objected is declared:**
  - it's assigned a class, a name, and some sections of memory
  - once it's named = **becomes a specific instance of the class**
- an object will have all the class's properties and functions
- however, an object is stand-alone, and each object has a unique name



## Constructor

- a special function in the Java class
- a constructor initializes the Java class when the class is instantiated
  - it takes the data and use it to **instantiate the object at runtime**
- constructor is named the same name as the class
- **a class can have more than one constructor**
  - **but the parameters must be different**
- Java selects the constructor based on how the constructor is called in the main function
- a **constructor is optional** => when there is no constructor, Java will <u>call an implicit constructor at runtime</u>



## Main Function

- where the Java classes are instantiated
- where the objects are executed and interact with each other
- where the business logic is built/executed
  - the source code follows the business logic for which the problem that the application is looking to solve
  - the business logic uses the instantiated objects to satisfy the application's requirements



## Concatenation

- term for **joining or combining**
- in Java, it's more used in the formatting of how data is output
- used to join String data with other data types (see example below)
- in Java, concatenation operator is "**+**"

```java
public String toString() {
	return "Car make: "+make+", model: "+model+", year: "+year;
}
```



## Instantiate Multiple Classes

- in order to instantiate multiple classes, they **must be declared in the main function**
- **only 1 class will have the main function** among the multiple classes

