# List

```{image} ../images/319-drawio.svg
:alt: frame
:class: bg-primary mb-1
:width: 500px
:align: center
```

## List methods

Use List, we can access objects by their index.

```java
package com.codewithmosh.collections;

import java.util.ArrayList;
import java.util.List;

public class ListDemo {
    public static void show() {
        // have all the methods in Collection
        List<String> list = new ArrayList<>();
        list.add("a");
        list.add(0, "!");  // overload add
        System.out.println(list);  // [!, a]
        System.out.println(list.get(0));  // get item by index
        System.out.println(list.set(0, "a+"));  // [a+, a]
        System.out.println(list.remove(0));  // remove by index
        System.out.println(list.indexOf("a"));  // first index else -1
        System.out.println(list.lastIndexOf("a"));
        System.out.println(list.subList(0, 2));  // [begin, end)
    }
}
```

## The comparable interface

```java
package com.codewithmosh.collections;

public class Customer implements Comparable<Customer>{
    private String name;

    public Customer(String name) {
        this.name = name;
    }

    @Override
    public int compareTo(Customer other) {
        // this <  other -> -1
        // this == other -> 0
        // this >  other -> 1
        return name.compareTo(other.name);
    }

    @Override
    public String toString() {
        return name;
    }
}
```

Usage:

```java
package com.codewithmosh;

import com.codewithmosh.collections.Customer;
import java.util.ArrayList;
import java.util.Collections;
import java.util.List;

public class Main {

    public static void main(String[] args) {
        List<Customer> customers = new ArrayList<>();
        customers.add(new Customer("b"));
        customers.add(new Customer("a"));
        customers.add(new Customer("c"));
        Collections.sort(customers);
        System.out.println(customers);  // [a, b, c]
    }
}
```

## The comparator interface

Suppose we want to sort Customers by their emails.

```java
package com.codewithmosh.collections;

public class Customer implements Comparable<Customer>{
    private String name;
    private String email;

    public Customer(String name, String email) {
        this.name = name;
        this.email = email;
    }

    @Override
    public int compareTo(Customer other) {
        // this <  other -> -1
        // this == other -> 0
        // this >  other -> 1
        return name.compareTo(other.name);
    }

    @Override
    public String toString() {
        return name;
    }

    public String getEmail() {
        return email;
    }
}
```

Build an `EmailComparator implements Comparator<Customer>`:

```java
package com.codewithmosh.collections;

import java.util.Comparator;

public class EmailComparator implements Comparator<Customer> {
    @Override
    public int compare(Customer o1, Customer o2) {
        return o1.getEmail().compareTo(o2.getEmail());
    }
}
```

Usage:

```java
package com.codewithmosh;

import com.codewithmosh.collections.Customer;
import com.codewithmosh.collections.EmailComparator;

import java.util.ArrayList;
import java.util.Collections;
import java.util.List;

public class Main {

    public static void main(String[] args) {
        List<Customer> customers = new ArrayList<>();
        customers.add(new Customer("b", "e3"));
        customers.add(new Customer("a", "e2"));
        customers.add(new Customer("c", "e1"));
        Collections.sort(customers);
        System.out.println(customers);  // [a, b, c]
        // overloaded sort
        Collections.sort(customers, new EmailComparator());
        System.out.println(customers);  // [c, a, b]
    }
}
```