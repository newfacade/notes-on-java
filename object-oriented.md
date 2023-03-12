# Object-oriented programming

## Programming paradigms

Ways or styles of writing code.

* Procedual:
* Functional:
* Object-oriented:
* Event-driven:
* ...

Many language, e.g. Python, Ruby, Java, JavaScript support multiple paradigms.

## Object-oriented programming

Objects contains some data(state) and methods(behaviour).

* Encapsulation(封装): Bundle the data and methods that operate on the data in a single unit.

* Abstraction:

* Inheritance:

* Polymorphism(多态):

* Interfaces:

## Classes

* Class: A blueprint(template) for creating objects

* Object: An instance of a class

## Java Classes

In java, we should add each class to a separate file.

### Creating Classes

```java
package com.codewithmosh;

// public: this class if visible to all other classes in this project
public class TextBox {
    // Field, technically, we should not declare fields as public
    public String text;
    
    public void setText(String text) {
        // text = text may be confusion
        // this is a reference to the current object
        this.text = text;
    }

    public void clear() {
        text = "";
    }
}
```

### Creating objects

```java
package com.codewithmosh;

public class Main {
    public static void main(String[] args) {
        TextBox textBox1 = new TextBox();
        // if omitted, print null, dangerous
        // to avoid that, init public String text = "" in TextBox;
        textBox1.setText("Box 1");
        System.out.println(textBox1.text);
    }
}
```

## Memory allocation

What happens under the hood when we create new objects in java.

java manages two different areas of the memory:

* heap: stores objects.

* stack: stores short lived variables like all the primitives, as well as variables that stored references to objects on the heap.

In java, we don't need to worry about deallocation, java will take care of that.

When we exit a method, java runtime will immediately remove all the variables in the stack. If there is no reference to one object in the heap and unused for a certain period of time, the backgroup process will automatically remove that object in the heap, this is called garbage collection.


## Procedural programming

paradigm before object-orientation.

## Getters and setters

```java
private int baseSalary;
// setter
public void setBaseSalary(int baseSalary) {
    if (baseSalary <= 0)
        throw new IllegalArgumentException("Salary cannot be 0 or less.");
    this.baseSalary = baseSalary;
}
// getter
public int getBaseSalary() {
    return baseSalary;
}
```
 
## Abstraction
 
Reduce complexity by hiding unnecessary details.
 
## Coupling
 
Coupling is about how much a class is dependent upon or coupled to another class.

We want to reduce the coupling between classes.
 
## Constructors

Constructor of Employee

```java
public class Employee {
    private int baseSalary;
    private int hourlyRate;
    // constructor, no ReturnType even void, same name as class
    public Employee(int baseSalary, int hourlyRate) {
        setBaseSalary(baseSalary);
        setHourlyRate(hourlyRate);
    }
    ...
    }
```

use Constructor in Main

```java
package com.codewithmosh;

public class Main {

    public static void main(String[] args) {
        Employee employee = new Employee(50_000, 20);
        int wage = employee.calculateWage(10);
        System.out.println(wage);
    }
}
```

beatiful!

## Method overloading

Creating different implementations of it with different parameters.

```java
public int calculateWage(int extraHours) {
    return baseSalary + (extraHours * hourlyRate);
}

public int calculateWage() {
    return calculateWage(0);
}
```

remember overloading a method too many times will make your application hard to maintain.

## Constructor overloading

```java
public Employee(int baseSalary, int hourlyRate) {
    setBaseSalary(baseSalary);
    setHourlyRate(hourlyRate);
}
public Employee(int baseSalary) {
    // call the first constructor
    this(baseSalary, 0);
}
```

## Static members

A class can have two types of members.

* instance members: belong to instances or objects. we can access through the `.` operator(e.g. `employee.calculateWage()`)

* static members: or class members. belong to a class, not objects(e.g. `Employee.xx`). When we want to present a concept that should be in a single place, the value is independent of objects, we want to share it between all objects. Static methods can only see the other static methods in this class.

