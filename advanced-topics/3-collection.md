# Iterables

```{image} ../images/319-drawio.svg
:alt: frame
:class: bg-primary mb-1
:width: 500px
:align: center
```

## Iterable

How can we iterate over a list, without knowing anything about its internal implementation.

```java
package com.codewithmosh.generics;

import java.util.Iterator;

public class GenericList<T> implements Iterable<T>{
    private T[] items = (T[]) new Object[10];
    private int count;

    public void add(T item) {
        items[count++] = item;
    }

    public T get(int index) {
        return items[index];
    }

    // the only method we have to implement
    @Override
    public Iterator<T> iterator() {
        return new ListIterator(this);
    }

    // private nested class, implement how to iterator
    private class ListIterator implements Iterator<T> {
        private GenericList<T> list;
        private int index;

        public ListIterator(GenericList<T> list) {
            this.list = list;
        }

        @Override
        public boolean hasNext() {
            return (index < list.count);
        }

        @Override
        public T next() {
            return list.items[index++];
        }
    }
}
```

Usage:

```java
package com.codewithmosh;

import com.codewithmosh.generics.GenericList;

public class Main {

    public static void main(String[] args) {
        GenericList<String> list = new GenericList<>();
        list.add("a");
        list.add("b");
        // use hasNext() and next()
        for (String item:
             list) {
            System.out.println(item);
        }
    }
}
```

## Collection

```java
package com.codewithmosh.collections;

import java.util.ArrayList;
import java.util.Collection;
import java.util.Collections;

public class CollectionsDemo {
    public static void show() {
        Collection<String> collection = new ArrayList<>();
        // or collection.add("a"); collection.add("b"); collection.add("c");
        Collections.addAll(collection, "a", "b", "c");
        // remove all: clear()
        collection.remove("a");
        System.out.println(collection.contains("a"));
        System.out.println(collection.size());
        System.out.println(collection.isEmpty());
        System.out.println(collection);

        // reverse collection to array, 0 is OK
        String[] stringArray = collection.toArray(new String[0]);

        // compare
        Collection<String> other = new ArrayList<>();
        other.addAll(collection);
        System.out.println(collection ==  other);  // false, based on memory address
        System.out.println(collection.equals(other));  // true, based on content
    }
}
```
