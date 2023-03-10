# Clean coding

Any fool can write code that computers can understand.<br>
Good programmers write code that humans can understand.

## Functions

```java
package com.codewithmosh;

public class Main {
    public static void main(String[] args) {
        greetUser("Mosh", "Hamadani");
        greetUser("New", "Facade");
    }
    
    public static void greetUser(String firstName, String lastName) {
        System.out.println("Hello " + firstName + " " + lastName);
    }
}
```

## Refactoring

Refactoring means changing the structure of the code without changing its bahavior.

Whenever you want to refactor your method, you should look for two things:

1. The concepts or lines of code that always go together.
2. Look for repetitive patterns in your code.

```java
package com.codewithmosh;

import java.text.NumberFormat;
import java.util.Scanner;

public class Main {
    public static void main(String[] args) {
        int principal = (int)readNumber("Principal", 1000, 1_000_000);
        float annualInterestRate = (float)readNumber("Annual Interest Rate: ", 1, 30);
        byte years = (byte)readNumber("Period (Years): ", 1, 30);

        double mortgage = calculateMortgage(principal, annualInterestRate, years);
        System.out.println("Mortgage: " + NumberFormat.getCurrencyInstance().format(mortgage).trim());

    }

    public static double calculateMortgage(
            int principal, float annualInterest, byte years) {
        final byte MONTHS_IN_YEAR = 12;
        final byte PERCENT = 100;

        float monthlyInterestRate = (annualInterest / PERCENT) / MONTHS_IN_YEAR;
        short numberOfPayments = (short)(years * MONTHS_IN_YEAR);
        // P * (r * (1+ r)^{n}) / ((1+ r)^{n} - 1)
        return principal * (monthlyInterestRate * Math.pow(1 + monthlyInterestRate, numberOfPayments) /
                (Math.pow(1 + monthlyInterestRate, numberOfPayments) - 1));
    }

    public static double readNumber(String prompt, double min, double max) {
        Scanner scanner = new Scanner(System.in);
        double value;
        while (true) {
            System.out.print(prompt);
            value = scanner.nextDouble();
            if (value >= min && value <= max) {
                break;
            }
            System.out.println("Enter a value between " + min + " and " + max);
        }
        return value;
    }
}
```

## Project: payment schedular

```java
package com.codewithmosh;

import java.text.NumberFormat;
import java.util.Scanner;

public class Main {
    final static byte MONTHS_IN_YEAR = 12;
    final static byte PERCENT = 100;

    public static void main(String[] args) {

        int principal = (int)readNumber("Principal: ", 1000, 1_000_000);
        float annualInterestRate = (float)readNumber("Annual Interest Rate: ", 1, 30);
        byte years = (byte)readNumber("Period (Years): ", 1, 30);
        float monthlyInterestRate = (annualInterestRate / PERCENT) / MONTHS_IN_YEAR;
        short numberOfPayments = (short)(years * MONTHS_IN_YEAR);

        printMortgage(principal, monthlyInterestRate, numberOfPayments);
        printPaymentSchedule(principal, monthlyInterestRate, numberOfPayments);
    }

    private static void printPaymentSchedule(int principal, float monthlyInterestRate, short numberOfPayments) {
        System.out.println("\nPAYMENT SCHEDULE");
        System.out.println("----------------");
        for (short month = 1; month <= numberOfPayments; month++) {
            double balance = calculateBalance(
                    principal, monthlyInterestRate, numberOfPayments, month);
            System.out.println(NumberFormat.getCurrencyInstance().format(balance).trim());
        }
    }

    private static void printMortgage(int principal, float monthlyInterestRate, short numberOfPayments) {
        System.out.println("\nMORTGAGE");
        System.out.println("--------");
        double mortgage = calculateMortgage(principal, monthlyInterestRate, numberOfPayments);
        System.out.println("Mortgage: " + NumberFormat.getCurrencyInstance().format(mortgage).trim());
    }

    public static double calculateMortgage(
            int principal, float monthlyInterestRate, short numberOfPayments) {
        return principal * (monthlyInterestRate * Math.pow(1 + monthlyInterestRate, numberOfPayments) /
                (Math.pow(1 + monthlyInterestRate, numberOfPayments) - 1));
    }

    public static double calculateBalance
            (int principal, float monthlyInterestRate, short numberOfPayments, short paymentsMade) {
        return principal *
                (Math.pow(1 + monthlyInterestRate, numberOfPayments) - Math.pow(1 + monthlyInterestRate, paymentsMade))
                / (Math.pow(1 + monthlyInterestRate, numberOfPayments) - 1);
    }

    public static double readNumber(String prompt, double min, double max) {
        Scanner scanner = new Scanner(System.in);
        double value;
        while (true) {
            System.out.print(prompt);
            value = scanner.nextDouble();
            if (value >= min && value <= max) {
                break;
            }
            System.out.println("Enter a value between " + min + " and " + max);
        }
        return value;
    }
}
```

## Dubugging

two types of errors:

* compile-time errors: or syntax error, errors that prevent us from compiling the application (we don't follow the grammer or syntax of java language).
* run-time errors: to find them, we need to use a tool called debugger. Execute the code line by line, look at the value of various variables.

### Common syntax error

* forget to specify the data type
* forget to add `;` at the end the statement. we don't need to terminate code blocks with a `;`.
* when call method, forget to add `()`.
* `""` for string, `''` for char.
* java is case-sensitive.
* `=` and `==`.

### Dubugging

1. set break point
2. run -> debug, not execute the break point line.
3. step over(F8), we can also rerun the program, step into(F7), step out.

we have the variable window, which automatically detect variables that are currently in their scope and shows their value.

we can also add watch `+`.

Resume program, run to the next break point.

down to terminate.

## Packaging java applications

package your application into jar file.

File -> Project structure -> Artifacts -> + JAR, from modules with dependencies.

Module is another level of abstraction above packages, select our Main class, click OK. So now we have an artifacts for building this project as a jar file. click OK.

Build -> Build Artifacts -> Build.

now in `out/artifacts/HelloWorld_jar/HelloWorld.jar`, open it in terminal.

```java
$ ls
HelloWorld.jar
$ java -jar HelloWorld.jar
Hello World
```

We could give this jar file to anyone who has the jre.

