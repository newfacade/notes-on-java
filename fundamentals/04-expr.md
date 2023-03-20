# Expressions and numbers

```{note}
We will learn arithmetic expressions, the math class and formatting numbers in this section.
```

## Arithmetic expressions

Division need attention:

```java
int result = 10 / 3;
// will print 3, a whole number
System.out.println(result);

double decimalResult =  (double)10 / (double)3;
// print 3.3333333333333335
System.out.println(decimalResult);
```

Increment and decrement:

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

Two ways of increment by 2:

```java
int x = 1;
x = x + 2;
x += 2;
```

Order of operations:

1. ()
2. \* /
3. \+ -

## The math class

```java
// cast float > int or double > long
int round = Math.round(1.1F);
// ceil will cast double > long
int ceil = (int)Math.ceil(1.1);
int floor = (int)Math.floor(1.1);

// overloaded method
int maximum = Math.max(1, 2);
// random number in [0, 1]
double random = Math.random() * 100;
```

## Formatting numbers

Print a number properly.

```java
import java.text.NumberFormat;

public class Main {
    public static void main(String[] args) {
        
        // NumberFormat is an abstract class
        NumberFormat currency = NumberFormat.getCurrencyInstance();
        String result = currency.format(1234567.891);
        
        // method chaining
        String newResult = NumberFormat.getCurrencyInstance().format(1234567.891);

        // other formats
        NumberFormat percent = NumberFormat.getPercentInstance();
    }
}
```
