# Revisite Project: Mortgage Calculator

```{note}
With basic error handling using control flow.
```

Solution:

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
            if (annualInterestRate >= 1.0 && annualInterestRate <= 30.0) {
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
        double mortgage = principal * (monthlyInterestRate * Math.pow(1 + monthlyInterestRate, months) /
                (Math.pow(1 + monthlyInterestRate, months) - 1));
        System.out.println("Mortgage: " + NumberFormat.getCurrencyInstance().format(mortgage).trim());

    }
}
```
