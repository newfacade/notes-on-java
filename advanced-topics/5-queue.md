# Queue

```{note}
We uses queues in situations where we want to process jobs base on the order we receive them.
```

```java
package com.codewithmosh.collections;

import java.util.ArrayDeque;
import java.util.Queue;

public class QueueDemo {
    public static void show() {
        Queue<String> queue = new ArrayDeque<>();
        queue.add("c");
        queue.add("a");
        // same as add in ArrayDeque
        // b -> a -> c
        queue.offer("b");
        // return front, if empty return null
        System.out.println(queue.peek());  // c
        // return front, if empty throw an Exception
        System.out.println(queue.element());
        // remove front item, if empty throw an Exception
        queue.remove();
        // remove front item, if empty return null
        queue.poll();
    }
}
```