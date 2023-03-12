# Control flow

```{note}
The statement inside your source file are generally executed from top to bottom. The control flow statements, however, break up the flow of execution by employing decision making, looping and branching, enable your program to conditionally execute particular blocks of code.
```

## Comparison operators

Sample code block:

```java
int x = 1;
int y = 1;
System.out.println(x == y);  // true
System.out.println(x != y);  // false
System.out.println(x <= y);  // true
```

```{caution}
== is a comparison operator, = is the assignment operator.
```

## Logical operators

* and: &&
* or: ||
* not: !

```java
int temperature = 22;
boolean isWarm = temperature > 20 && temperature < 30;
```

## If statements

Sample code:

```java
public class Main {
    
    public static void main(String[] args) {
        int temperature = 32;
        if (temperature > 30) {
            System.out.println("It's a hot day");
        } else if (temperature > 20) {
            System.out.println("Beautiful day");
        } else {
            System.out.println("Cold day");
        }
    }
}
```

Assign boolean variables using statements:

```java
int income = 120_000;
boolean hasHighIncome = (income > 10_000)
```

The ternary operator:

```java
int income = 120_000;
String className = income > 10_000 ? "First" : "Economy";
```

## Switch statements

We use switch statements to execute different parts of code depending on the value of expression.

```java
public class Main {
    
    public static void main(String[] args) {
        String role = "admin";
        switch (role) {
            case "admin":
                System.out.println("You are an admin");
                break;

            case "moderator":
                System.out.println("You are a moderator");
                break;

            default:
                System.out.println("You are a guest");
        }
    }
}
```

```{caution}
Use break at the end of each case, otherwise Java will continue executing the following cases.<br>
Use default at the end the switch statement.
```

## For loops

```java
for (initiation, end_condition, update) {
    body;
}
```

1. initiation
2. see if end_condition satisfied, if satisfied, break; else, run the body.
3. update, go back to step2.

```java
public class Main {
    
    public static void main(String[] args) {
        // 0 with <; 1 with <=
        for (int i = 0; i < 5; i ++) {
            System.out.println("Hello World " + i);
        }
    }
}
```

Decrement is also possible:

```java
for (int i = 5; i > 0; i --)
```


## While loops

While loops can be used when we have no idea how many time we will repeate something. For example, ask the user to continues enter something until they type 'quit'.

```java
import java.util.Scanner;

public class Main {
    
    public static void main(String[] args) {
        // create Scanner object outside the loop
        Scanner scanner = new Scanner(System.in);
        String input = "";
        while (!input.equals("quit")) {
            System.out.print("Input: ");
            input = scanner.next().toLowerCase();
            System.out.println(input);
        }
    }
}
```

```{caution}
String is a reference type, != will compare the address of objets, not their values, use method equals instead.
```

## Do while loops

Do while loops get executed at least once.

```java
import java.util.Scanner;

public class Main {
    
    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);
        String input = "";
        do {
            System.out.print("Input: ");
            input = scanner.next().toLowerCase();
            System.out.println(input);
        } while (!input.equals("quit"));
    }
}
```

## Break and continue

* break: jump out of the loop
* continue: move control to the beginning of the loop

## For each loops

```java
for (Type name: array) {
    body;
}
```

Simpler but restricted.

```java
public class Main {
    
    public static void main(String[] args) {
        String[] fruits = {"Apple", "Mongol", "Orange"};
        for (String fruit:
             fruits) {
            System.out.println(fruit);
        }
    }
}
```
