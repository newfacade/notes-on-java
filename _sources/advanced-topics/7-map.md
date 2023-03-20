# Map

```{note}
A map is a key-value pairs.
```

```java
package com.codewithmosh.collections;

import java.util.HashMap;
import java.util.Map;

public class MapDemo {
    public static void show() {
        Customer c1 = new Customer("a", "e1");
        Customer c2 = new Customer("b", "e2");
        Map<String, Customer> map = new HashMap<>();
        
        // put
        map.put(c1.getEmail(), c1);
        map.put(c2.getEmail(), c2);
        // get, if does not exists return null
        Customer c = map.get("e1");
        System.out.println(c);
        // get with default
        Customer unknown = new Customer("Unknown", "");
        Customer customer = map.getOrDefault("e10", unknown);
        System.out.println(customer);
        // if contains keys
        boolean exists = map.containsKey("e5");
        System.out.println(exists);
        // replace
        map.replace("e1", new Customer("a++", ""));
        System.out.println(map);
        
        // map is not Iterable,
        // we can not use for-each directly,
        // but we can also iterate.
        for (String key :
                map.keySet()) {
            System.out.println(key);
        }
        for (Customer value:
                map.values()) {
            System.out.println(value);
        }
        for (Map.Entry entry:
             map.entrySet()) {
            System.out.println(entry.getKey());
            System.out.println(entry.getValue());
        }
    }
}
```
