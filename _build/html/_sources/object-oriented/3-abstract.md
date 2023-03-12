# Abstraction

```{note}
Objects in an OOP language provide an abstraction that hides the internal implementation details.
```

## Constructors

Constrcutor is an method whose function name equals Class name, it has no return type.

```java
public class Employee {
    private int baseSalary;
    private int hourlyRate;
    
    // constructor
    public Employee(int baseSalary, int hourlyRate) {
        setBaseSalary(baseSalary);
        setHourlyRate(hourlyRate);
    }
    ...
    }
```

Use Constructor in Main:

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

```{caution}
If there is no explicit constructor, Java will create a default constructor that set all primitive types to 0 (or false) and set all reference types to null.
```

## Getters and setters

Create a getter and a setter for a field if necessary, so that we can set this field private.

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

## Coupling
 
Coupling is about how much a class is dependent upon or coupled to another class.

We want to reduce the coupling between classes.

## Method overloading

Creating different implementations with different parameters.

```java
public int calculateWage(int extraHours) {
    return baseSalary + (extraHours * hourlyRate);
}

public int calculateWage() {
    return calculateWage(0);
}
```

```{caution}
Remember overloading a method too many times will make your application hard to maintain.
```

### Constructor overloading

```java
public Employee(int baseSalary, int hourlyRate) {
    setBaseSalary(baseSalary);
    setHourlyRate(hourlyRate);
}

public Employee(int baseSalary) {
    this(baseSalary, 0);
}
```

## Static members

A class can have two types of members.

* instance members: belong to instances or objects. we can access through the `.` operator(e.g. `employee.calculateWage()`)

* static members: or class members. belong to a class, not objects(e.g. `Employee.numberOfEmployees`). When we want to present a concept that should be in a single place, the value is independent of objects, and we want to share it between all objects, set it static.

Employee:

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
        // use static field
        System.out.println(Employee.numberOfEmployees);
        // use static methods
        Employee.printNumberOfEmployees();
        int wage = employee.calculateWage(10);
        System.out.println(wage);
    }
}
```

```{note}
Static methods can only see the other static methods in this class.<br>
main method be static, this enables the java runtime to directly call the method without having to create a new object.
```