Emloyee:

```java
package com.codewithmosh;

public class Employee {
    private int baseSalary;
    private int hourlyRate;
    // static field
    public static int numberOfEmployees;
    // static method
    public static void printNumberOfEmployees() {
        System.out.println(numberOfEmployees);
    }

    public Employee(int baseSalary, int hourlyRate) {
        setBaseSalary(baseSalary);
        setHourlyRate(hourlyRate);
        numberOfEmployees++;
    }
    ...
    }
```

Main:

```java
package com.codewithmosh;

public class Main {

    public static void main(String[] args) {
        Employee employee = new Employee(50_000, 20);
        System.out.println(Employee.numberOfEmployees); // use static field
        Employee.printNumberOfEmployees();  // use static methods
        int wage = employee.calculateWage(10);
        System.out.println(wage);
    }
}
```

main method be static: This is enable the java runtime to directly call the method without having to create a new object.
 
 
## Project

Classes:

1. Console: `readNumber`.
2. MortgageReport: all about presentation.
3. MortgageCalculator: all about calculate.

### Extracting the Console class

IntelliJ Safe refactor: Refactor -> Refactor this -> Move to another class.

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

### Extracting the MortgageReport

```java
package com.codewithmosh;

import java.text.NumberFormat;

public class MortgageReport {
    private final MortgageCalculator calculator;
    private final NumberFormat currency;

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

### Extracting the MortgageCalculator

Generate -> Constructor, etc.

```java
package com.codewithmosh;

public class MortgageCalculator {
    private final byte MONTHS_IN_YEAR = 12;

    private final int principal;
    private final float annualInterestRate;
    private final byte years;

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
        byte PERCENT = 100;
        return annualInterestRate / PERCENT / MONTHS_IN_YEAR;
    }

    private int getNumberOfPayments() {
        return years * MONTHS_IN_YEAR;
    }
}

```

`Main` class:

```java
package com.codewithmosh;

