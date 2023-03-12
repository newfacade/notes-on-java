# How Java code gets executed

There are two steps:

* Compilation: use Java compiler (in JDK) to compile *.java to byte code
* Execution: JVM(Java Virtual Machine, in JDK) translate byte code(platform independent) to native code (windows, mac, ...)

Compilation and execution using the command line:

```bash
(base) facer@localhost src % ls
Main.java
(base) facer@localhost src % javac Main.java
(base) facer@localhost src % java Main
Hello World!
(base) facer@localhost src % 
```
