# Java tutorial for beginners

## Installation

1. download and install Java JDK
2. download and install code editor, e.g. IntelliJ
3. create new IntelliJ projects, remember to select JDK

## Hello World

Basic structure of Java functions (or methods):

```java
ReturnType name(...) {
    ...
}
```

we must have a `main` method which is the entry point of our program. Every method must be contained in a Class (`main` in `Main`).

```java
public class Main {

    public static void main() {
        ...
    }
}
```

This is the basic structure of our program.

* public: accessible from other parts of the program
* static: main function must be static

Hello World program (in our project, the `Main.java` file):

```java
public class Main {
    public static void main(String[] args) {
        System.out.println("Hello world!");
    }
}
```

Click the Run buttom in IntelliJ, our first java program will be executed.

## How java code gets executed

basically two steps:

* Compilation: use Java compiler(in JDK) to compile *.java to byte code
* Execution: JVM(in JRE, which in JDK) translate byte code(platform independent) to native code(windows, mac, ...)

Compilation and execution using command line:

```
$ javac Main.java
$ ls
Main.class      Main.java
$ java Main
Hello world!
```

## Types

* Primitive types: for storing simple values
* Reference types: for storing complex objects

### Primitive types

| Type    | Bytes | Range       |
|---------|-------|-------------|
| byte    | 1     | [-128, 127] |
| short   | 2     | [-32k, 32k] |
| int     | 4     | [-2B, 2B]   |
| long    | 8     |             |
| float   | 4     |             |
| double  | 8     |             |
| char    | 2     | A,B,...     |
| boolean | 1     | true/false  |

```java
public class Main {
    public static void main(String[] args) {
        byte age = 30;
        short numCountries = 200;
        int income = 12_000;
        // L for long
        long viewsCount = 3_123_456_789L;

        // F for float
        float price = 10.99F;
        double previousPrice = 10.99;

        // single quotation mark
        char letter = 'A';
        
        boolean isEligible = false;
    }
}
```

### Reference types

All the other types except the 8 primitive types.

```java
import java.util.Date;

public class Main {
    public static void main(String[] args) {
        byte age = 30;
        // reference type need allocate memory
        Date now = new Date();
        System.out.println(now);
    }
}
```

### Primitive types vs Reference types

```java
import java.awt.*;

public class Main {
    public static void main(String[] args) {
        // x and y: different address in memory
        byte x = 1;
        byte y = x;
        x = 2;
        System.out.println(y);  // print 1

        // point1 and point2: reference the same address in memory
        Point point1 = new Point(1, 1);
        Point point2 = point1;
        point1.x = 2;
        System.out.println(point2);  // print java.awt.Point[x=2,y=1]
    }
}

```

### Strings

initialize:

```java
String message = new String("Hello World");
// we can initialize String variable like Primitive types.
String newMessage = "Hello World";
```

usefull methods:

```java
String message = "Hello World" + "!!";
System.out.println(message.endsWith("!!"));  // return true
System.out.println(message.length());
// first index appears, if does not exists, return -1
System.out.println(message.indexOf("W"));
// "!" and "*" are arguments. target and replacement are parameters
System.out.println(message.replace("!", "*"));
System.out.println(message.toLowerCase());
System.out.println(message.trim());  // strip
// strings are immutable, methods that modifies a string will return a new string object
System.out.println(message);
// four useful escape sequences
String newMessage = "c:\\Windows...Hello \"World\n\t";
```

### Arrays

```java
import java.util.Arrays;

public class Main {
    public static void main(String[] args) {
        // arrays are reference types, need specify the size of the array
        int[] numbers = new int[5];
        numbers[0] = 1;
        numbers[1] = 2;
        // print a wired string based on the address of the array
        System.out.println(numbers);
        // print numbers
        System.out.println(Arrays.toString(numbers));
    }
}
```

simpler way to initialize:

```java
int[] numbers = {2, 3, 5, 1, 4};
```

sort array:

```java

int[] numbers = {2, 3, 5, 1, 4};
Arrays.sort(numbers);
System.out.println(Arrays.toString(numbers));
```

### Multi-dimensional arrays

