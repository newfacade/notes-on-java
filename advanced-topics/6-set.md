# Set

```{note}
Set represents a collection that contains no duplicates.
```

```java
package com.codewithmosh.collections;

import java.util.*;

public class SetDemo {
    public static void show() {
        Set<String> set = new HashSet<>();
        set.add("sky");
        set.add("is");
        set.add("blue");
        set.add("blue");
        // {sky, blue, is}
        // order is not guaranteed
        System.out.println(set);

        // list -> set
        Collection<String> collection = new ArrayList<>();
        Collections.addAll(collection, "a", "b", "c", "c");
        Set<String> stringSet = new HashSet<>(collection);
    }
}
```

Operations:

```java
package com.codewithmosh.collections;

import java.util.*;

public class SetDemo {
    public static void show() {
        Set<String> set1 = new HashSet<>(Arrays.asList("a", "b", "c"));
        Set<String> set2 = new HashSet<>(Arrays.asList("b", "c", "d"));
        // Union
        set1.addAll(set2); // change set1, keep set2
        System.out.println(set1); // {a, b, c, d}
        // Intersection
        set1.retainAll(set2);
        // Difference
        set1.removeAll(set2);
    }
}
```
