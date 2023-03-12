# Project: Mortgage Calculator

Input principal $P$, annual interest rate $R$, years $Y$. Calculate monthly mortgage:

$$
P\frac{r(1+ r)^{n}}{(1+ r)^{n} - 1}
$$

where $r=\frac{R}{12}$ is the monthly interest rate, $n=12Y$ is the total months.

Solution:

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
        
        double mortgage = principal * (monthlyInterestRate * Math.pow(1 + monthlyInterestRate, months) /
                (Math.pow(1 + monthlyInterestRate, months) - 1));
        System.out.println("Mortgage: " + NumberFormat.getCurrencyInstance().format(mortgage).trim());
    }
}
```
