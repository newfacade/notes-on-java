# Exceptions

```{note}
An exception is an object that contains information about an error.
```

## Types of exceptions

In Java, we have three types of exceptions:

* Checked exceptions: we developer should anticipate and handle properly, Java compiler inforces us to handle these exceptions.
* Unchecked exceptions (runtime exceptions): Not checked by the compiler at compile time, e.g. `ArithmeticException` if divide by 0.
* Errors: Error external to our application, e.g. `OutOfMemoryError`.

## Catching exceptions

```java
package com.codewithmosh;

import java.io.FileNotFoundException;
import java.io.FileReader;

public class Main {

    public static void main(String[] args) {
        // Surround with try/catch
        try {
            FileReader reader = new FileReader("file.txt");
            System.out.println("File opened.");
        } catch (FileNotFoundException ex) {
            // ex is an instance of FileNotFoundException
            // or anything else
            System.out.println(ex.getMessage());
        }
    }
}
```

## Catching multiple types of exceptions

```java
package com.codewithmosh;

import java.io.FileNotFoundException;
import java.io.FileReader;
import java.io.IOException;

public class Main {

    public static void main(String[] args) {
        try {
            FileReader reader = new FileReader("file.txt");
            double  value = reader.read();
        } catch (FileNotFoundException ex) {
            // handle `FileReader reader = new FileReader("file.txt");`
            ex.printStackTrace();
        } catch (IOException ex) {
            // handle `double  value = reader.read();`
            System.out.println("Could not read data.");
        }
    }
}
```

or use the `|` operator:

```java
try {
    // FileNotFoundException is an instance of IOException
    FileReader reader = new FileReader("file.txt");
    double  value = reader.read();
    new SimpleDateFormat().parse("");
} catch (IOException | ParseException e) {
    System.out.println("An IOException or ParseException occured.");
}
```

## The finally block

The finally block will always executed.

```java
package com.codewithmosh;

import java.io.FileReader;
import java.io.IOException;

public class Main {

    public static void main(String[] args) {
        FileReader reader = null;
        try {
            reader = new FileReader("file.txt");
            double value = reader.read();
            reader.close();
        } catch (IOException e) {
            System.out.println("An IOException or ParseException occured.");
        } finally {
            if (reader != null) {
                try {
                    reader.close();
                } catch (IOException e) {
                    e.printStackTrace();
                }
            }
        }
    }
}
```

ugly.

## The try-with-resources statement

We don't need to explicitly close these resources then.

```java
public static void main(String[] args) {
    try (FileReader reader = new FileReader("file.txt")) {
        double  value = reader.read();
    }
    catch (IOException e) {
        System.out.println(e.getMessage());
    }
}
```

beautiful.

## Throwing exceptions

```java
package com.codewithmosh.exceptions;

public class Account {
    // defensive programming
    // at the boundary of the application, not within
    public void deposit(float value) {
        if (value <= 0) {
            throw new IllegalArgumentException();
        }
    }
}
```

When we throw an exception that needs to handle, use `throws`:

```java
package com.codewithmosh.exceptions;

import java.io.IOException;

public class Account {
    public void deposit(float value) throws IOException {
        if (value <= 0) {
            throw new IOException();
        }
    }
}
```

## Custom exceptions

```java
package com.codewithmosh.exceptions;

// Checked -> Exception
// Unchecked (runtime) -> RuntimeException

public class InsufficientFundsException extends Exception{
    public InsufficientFundsException() {
        super("Insufficient funds in your account.");
    }

    public InsufficientFundsException(String message) {
        super(message);
    }
}
```

Usage:

```java
package com.codewithmosh.exceptions;

import java.io.IOException;

public class Account {
    private float balance;

    public void deposit(float value) throws IOException {
        if (value <= 0) {
            throw new IOException();
        }
    }

    public void withdraw(float value) throws InsufficientFundsException{
        if (value > balance) {
            throw new InsufficientFundsException();
        }
    }
}
```

