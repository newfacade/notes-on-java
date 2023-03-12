# Classes and Objects

```{note}
Classes are the blueprint or template for creating objects. Objects are instances of classes.
```

## Creating classes

In Java, we should add class ClassName to a file named ClassName.java

Sample code in `TextBox.java`:

```java
package com.codewithmosh;

// public: this class is visible to all the other classes in this project
public class TextBox {
    // Field, technically, we should not declare fields as public
    public String text;
    
    public void setText(String text) {
        // this is a reference to the current object
        this.text = text;
    }

    public void clear() {
        text = "";
    }
}
```

## Creating objects

```java
ClassName objectName = new ClassName(arguments);
```

As we stated in the initiazation of reference types.

```java
package com.codewithmosh;

public class Main {
    
    public static void main(String[] args) {
        TextBox textBox = new TextBox();
        textBox1.setText("This is a box");
        // if no setText, will print null, dangerous
        System.out.println(textBox.text);
    }
}
```

## Memory allocation

What happens under the hood when we create new objects in Java? In fact, Java manages two different areas of the memory:

* heap: stores objects.

* stack: stores short lived variables like all the primitives, as well as variables that stored references to objects on the heap.

When we exit a method, Java runtime will immediately remove all the variables in the stack. If there is no reference to one object in the heap and unused for a certain period of time, the backgroup process will automatically remove that object in the heap, this is called garbage collection.

So in Java, we don't need to worry about deallocation, Java will take care of that.