```java
int[][] numbers = new int[2][3];  // 2 rows, 3 columns
numbers[0][0] = 1;
// multi-dimensional array: use deepToString
// [[1, 0, 0], [0, 0, 0]]
System.out.println(Arrays.deepToString(numbers));
// simpler way to initialize
int[][] newNumbers = {{1, 2, 3}, {4, 5, 6}};
```

### Constants

```java
// use upper case
final float PI = 3.14F;
```

### Casting

implicit casting:

```java
// byte > short > int > long > float > double
short x = 1;
int y = x + 2;
System.out.println(y);
```

explicit casting:

```java
double x = 1;
int y = (int)x + 2;
System.out.println(y);
```

When explicit casting, types need to be compatible. We cannot cast `String` to `int`, even if that `String` equals "1". The right way to do this:

```java
String x = "1";
// int y = (int)x + 2 will raise a Exception.
// similarly, we have Short.parseShort(), Float.parseFloat(), etc.
int y = Integer.parseInt(x) + 2;
System.out.println(y);
```

## Expressions and numbers

### Arithmetic expressions

division need attention.

```java
int result = 10 / 3;
// print 3, a whole number
System.out.println(result);

double decimalResult =  (double)10 / (double)3;
// print 3.3333333333333335
System.out.println(decimalResult);
```

increment and decrement:

```java
int x = 1;
int y = x++;  // increment after assignment
System.out.println(x);  // 2
System.out.println(y);  // 1
```

```java
int x = 1;
int y = ++x;  // increment before assignment
System.out.println(x);  // 2
System.out.println(y);  // 2
```

two ways of increment by 2:

```java
int x = 1;
x = x + 2;
x += 2;
```

order of operation:

1. ()
2. \* /
3. \+ -

### The math class

```java
int round = Math.round(1.1F);  // float > int or double > long.
int ceil = (int)Math.ceil(1.1);  // ceil: double > long
int floor = (int)Math.floor(1.1);
int maximum = Math.max(1, 2);  // overloaded
double random = Math.random() * 100;
```

### Formatting numbers

```java
import java.text.NumberFormat;

public class Main {
    public static void main(String[] args) {
        // NumberFormat is an abstract class, can't use new directly
        NumberFormat currency = NumberFormat.getCurrencyInstance();
        String result = currency.format(1234567.891);
        System.out.println(result);
        
        // method chaining
        String newResult = NumberFormat.getCurrencyInstance().format(1234567.891);

        // other formats
        NumberFormat percent = NumberFormat.getPercentInstance();
    }
}
```

## Reading input

```java
import java.util.Scanner;

public class Main {
    public static void main(String[] args) {
        // read from the terminal window
        Scanner scanner = new Scanner(System.in);
        System.out.print("Age: ");  // use print not println, to avoid new line
        // get the next byte
        byte age = scanner.nextByte();
        System.out.println("You are " + age);

        // type Mosh, get You are Mosh
        // type Mosh Hamedani, also get You are Mosh
        System.out.print("Name: ");
        String name = scanner.next();  // get first word
        System.out.println("You are " + name);

        // type Mosh Hamedani, get You are Mosh Hamedani
        System.out.print("Name: ");
        String line = scanner.nextLine().trim();
        System.out.println("You are " + name);
    }
}
```

## Project: Mortgage Calculator

```java
import java.text.NumberFormat;
import java.util.Scanner;

public class Main {
    public static void main(String[] args) {
        final byte MONTHS_IN_YEAR = 12;
        final byte PERCENT = 100;

        Scanner scanner = new Scanner(System.in);
        System.out.print("Principal: ");
        int principal = scanner.nextInt();
        System.out.print("Annual Interest Rate: ");
        float annualInterestRate = scanner.nextFloat();
        System.out.print("Period (Years): ");
        byte years = scanner.nextByte();

        float monthlyInterestRate = (annualInterestRate / PERCENT) / MONTHS_IN_YEAR;
        int months = years * MONTHS_IN_YEAR;
        // P * (r * (1+ r)^{n}) / ((1+ r)^{n} - 1)
        double mortgage = principal * (monthlyInterestRate * Math.pow(1 + monthlyInterestRate, months) /
                (Math.pow(1 + monthlyInterestRate, months) - 1));
        System.out.println("Mortgage: " + NumberFormat.getCurrencyInstance().format(mortgage).trim());

    }
}
```


## Control flow

### Comparison operators

