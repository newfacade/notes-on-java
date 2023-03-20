# Java Hello World

```{note}
Print "Hello World" using Java.
```

## Installation

1. Download and install IntelliJ IDEA (one Java IDE).
2. Use IntelliJ to create a new command line Java project, remember to select and download JDK (Java Development Kit, this tutorial have been written for JDK 8).

## Classes and Methods

Once the new project is created, IntelliJ will automatically create a file named Main.java:

```{code-block} java
public class Main {

    public static void main(String[] args) {
	// write your code here
    }
}
```

Here `Main` is a class and `main` is a method (function). In Java:

* A method must be contained in a class
* Class YourClassName should be contained in a file named YourClassName.java
* `main` method is the entry point of our program

Next briefly explain keywords `public` and `static`:

* public: accessible from other parts of the program
* static: `main` method must be static

### Basic structure of classes

```{code-block} java
Keywords class ClassName {
    ...
}
```

### Basic structure of methods

```{code-block} java
Keywords ReturnType functionName(Parameters) {
    ...
}
```

## Hello World

Use `System.out.println` to print a String:

```{code-block} java
public class Main {
    
    public static void main(String[] args) {
        System.out.println("Hello world");
    }
}
```

Click the Run buttom in IntelliJ, our first Java program will be executed.