public class Main {
    public static void main(String[] args) {
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

## Inheritance

```java
public class Child extends Parent {
    ...
}
```

### Object class

All class directly or indirectly inherits from the `Object` class. Has `hashCode`, `equals`, `toString` ... methods.

```java
package com.codewithmosh;

public class Main {
    public static void main(String[] args) {
        TextBox box1 = new TextBox();
        TextBox box2 = box1;
        // calculate based on the address of this object in memory
        System.out.println(box1.hashCode());
        // both objects reference the same object in memory
        System.out.println(box2.hashCode());

        // compare based on their hashCode
        TextBox box3 =  new TextBox();
        System.out.println(box1.equals(box2));  // true
        System.out.println(box1.equals(box3));  // false

        // can be overloaded
        System.out.println(box1.toString());
    }
}
```

### Constructors and inheritance

will call parent's Constructor first!

```java
public class UIControl {
    private boolean isEnabled = true;

    public UIControl(boolean isEnabled) {
        this.isEnabled = isEnabled;
        System.out.println("UIControl");
    }
    ...
    }
```

```java
public class TextBox extends UIControl{
    private String text = "";

    public TextBox() {
        // explicitly call constructor
        // should be the first statement of constructor
        super(true);
        System.out.println("TextBox");
    }
    ...
    }
```

### Access modifiers

Private members (fields and methods): `not inherited by subclasses`, not accessible outside the class.

Protected members: public in package (`com.codewithmosh`), accessible by child classes in different packages, kind of confusing, should avoid it.

no access modifier: package private, public in package, private outside the package.


### Method overriding

Not method overloading (implement using different parameters).

```java
// Override the toString method in the base Object class
// @Override is annotation, get extra information to the Java Compiler
@Override
public String toString() {
    return text;
}
```

in `Main`:

```java
package com.codewithmosh;

public class Main {
    public static void main(String[] args) {
        TextBox textBox = new TextBox();
        textBox.setText("Hello");
        System.out.println(textBox.toString());
        // println automatically call toString method
        System.out.println(textBox);
    }
}
```

### Upcasting and downcasting

* Upcasting: casting an object to one of its super types
* Downcasting: casting an object to one of its sub types

```java
package com.codewithmosh;

public class Main {
    public static void main(String[] args) {
        UIControl control = new UIControl(true);
        TextBox textBox = new TextBox();
        // Up-casting: TextBox is UIControl
        show(textBox);
    }

    public static void show(UIControl control) {
        // Down-casting: UIControl -> TextBox
        // make setText accessible at compile time
        if (control instanceof TextBox) {
            TextBox textBox = (TextBox) control;
            textBox.setText("Hello World");
        }
        System.out.println(control);
    }
}
```

### Comparing objects

Override the `equals` method and compare objects based on their content.


Best practice: whenever we override the `equals` method, we should also override the `hashCode` method.

```java
@Override
public boolean equals(Object obj) {
    // if same reference
    if (this == obj) {
        return true;
    }
    // not the same type
    if (!(obj instanceof Point)) {
        return false;
    }
    // down-casting
    Point other = (Point)obj;
    return other.x == x && other.y == y;
}

@Override
public int hashCode() {
    // default hashCode hash based on the address.
    // hashCode based on the content of the object.
    return Objects.hash(x, y);
}
```
in `Main`:

```java
package com.codewithmosh;

public class Main {
    public static void main(String[] args) {
        Point point1 = new Point(1, 2);
        Point point2 = new Point(1, 2);
        System.out.println(point1.equals(point2));
        System.out.println(point1.hashCode());
        System.out.println(point2.hashCode());
    }
}
```

### Polymorphism

Means many forms. Allows an object to take different forms.

```java
public class CheckBox extends UIControl{
    @Override
    public void render() {
        System.out.println("Render CheckBox");
    }
}
```

```java
public class TextBox extends UIControl{
    @Override
    public void render() {
        System.out.println("Render TextBox");
    }
    ...
    }
```

in `Main`:

```java
public class Main {
    public static void main(String[] args) {
        UIControl[] controls = { new TextBox(), new CheckBox()};
        // each object has it's own render method
        // in many different forms
        for (UIControl control:
             controls) {
            control.render();
        }
    }
}
```

### Abstract classes and methods

```java
public abstract class UIControl {
    // method declaration, not implementation
    public abstract void render();
    ...
}
```

### Final classes and methods

Classes and methods that we can not extend any more.

```java
public final class CheckBox extends UIControl{
    @Override
    public final void render() {
        System.out.println("Render CheckBox");
    }
}
```

### Deep inheritance and hierarchies

Don't create deep inheritance and hierarchies.

### Multiple inheritance

Java class has at most one parent. They want Java to be simple and robust.



## Interfaces

We use interface to build loosely-coupled, extensible, testable applications.

We should try to keep the coupling or relationship between classes as loosely as possible. Abstract is not enough.

An interface is a type similar to a class, but it includes only methods declarations.

```java
public interface Draggleble {
    void drag();
}
```

* Interfaces: what should be down.
* Classes: How it should be down.

### Tightly-coupled code

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

### Creating an interface

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

    // best practice to use Override
    @Override
    public double calculateTax() {
        return taxableIncome * 0.3;
    }
}
```

### Dependency injection

Our classes should not instantiate their dependencies. Do not create it, just use it.

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

We can change the dependencies of class throughout the lifetime of our application.

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

In reality, most of the time, we use construct injection.

### Interface segregation principal

segregation: 隔离并差别对待。

Divide big interfaces into smaller ones.

Unlike classes, Java interface can have multiple parents.


### Project: Mytube Video Platform

### Interfaces vs Abstract classes

* Interfaces: Contracts, no implementation.
* Abstract classes: Partially-completed classes, to share code between a few classes.

Use interfaces when you want to decouple a class from it's dependencies. 

* You can easily swap implementation to another. 
* Extend your applications with minimal impact. Program against interfaces.
* Test your classes in isolation, unit test.
