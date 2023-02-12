## Java Virtual Machine - JVM

The goal was develop a machine that intepret the Java code and translate to other devices, for example: TV, Computers , DVD and etc..

- JDK : Java Development Kit
- JRE : Java Runtime Enviroment

To create a code with Java, must have `.java` extension and later pass the command `javac` to compile the code to `.class`, in which the JVM can read. After the javac compile the code, run the command java, and pass the public class name.

**Java code:**

```Java
public class Program {
  public static void main(String[] args) {
    System.out.println("Hello World")
  }
}
```

**how to compile and run the code:**

```bash
  javac Program.java # return a Program.class file that tje JMV can read
  java Program # Execute the code
  #   Hello world
```

### Major erros

- Forget to add the ";" after an instruction
- Use quote ('') instead of double quote ("")
- java is sensitive case, so if you write **Public** instead of **public**, will throw an exception

## Types Numbers

- int (Primitive): declare a integer number `5, 10, 60`, accepts only 32 bits number (limit is 2 billions)
- double (Primitive): declare a float number `10.3, 4.45`
- long (Primitive): accepts 64 bits, over 2 billions
- short (Primitive): small value, limit up to 5000;
- byte (Primitive): 256 limit

## Types String

- char (Primitive): use to declare a single character and unicode and uses single quote ´''´. (on background the type char is integer)
- String: is a reference type and holds a sequence of words

### Warning

**if you divide two integer and the return is supposed to be a float, the Java will automate return truncate the value.**

```Java
  int divideFiveByTwo = 5 / 2; // return 2
  // same happens if the type is double
  double divideFiveByTwo = 5 / 2; // return 2.0
  // To get the expected result, one of the number must be a double
  double divideFiveByTwo = 5.0 / 2; // return 2.5
```
