# Packaging java applications

```{note}
A package in Java is used to group related classes. In this section, we will learn how to package your application into jar files so that you can give it to anyone who has a JRE(java runtime environment, a subset of JDK and a superset of JVM) and run the program.
```

Steps of package in IntelliJ

1. Click File > Project structure > Artifacts > + JAR from modules with dependencies (Module is another level of abstraction above packages).
2. Select Main Class, click OK, so now we have an artifacts for building this project as a jar file.
3. Build > Build Artifacts > Build.

Now we have a file like `out/artifacts/HelloWorld_jar/HelloWorld.jar`, open it in terminal and execute using this jar file:

```bash
(base) facer@localhost src % ls
HelloWorld.jar
(base) facer@localhost src % java -jar HelloWorld.jar
Hello World!
```
