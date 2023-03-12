# Inheritance

```java
public class Child extends Parent {
    ...
}
```

## Object class

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

## Constructors and inheritance

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

## Access modifiers

Private members (fields and methods): `not inherited by subclasses`, not accessible outside the class.

Protected members: public in package (`com.codewithmosh`), accessible by child classes in different packages, kind of confusing, should avoid it.

no access modifier: package private, public in package, private outside the package.


## Method overriding

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

## Upcasting and downcasting

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

## Comparing objects

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
