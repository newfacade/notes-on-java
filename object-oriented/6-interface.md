# Interfaces

```{note}
We use interface to build loosely-coupled, extensible, testable applications.<br>
We should try to keep the coupling or relationship between classes as loosely as possible. Abstract is not enough.
```

An interface is a type similar to a class, but it includes only methods declarations.

```java
public interface Draggleble {
    void drag();
}
```

* Interfaces: what should be down.
* Classes: How it should be down.

## Tightly-coupled code

These two classes are tightly-coupled:

```java
public class TaxCalculator {
    private double taxableIncome;

    public TaxCalculator(double taxableIncome) {
        this.taxableIncome = taxableIncome;
    }

    public double calculateTax() {
        return taxableIncome * 0.3;
    }
}
```

```java
public class TaxReport {
    private TaxCalculator calculator;

    public TaxReport(TaxCalculator calculator) {
        this.calculator = calculator;
    }

    public void show() {
        double tax = calculator.calculateTax();
        System.out.println(tax);
    }
}
```

## Creating an interface

New Java Class > Interface.

```java
public interface TaxCalculator {
    double calculateTax();
}
```

```java
public class TaxCalculator2023 implements TaxCalculator {
    private double taxableIncome;

    public TaxCalculator2023(double taxableIncome) {
        this.taxableIncome = taxableIncome;
    }

    @Override
    public double calculateTax() {
        return taxableIncome * 0.3;
    }
}
```

## Dependency injection

```{tip}
In reality, most of the time, construct injection is enough.
```

### Constructor injection

```java
public class TaxReport {
    private TaxCalculator calculator;

    // working with a interface
    // does not know anything about the concrete implementation
    public TaxReport(TaxCalculator   calculator) {
        this.calculator = calculator;
    }

    public void show() {
        double tax = calculator.calculateTax();
        System.out.println(tax);
    }
}
```

in `Main`:

```java
public class Main {
    public static void main(String[] args) {
        TaxCalculator2023 calculator = new TaxCalculator2023(100_000);
        // inject dependencies
        TaxReport report =  new TaxReport(calculator);
    }
}
```

### Setter injection

Setter injection allows us to change the dependencies of class.

```java
public void setCalculator(TaxCalculator calculator) {
    this.calculator = calculator;
}
```

in `Main`

```java
public class Main {
    public static void main(String[] args) {
        TaxCalculator2023 calculator = new TaxCalculator2023(100_000);
        TaxReport report =  new TaxReport(calculator);
        report.show();

        // change dependencies
        report.setCalculator(new TaxCalculator2022(100_000));
        report.show();
    }
}
```

### Method injection

Injection dependency when we use it.

```java
public class TaxReport {
    public void show(TaxCalculator calculator) {
        double tax = calculator.calculateTax();
        System.out.println(tax);
    }
    ...
    }
```

## Interface segregation principal

```{note}
Divide big interfaces into smaller ones!<br>
Unlike classes, Java interface can have multiple parents.
```

## Interfaces vs Abstract classes

* Interfaces: Only declarations, no implementation.
* Abstract classes: Partially-completed classes, wo that we can share code between a few classes.

Use interfaces when you want to decouple a class from it's dependencies. 

* You can easily swap implementation to another. 
* Program against interfaces: extend your applications with minimal impact.
* Unit test: test your classes in isolation.
