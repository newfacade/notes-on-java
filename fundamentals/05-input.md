# Reading input

```{note}
Reading input using Scanner.
```

Initialization:

```java
Scanner scanner = new Scanner(InputStream);
```

Read:

```java
Type variableName = scanner.nextXX();
```

Sample code:

```java
import java.util.Scanner;

public class Main {
    
    public static void main(String[] args) {
        // read from the terminal window
        Scanner scanner = new Scanner(System.in);
        
        // use print to avoid new line
        System.out.print("Age: ");
        // get the next byte
        byte age = scanner.nextByte();
        // type 20, print You are 20
        System.out.println("You are " + age);

        System.out.print("Name: ");
        // get first word
        String name = scanner.next();
        // type Mosh, print You are Mosh
        // type Mosh Hamedani, also print You are Mosh
        System.out.println("You are " + name);

        System.out.print("Name: ");
        // get the whole line
        String line = scanner.nextLine().trim();
        // type Mosh Hamedani, print You are Mosh Hamedani
        System.out.println("You are " + name);
    }
}
```