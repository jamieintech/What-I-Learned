# Errors (compile & run time)

- [Compile-time errors](#compile-time-errors)
- [Run-time errors](#run-time-errors)

## Compile-time errors

Compile-time errors are errors that prevent a java program to compile:

- syntax error: incorrect keyword, a forgotten symbol `;` at the end of a statement;
- a bad source code file name;
- invoking a non-existing method;
- and etc.

```java
package errors;

public class compileError {
	public static void main(String[] args) {
		int x = 20, y = 30;	
		int sum = x+y;
		
		System.out.println(Sum);	//non existing variable
	}
}
```

```bash
Exception in thread "main" java.lang.Error: Unresolved compilation problem: 
	Sum cannot be resolved to a variable

	at errors.ex01.main(ex01.java:10)
```

Most compile-time errors can be easily prevented when using a modern IDE since it detects any compile-time errors beforehand.



## Run-time errors

Run-time errors (a.k.a "bugs") are errors that occur when the program is running. 

It is the JVM that is responsible to detect run-time errors while the program is running. A program that contains run-time errors may produce wrong results or may even stop during execution. 

There are two subtypes of run-time errors:

- logic error
- unhandled execeptional events (ex. division by zero)

**Example 1: division by zero**

```java
package errors;

public class RuntimeError {
	public static void main(String[] args) {
		int a = 20, b = 0;
		System.out.println(a/b);	//Division by zero
	}
}
```

```bash
Exception in thread "main" java.lang.ArithmeticException: / by zero
	at errors.RuntimeError.main(RuntimeError.java:6)
```

**Example 2: Array index out of bounds**

```java
package errors;

public class RuntimeError {
	public static void main(String[] args) {	
		int[] arr = {1, 2, 3, 4};
		System.out.println(arr[5]);	//Array index out of bounds
	}
}
```

```bash
Exception in thread "main" java.lang.ArrayIndexOutOfBoundsException: Index 5 out of bounds for length 4
	at errors.RuntimeError.main(RuntimeError.java:9)
```

