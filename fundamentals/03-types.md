# Types

```{note}
There are two kinds of types in Java: the primitive types for storing simple values and the reference types for storing complex objects.
```

## Primitive types

| Type    | Bytes | Range       |
|---------|-------|-------------|
| byte    | 1     | [-128, 127] |
| short   | 2     | [-32k, 32k] |
| int     | 4     | [-2B, 2B]   |
| long    | 8     |             |
| float   | 4     |             |
| double  | 8     |             |
| char    | 2     | A,B,...     |
| boolean | 1     | true/false  |

```java
public class Main {
    
    public static void main(String[] args) {
        byte age = 30;
        short numCountries = 200;
        int income = 12_000;
        // L for long
        long viewsCount = 3_123_456_789L;

        // F for float
        float price = 10.99F;
        double newPrice = 10.88;

        // single quotation mark for char
        char letter = 'A';
        
        boolean isEligible = false;
    }
}
```

## Reference types

All the other types except the 8 primitive types, for example the `Date` type:

```java
import java.util.Date;

public class Main {
    
    public static void main(String[] args) {
        // need to allocate memory
        Date now = new Date();
        System.out.println(now);
    }
}
```

How to init reference types:

```java
TypeName name = new TypeName(Arguments);
```

## Primitive types vs Reference types

```java
import java.awt.*;

public class Main {
    
    public static void main(String[] args) {
        // x and y: different address in memory
        byte x = 1;
        byte y = x;
        x = 2;
        System.out.println(y);  // print 1

        // point1 and point2: reference the same address in memory
        Point point1 = new Point(1, 1);
        Point point2 = point1;
        point1.x = 2;
        System.out.println(point2);  // print java.awt.Point[x=2,y=1]
    }
}

```

## Strings

Initialize:

```java
String message = new String("Hello World");
// we can initialize String variable like Primitive types.
String newMessage = "Hello World";
```

Usefull methods (String is immutable, methods that modifies a String will return a new String object):

```java
String message = "Hello World" + "!!";
System.out.println(message.length());
// strip
System.out.println(message.trim());
System.out.println(message.toLowerCase());
System.out.println(message.endsWith("!!"));
// first index appears, if does not exists, return -1
System.out.println(message.indexOf("W"));
System.out.println(message.replace("!", "*"));
```

Escape sequences:

```java
String path = "\\User\\facer";
String quotation = "\"A quotated sentence\""
String basicEscape = "\n\t"
```


## Arrays

```java
import java.util.Arrays;

public class Main {
    
    public static void main(String[] args) {
        // arrays are reference types, need specify the size of the array
        int[] numbers = new int[5];
        numbers[0] = 1;
        numbers[1] = 2;
        
        // will print a wired string based on the address of the array
        System.out.println(numbers);
        // print numbers
        System.out.println(Arrays.toString(numbers));
    }
}
```

Simpler way to initialize an array:

```java
int[] numbers = {2, 3, 5, 1, 4};
```

Sort array:

```java
int[] numbers = {2, 3, 5, 1, 4};
Arrays.sort(numbers);
System.out.println(Arrays.toString(numbers));
```

## Multi-dimensional arrays

```java
// 2 rows, 3 columns
int[][] numbers = new int[2][3];
numbers[0][0] = 1;

// use deepToString to print numbers
System.out.println(Arrays.deepToString(numbers));

// simpler way to initialize
int[][] newNumbers = {{1, 2, 3}, {4, 5, 6}};
```

## Constants

```java
// use upper case name
final float PI = 3.14F;
```

## Casting

Implicit casting (chain: byte > short > int > long > float > double):

```java
byte x = 1;
// byte > int
int y = x;
```

Explicit casting:

```java
double x = 1;
// double > int
int y = (int)x;
```

When explicit casting, types needs to be compatible. We cannot cast `String` to `int` directly, the right way to do this:

```java
// int y = (int)x will raise a Exception
String x = "1";
// similarly, we have Short.parseShort(), Float.parseFloat() ...
int y = Integer.parseInt(x) + 2;
```
