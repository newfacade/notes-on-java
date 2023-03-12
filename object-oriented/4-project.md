# OOP Project: Mortgage Calculator

```{note}
Use OOP principals to refactoring the Mortgage Calculator.
```

Base on the principals of Encapsulation and Abstraction, we decided to construct 3 classes:

1. Console: implement `readNumber`
2. MortgageReport: all about presentation
3. MortgageCalculator: all about calculation

## The Console

```java
package com.codewithmosh;

import java.util.Scanner;

public class Console {
    private static final Scanner scanner = new Scanner(System.in);

    public static double readNumber(String prompt, double min, double max) {
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

```{tip}
IntelliJ Safe refactor: Refactor > Refactor this > Move to another class.
```

## The MortgageCalculator

Here, additionally, we calculate the balance remained after each month:

$$
P\frac{(1+r)^{n} - (1+r)^{k}}{(1+r)^{n} -1}
$$

where $P$ is the principal, $r$ is the monthly interest rate, $n$ is the total months, $k$ is the months we already payed.

```java
package com.codewithmosh;

public class MortgageCalculator {
    private final byte MONTHS_IN_YEAR = 12;
    private final byte PERCENT = 100;

    private int principal;
    private float annualInterestRate;
    private byte years;

    // constructor
    public MortgageCalculator(int principal, float annualInterestRate, byte years) {
        this.principal = principal;
        this.annualInterestRate = annualInterestRate;
        this.years = years;
    }

    public double calculateMortgage() {
        float monthlyInterestRate = getMonthlyInterestRate();
        int numberOfPayments = getNumberOfPayments();
        return principal * (monthlyInterestRate * Math.pow(1 + monthlyInterestRate, numberOfPayments) /
                (Math.pow(1 + monthlyInterestRate, numberOfPayments) - 1));
    }
    
    // return one balance
    private double calculateBalance(int paymentsMade) {
        float monthlyInterestRate = getMonthlyInterestRate();
        int numberOfPayments = getNumberOfPayments();
        return principal *
                (Math.pow(1 + monthlyInterestRate, numberOfPayments) - Math.pow(1 + monthlyInterestRate, paymentsMade))
                / (Math.pow(1 + monthlyInterestRate, numberOfPayments) - 1);
    }

    // return balances
    public double[] getRemainingBalances() {
        double[] balances = new double[getNumberOfPayments()];
        for (short month = 0; month < balances.length; month++) {
            balances[month] = calculateBalance(month);
        }
        return balances;
    }

    private float getMonthlyInterestRate() {
        return annualInterestRate / PERCENT / MONTHS_IN_YEAR;
    }

    private int getNumberOfPayments() {
        return years * MONTHS_IN_YEAR;
    }
}
```

```{tip}
Use Generate -> Constructor in IntelliJ to easily create a constructor.
```

## The MortgageReport

Initialize a MortgageReport using a MortgageCalculator.

```java
package com.codewithmosh;

import java.text.NumberFormat;

public class MortgageReport {
    private MortgageCalculator calculator;
    private final NumberFormat currency;
    
    // constructor
    public MortgageReport(MortgageCalculator calculator) {
        this.calculator = calculator;
        currency = NumberFormat.getCurrencyInstance();
    }

    public void printMortgage() {
        double mortgage = calculator.calculateMortgage();
        System.out.println();
        System.out.println("MORTGAGE");
        System.out.println("--------");
        System.out.println("Mortgage: " + currency.format(mortgage));
    }

    public void printPaymentSchedule() {
        System.out.println();
        System.out.println("PAYMENT SCHEDULE");
        System.out.println("----------------");
        for (double balance :
                calculator.getRemainingBalances()) {
            System.out.println(currency.format(balance));
        }
    }
}
```

## The Main Class

```java
package com.codewithmosh;

public class Main {
    
    public static void main(String[] args) {
        // return double and explicit casting
        int principal = (int)Console.readNumber("Principal: ", 1000, 1_000_000);
        float annualInterestRate = (float)Console.readNumber("annualInterestRate: ", 1, 30);
        byte years = (byte)Console.readNumber("Years: ", 1, 30);

        MortgageCalculator calculator = new MortgageCalculator(principal, annualInterestRate, years);

        MortgageReport report = new MortgageReport(calculator);
        report.printMortgage();
        report.printPaymentSchedule();
    }
}
```

Beatiful!
