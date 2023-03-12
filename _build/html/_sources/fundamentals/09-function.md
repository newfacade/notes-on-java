# Functions

```{note}
Any fool can write code that computers can understand.<br>
Good programmers write code that humans can understand.
```

Functions are code blocks with parameters, Sample code of function:

```java
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

## Refactoring Mortgage Calculator using functions

Refactoring means changing the structure of the code without changing its bahavior. Whenever you want to refactor your method, you should look for two things:

1. The concepts or lines of code that always go together.
2. Look for repetitive patterns in your code.

We encapsulate the repetitive read number pattern to function `readNumber` and the meaningful concepts of calculate mortgage to fucntion `calculateMortgage`.

```java
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

    public static double calculateMortgage(
            int principal, float annualInterest, byte years) {
        final byte MONTHS_IN_YEAR = 12;
        final byte PERCENT = 100;

        float monthlyInterestRate = (annualInterest / PERCENT) / MONTHS_IN_YEAR;
        short numberOfPayments = (short)(years * MONTHS_IN_YEAR);
        return principal * (monthlyInterestRate * Math.pow(1 + monthlyInterestRate, numberOfPayments) /
                (Math.pow(1 + monthlyInterestRate, numberOfPayments) - 1));
    }
}
```