```java
int x = 1;
int y = 1;
System.out.println(x == y);  // true
System.out.println(x != y);  // false
System.out.println(x <= y);  // true
```

### Logical operators

```java
int temperature = 22;
// and: &&
// or: ||
// not: !
boolean isWarm = temperature > 20 && temperature < 30;
System.out.println(isWarm);
```

### If statements

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

simplify if statements:

```java
int income = 120_000;
boolean hasHighIncome = (income > 10_000)
```

The ternary operator:

```java
int income = 120_000;
String className = income > 10_000 ? "First" : "Economy";
```

### Switch statements

We use switch statements to execute different parts of code depending on the value of expression.

```java
public class Main {
    public static void main(String[] args) {
        String role = "admin";
        switch (role) {
            case "admin":
                System.out.println("You are an admin");
                break;  // if not break, java will continue executing in switch

            case "moderator":
                System.out.println("You are a moderator");
                break;

            default:
                System.out.println("You are a guest");
        }
    }
}
```

### For loops

for (initiation, end_condition, update)

1. initiation
2. see if end_condition satisfied. if satisfied, break; else, run the body.
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

decrement is also possible.

```java
for (int i = 5; i > 0; i --)
```


### While loops

```java
public class Main {
    public static void main(String[] args) {
        int i = 0;
        while (i < 5) {
            System.out.println("Hello World " + i);
            i++;
        }
    }
}
```

while loops can be used when we many times we will repeate something. e.g. ask the user to continues enter something until they type 'quit'.

```java
import java.util.Scanner;

public class Main {
    public static void main(String[] args) {
        // create Scanner object outside the loop
        Scanner scanner = new Scanner(System.in);
        String input = "";
        // string is a reference type, != will compare the address of objets, not their value.
        while (!input.equals("quit")) {
            System.out.print("Input: ");
            input = scanner.next().toLowerCase();
            System.out.println(input);
        }
    }
}
```

### Do while loops

```java
import java.util.Scanner;

public class Main {
    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);
        String input = "";
        // do while loops get executed at least once.
        do {
            System.out.print("Input: ");
            input = scanner.next().toLowerCase();
            System.out.println(input);
        } while (!input.equals("quit"));
    }
}
```

### Break and continue

```java
import java.util.Scanner;

public class Main {
    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);
        String input = "";
        while (true) {
            System.out.print("Input: ");
            input = scanner.next().toLowerCase();
            // move control to the beginning of the loop
            if (input.equals("pass"))
                continue;
            // do not print quit
            if (input.equals("quit"))
                break;
            System.out.println(input);
        }
    }
}
```

### For each loops

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

## Revisite Project: Mortgage Calculator

with error handling.

```java
import java.text.NumberFormat;
import java.util.Scanner;

public class Main {
    public static void main(String[] args) {
        final byte MONTHS_IN_YEAR = 12;
        final byte PERCENT = 100;

        Scanner scanner = new Scanner(System.in);

        int principal = 0;
        while (true) {
            System.out.print("Principal ($1K - $1M): ");
            principal = scanner.nextInt();
            if (principal >= 1000 && principal <= 1_000_000) {
                break;
            }
            System.out.println("Enter a number between 1,000 and 1,000,000.");
        }

        float annualInterestRate = 0.0F;
        while (true) {
            System.out.print("Annual Interest Rate: ");
            annualInterestRate = scanner.nextFloat();
            if (annualInterestRate > 0.0 && annualInterestRate <= 30.0) {
                break;
            }
            System.out.println("Enter a number greater than 0 and less than or equal to 30.");
        }

        byte years = 0;
        while (true) {
            System.out.print("Period (Years): ");
            years = scanner.nextByte();
            if (years >= 1 && years <= 30) {
                break;
            }
            System.out.println("Enter a value between 1 and 30.");
        }

        float monthlyInterestRate = (annualInterestRate / PERCENT) / MONTHS_IN_YEAR;
        int months = years * MONTHS_IN_YEAR;
        // P * (r * (1+ r)^{n}) / ((1+ r)^{n} - 1)
        double mortgage = principal * (monthlyInterestRate * Math.pow(1 + monthlyInterestRate, months) /
                (Math.pow(1 + monthlyInterestRate, months) - 1));
        System.out.println("Mortgage: " + NumberFormat.getCurrencyInstance().format(mortgage).trim());

    }
}
```
