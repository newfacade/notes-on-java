# Generics

```{note}
Generics allow you to abstract over types.
```

## Problem

Basic implementation of a list:

```java
package com.codewithmosh.generics;

public class List {
    private int[] items = new int[10];
    private int count;

    public void add(int item) {
        items[count++] = item;
    }

    public int get(int index) {
        return items[index];
    }
}
```

But we can only store integers here.

## A poor solution

```java
package com.codewithmosh.generics;

// array of Objects
public class List {
    private Object[] items = new Object[10];
    private int count;

    public void add(Object item) {
        items[count++] = item;
    }

    public Object get(int index) {
        return items[index];
    }
}
```

Usage:

```java
package com.codewithmosh;

import com.codewithmosh.generics.List;

public class Main {

    public static void main(String[] args) {
        List list = new List();
        // equals list.add(Integer.valueOf(1))
        list.add(1);
        list.add("1");

        // (int)list.get(1) will raise an RuntimeException
        int number = (int)list.get(0);
    }
}
```

## Generic classes

```java
package com.codewithmosh.generics;

// T is the type parameter of this class
public class GenericList<T> {
    // new T[10] is not OK
    private T[] items = (T[]) new Object[10];
    private int count;

    public void add(T item) {
        items[count++] = item;
    }

    public T get(int index) {
        return items[index];
    }
}
```

Usage:

```java
// GenericList<int> is not OK
GenericList<Integer> list = new GenericList<>();
```

## Generics and primitive types

When creating an instance of a generic type, we can only use a reference type as a generic type argument. Use wrapper classes instead.

```java
package com.codewithmosh;

import com.codewithmosh.generics.GenericList;

public class Main {

    public static void main(String[] args) {
        // int -> Integer
        // float -> Float
        // ...
        GenericList<Integer> list = new GenericList<>();
        list.add(1);  // Boxing
        int number = list.get(0);  // Unboxing
    }
}
```

## Constraints

`extends` Classes or Interfaces.

```java
public class GenericList<T extends Number>
```

or

```java
public class GenericList<T extends Comparable  & Cloneable>
```
