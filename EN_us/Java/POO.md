# Object-oriented programming Java

## **class**

Is a key word on java to define a type and can declare all variables inside the brackets `{}`

```Java
class Account {
// specification of attributes
  double balance;
  int agency;
  int accountNumber;
  String owner;
}

// This is a valid code in java, but can't run, because don't hava an entry point
```

This code above is a specification of an account, like a blueprint/schema to an account

<img src="https://i.imgur.com/brSrUWk.png
 /">

The table is a instance/object of type Conta

To create an object, use the key word `new`, like `new Account();`

obs: when use new to create an object and associate a varible to the object, the `new` don't return the object itself, instead point a ponter to the object by reference.

```Java
public class CreateAccount {

  public static void main(String[] args) {

     Account firstAccount = new Account();
     firstAccount.balance = 2000;
     firstAccount.agency = 1;
     firstAccount.owner = "Gabriel";
     firstAccount.accountNumber = 10;
    System.out.println(firstAccount);

  }

}
```

## **Atrribute default value**

When we instance a new object, java automate reset all attributes, so number types turn to 0 and tyoe String turn to _null_.

```Java
class Account {
  double double_; // default value -> 0.0
  int int_; // default value -> 0
  boolean boolean_; // default value -> false
  char char_; // default value -> 0 ASCII index
  String string_; // default valeu -> null
}
```

## **Reference X Objects**

- Reference is a pointer to an object type

```Java
  Account accountOne = new Account(); // create a reference to an object
  System.out.println(accoutOne); // output -> Account@372f7a8d

  Account accountTwo = accountOne; //create a reference to the same object that accountOne refences

  System.out.println(accoutTwo); // output -> Account@372f7a8d

  System.out.println(accoutTwo == accountOne) // return -> true
```

_OBS: variables in Java never receives an object, always will be a reference_

- Attribute: What's the class has
- Method: What's the class does

## **Method**

```Java
public class Account {
    double balance;
    int agency;
    int accountNumber;
    String owner;

    public void deposit(double value) {
        this.balance+= value;
    }
}
```

`this` is a optional key, is used to reference the object where the method was cretead.

To invoke the `deposit` method, we need to our variable that references the object.

```Java
public class CreateAccount {

  public static void main(String[] args) {
    Account account = new Account;
    account.deposit(1000);
    // add 1000 to the object's balance
  }
}
```

## **Structure of a method**

```Java
  void deposit(double value) {
    // what the method does
  }
```

- Return type: in this example the method don't have return. (`void`)
- Method's name
- Argument(s): is optional

## **null**

By default, when you call a variable that references a class that isn't already made, the return will be `null`. _In other words, the reference never was populated_.

## **Private Attribute**

- Is the principle of encapsulation

Use the key word `private` to turn an attribute in an private attribute.

An private aattribute can't be access outside of the class and can be assigned directly.

```Java
public class Student {
  String name;
  int age;
  String course;
  private double grade;

  public void addGrade(double grade) {
    this.grade += grade;
  }

}
/// Another file
public class Main {
  public static void main(String[] args) {
    Student gabriel = new Student();
    gabriel.age = 21;
    gabriel.course = "Business";
    gabriel.grade = 10.0; // will throw an exception (attribute has private access)
    gabriel.addGrade(10.0) // It works
  }
}
```

## **Getter x Setter**

When we have private attribute, we need tp create setters and getters to change the state of our attributes in a safer way. Is a convention to use the word `set` and `get` in the method, like: `setSomething` and `getSomething`.

The main reason to use setters, getters and private attributes is the refactor factor. When we need to change or validate somthing before assign the value, we can just change the code in one place and automatically changes on the rest of our code.

## **Constructor**

Is a way to tell which attributes must be aasign when the object is build. The constructor just occers one time and when the object is constructed. in other words, you can't use the object without passing these values.

```Java
public class Person {
  String name;
  int age;
  double weight;

  // The constructor
  // by default -> public Person { //c}
  public Person(String name, int age, double weight) {
    this.name = name;
    this.age = age;
    this.weight;
  }
}
```

_PS: the constructor is not a method and must be the same name as the class_

## **static**

Is a class's attribute and have the `static` keyword . A static attribute refences to the class itself and not an instance, so don't need to use `this` keyword. To create a static method, we also have to use the `static` keyword.

```Java
public class Person {
  String name;
  int age;
  double weight;
  private static int totalOfInstances;

  public Person() {
    Person.totalOfInstances++; // or totalOfInstance ++
    //
  }

  public int getTotalOfInstances() {
    return Person.totalOfIntances;
  }
}

public class Test {
  public static void main(String[] args) {
    Person person = new Person();
    Person person1 = new Person();
    Person person2 = new Person();
    System.out.println(Person.getTotalOfInstances); // return -> 3
  }
}
```
