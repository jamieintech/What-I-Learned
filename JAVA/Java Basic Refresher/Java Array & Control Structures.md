# Java Array & Control Structures

* [Arrays](#arrays)
- [Control Structures](#control-structures)
  * [if & else & else if](#if---else---else-if)
  * [for Loop](#for-loop)
  * [while Loop](#while-loop)
  * [do while Loop](#do-while-loop)
  * [switch case](#switch-case)
- [Error Handling](#error-handling)

## Arrays

- data structures where one variable type contains multiple values
- can be fixed size, and ArrayLists are dynamic in size
- values are added or removed from the ArrayList using member methods `add` and`get`

```java
public int[] myNum = {10, 20, 30, 40};
private String[] pizza = {"Cheese", "Pepperoni", "Onions"};
ArrayList<String> miniPizza = new ArrayList<String>();
```





## Control Structures

- `if, else, while, do, for, break, continue, return` have typical funcionality
- a statement is evaluated for true/fase => control structure takes place after the evaluation
  - `return` statement ends the function and returns control to where the function was called
  - `break` just breaks the loop and returns to the caller method
  - `continue` statement ends program execution of the current loop iteration but does not stop execution of the loop



### if & else & else if

- way of testing for a condition
- when the condition evaluates to be true, the `if` block is executed
  - when false, the `else` block will execute (if there is one)
- **else if**
  - a way of testing for multiple conditions using multiple code blocks



### for Loop

- header consists of the initialization, condition and the iterator
- expression in the loop will execute as long as the header condition is true

```java
int iLength = pizza.length;
String myPizzas = "";

for(int i=0; i<iLength; i++){	//the code inside will run based on the condition here
    myOut1 = pizza[i];
    myPizzas = myPizzas + " " + myOut1;
}
```



### while Loop

- header with a condition
- the expressions in the while loop will execute as long as the condition in the header is true

```java
while(itr.hasNext()){	//this part should be true to run
    myList = itr.next();
    fullList += myList + " ";
    iCount ++;
}
```



### do while Loop

- similar to while loops except the condition is evaluated at the end of the loop
- the loop expression will be executed at least once, even if the condition is false

```java
int i = 5;
do {
    System.out.println(i);	//this will execute first
    i--;
}while(i>1);	//the condition is at the end of the loop

/*
* 5
* 4
* 3
* 2
* 1
*/
```



### switch case

- simplified version of if-else
- value is completed to another value or constant
- case equal to the value is returned and evaluation ends
- default value is returned when there is no match

```java
int n = 2;
switch(n+2){
    case 1:
        System.out.println("case 1 : "+n);
    case 2:
        System.out.println("case 2 : "+n);
    default:
        System.out.println("default : "+n);
}

// default : 2
```



## Error Handling

- Java supports error handling
- errors can be captured and handled => this allows the application to return friendly errors to the user
- in Java errors are handled using a `try/catch` block
- if there is a potential of error, the line enters the `try` block
- if the error occurs, the error is handled in the `catch` block

```java
try {
    baseDt = new SimpleDateFormat("yyyyMMdd").parse("202011");
} catch (ParseException e) {
    e.printStackTrace(); 
    System.out.println("Incorrect date format")
}
// java.text.ParseException: ~~~~
// Incorrect date format
```

