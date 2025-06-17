# Unit 6: Basic Object-Oriented Programming

## Introduction
**Object-Oriented Programming (OOP)** is a programming model that organizes code into **classes** of **objects** to make it easier to manage. It keeps code structured, readable, and easier to debug.

The Java programming language is built around this core **paradigm**, a style or way of programming. OOP is the most popular programming paradigm because of how well it matches human thinking.

Unit 6 and Unit 7 can be difficult to understand because of the more conceptual ideas. If you still have a hard time understanding the concepts in the lesson, ask the mentors for extra explanation.

### Table of Contents
- [Introduction](#introduction)
    - [Table of Contents](#table-of-contents)
- [Classes](#classes)
    - [Fields](#fields)
- [Objects](#objects)
    - [>Exercise: Octopus Creation](#exercise-octopus-creation)
- [Constructors](#constructors)
    - [The `this` Keyword](#the-this-keyword)
    - [>Exercise: Louvre Museum](#exercise-louvre-museum)
- [Modifiers](#modifiers)
    - [Access Modifiers](#access-modifiers)
    - [Non-Access Modifiers](#non-access-modifiers)
        - [Final Modifier](#final-modifier)
        - [Static Modifier](#static-modifier)
    - [>Exercise: Social Media App](#exercise-social-media-app)
- [Encapsulation](#encapsulation)
    - [>Exercise: Dog Shelter](#exercise-dog-shelter)
- [Recap](#recap)
- [>>Project: Pokédex](#project-pokédex)

[Feedback](#feedback) \
[License](#license)

## Classes
**Classes** are templates that we use to create objects. Classes act as a definition of the set of data and methods that all objects of that class have. They allow us to create multiple objects with the same functionality without writing the code multiple times.

Intuitively, a class is a type. For example, a `Car` class would describe the functionality of a bunch of actual car objects.

Note that in Java, not all classes are used to describe objects. For example, the main class holds the main method sometimes there is no need to create a 'main object'.

We can create classes like this:
```java
<modifiers> class <class_name> {
    // Code inside the class: methods, fields, and more!
}
```
Example:
```java
public class Person {
    String name; // field

    void speak() { // method
        System.out.println("yippee!");
    }
}
```
You've already been introduced to methods in the last unit. These define 'behavior' for the class's objects. Fields define the data, and will be explained shortly.

One class that you have already been using is the built-in `String` class. Note that `int`, `double`, and `boolean` are not technically classes, which will be discussed in the next unit.

## Objects
We refer to the things created using classes as **objects**. They are also called **instances** (of a class). \
These objects each contain their own set of data in their fields.

Like with `String` and `int`, use the class as the type when declaring variables, return type, etc.

We can create objects like this, using the `new` keyword:
```java
new <class_name>(<arguments>)
```
This **initializes** a new object of the class, ready to be used in your program! \
Example:
```
Person me = new Person();
```

### Fields
**Fields**, also called attributes, are like variables that are attached to an object of a class. Each object gets its own separate set of field data, independent from other objects.

Declaring a field is just like declaring a local variable, where the declaration is inside the class but outside any methods.

If the field declaration has an initial assignment, then the expression acts as the default field value for all objects of the class. This expression is evaluated every time an object is created, so each object doesn't share the same field object. \
However, many fields don't need default values, e.g. if the value is always provided by the object creator.

Example fields:
```java
public class Person {
    String name;
    int fingers = 10;
    int age;
}
```
You can access these fields with just their name, inside a non-static method of the same class. When a method of an object is called, the field accesses in the method will refer to that associated object's fields. \
You can then get and set a field like a normal variable.
```java
void speak() {
    System.out.println("yippee! My name is " + name);
}
```

For other objects though, the `.` has to be used, similar to methods:
```
<object>.<fieldName>
```
(Inside a main method of `Person`:)
```java
Person you = new Person();
you.age = 16;
System.out.println(you.fingers);
you.name = "Cool Person";
you.speak();
```

Full commented example:
```java
// Declares a (public) class called Person
public class Person {
    String name; // Declares a String field called name
    int fingers = 10; // Declares an int field with default value 10
    int age;

    void speak() { // Declares a method (no parameters, no return value)
        // Prints a greeting with the person's name
        System.out.println("yippee! My name is " + name);
    }

    public static void main(String[] args) {
        Person you = new Person(); // Creates a new person
        you.age = 16; // Sets a field on the person
        System.out.println(you.fingers); // Gets a field on the person
        you.name = "Cool Person";
        you.speak(); // Calls a method on the person
    }
}
```
Field declarations are typically put near the start of the class declaration, before the method declaration.

### >Exercise: Octopus Creation
You're a genetic engineer with a strange fixation on eight-appendaged marine life. Finally, you've made the breakthrough possible for creating a new octopus in your lab simply by declaring it in a computer program.

[`Octopus.java`](Octopus.java)
1. Create a class to hold your beloved octopuses. Add a field for how many tentacles they should have, with an appropriate default value.
2. Put a `main()` method in your class (`public static void main(String[] args) {}`)
3. Inside the `main()` method, create a new octopus.
4. Print the number of tentacles your octopus has.
5. The dolphins from Unit 2 attack and eat 2 of your octopus' tentacles (apparently they have a violent streak). Update the number of tentacles your octopus has.
6. Print the number of tentacles your octopus now has.

<details><summary>Solution Code</summary>

```java
public class Octopus {
    int tentacles = 8;
    public static void main(String[] args) {
        Octopus fredrick = new Octopus();
        System.out.println("Fredrick has " + fredrick.tentacles + " tentacles!");
        fredrick.tentacles -= 2;
        System.out.println("Now he has " + fredrick.tentacles + " tentacles :(");
    }
}
```
Output:
```
Fredrick has 8 tentacles!
Now he has 6 tentacles :(
```
</details>

## Constructors
Constructors are special methods that are called when an object is created. Constructors can initialize objects and set up or assign default values or inputs to their fields.

Recall that to create an object, we use `new ClassName()`, and can sometimes pass in arguments. You may have noticed it looks similar to a method call. \
These expressions invoke the constructor of the class. Constructors can be overloaded.

Note that the constructor doesn't return anything, and isn't what creates the object. The `new` operator creates the object.

The constructor declaration for a class looks like a regular method, where the return type is completely omitted, and the method name is the same as the class name.

Constructors look like this:
```java
// Constructors are created inside a class
class Main {
    // This is the constructor
    Main() {
        System.out.println("Making an object!");
    }

    public static void main(String[] args) {
        Main thingy = new Main();
        // Program output is: Making an object!
    }
}
```
This example demonstrates when the code block inside the constructor is run. Our constructor, `Main()`, does nothing but print a message when a new object of the `Main` class is created. In this program, the constructor is called when we create `thingy`, a new object of the `Main` class. The instantiation expression calls the constructor to initialize a new object, running the code inside and printing `Making an object!`.

Here is an example where the constructor initializes a field of the object:
```java
class Main {
    // This is where we declare fields that the constructor must initialize for each object
    int x; 

    // This is the constructor
    Main() {
        System.out.println("Making an object!");
        x = 10;
    }

    public static void main(String[] args) {
        Main thingy = new Main();
        System.out.println(thingy.x);
    }
}
```
Output:
```
Making an object!
10
```
In this example, new objects of class `Main` have their `x` field initialized to `10` in the constructor. Then, after the object is done being created, `System.out.println(thingy.x);` prints `10`. \

We can use *parameters* in constructors so the programmer using the class can easily customize the field values of individual objects:
```java
class Main {
    // This is where we declare fields that the constructor must initialize for each object
    int x; 
    int y;

    // This is the constructor
    Main(int z) {
        System.out.println("Making an object!");
        x = 10;
        y = z;
    }

    public static void main(String[] args) {
        Main thingy = new Main(5);
        System.out.println(thingy.x);
        System.out.println(thingy.y);

        Main item = new Main(0);
        System.out.println(item.y);
    }
}
```
Output:
```
Making an object!
10
5
Making an object!
0
```
Here, we have added another field `y` to the `Main` class. It's declared the same way `x` is, but the way we initialize it in the constructor is different. Now, our constructor takes in a *parameter* `z`, and sets `y` to the value of `z`. Now our different objects can have different initial field values of `y` depending on what we input to the constructor! \
These *parameterized* constructors take input arguments in the same way as normal methods with parameters.

### The `this` Keyword
We can use `this` to refer to the current, associated object being used in a method or constructor. \
This is useful when a local variable or parameter has the same name as a field we want to access. The local variable **shadows**, or hides, the field since using the name would be referring to the local variable instead of the field. \
So instead of:
```java
class Main {
    int x;
    int y;

    Main(int x, int y) {
        x = x; // x parameter is assigned to itself
        y = y; // y parameter is assigned to itself
        // Fields never get initialized
    }
}
```

We can write:
```java
class Main {
    int x;
    int y;

    Main(int x, int y) {
        this.x = x;
        this.y = y;
        // Both fields are properly assigned
    }
}
```
Here, we use the `this` keyword to specify that it is the *field* `x` being assigned to the *parameter* `x`, and the same for `y`.

It is only available in non-static methods; anywhere where instance fields are accessible, `this` keyword is also accessible.

### >Exercise: Louvre Museum
You're in charge of documenting the artworks in the Louvre (a very famous art museum). They want you to store this data in a way that's easily accessible and organized (hmm... I wonder if OOP can help with that...).

[`Artwork.java`](Artwork.java)
1. Create a class to store the `name`, `artist`, and `year` of creation of a work.
2. Create a parameterized constructor that assigns values for these fields for each new work.
3. Create a `main()` method (`public static void main(String[] args) {}`) inside the same class.
4. Record the painting `Mona Lisa`, created by `Leonardo da Vinci` in `1503` with a variable of an artwork object.
5. Record the painting `The Raft of the Medusa`, created by `Théodore Géricault` in `1818`.
6. For the second artwork, print a one-line description with the name, the artist, and year.

<details><summary>Solution Code</summary>

```java
public class Artwork {
    String name;
    String artist;
    int year;

    public Artwork(String name, String artist, int year) {
        this.name = name;
        this.artist = artist;
        this.year = year;
    }
    public static void main(String[] args) {
        Artwork monaLisa = new Artwork("Mona Lisa", "Leonardo da Vinci", 1503);
        Artwork raft = new Artwork("The Raft of Medusa", "Théodore Géricault", 1818);
        System.out.println("This work is called " + raft.name + ".");
        System.out.println(raft.name + " was created by " + raft.artist + " in " + raft.year + "!");
    }
}
```
Output:
```
This work is called The Raft of Medusa.
The Raft of Medusa was created by Théodore Géricault in 1818!
```
</details>

## Modifiers
We can use **modifiers** to specify in their declaration how classes, fields, methods, and sometimes variables, are accessed and used. \
The term for either a field or a method is a **member**. Constructors are considered methods.

When used, they are placed before the data type.

### Access Modifiers
**Access modifiers** specify the access level. These make sure that certain things can't be accessed from anywhere in the program, which helps enforce intended usage of objects. \
Note that packages and subclasses will be taught in the next unit.

Access modifiers for **classes**:  
| Modifier | Description                                 |
|----------|---------------------------------------------|
| `public` | The class is accessible by any other class. |
| default  | When a modifier isn't specified, the class  |
|          | is only accessible to classes in the same   |
|          | package.                                    |

Access modifiers for **members**:
| Modifier    | Description                                 |
|-------------|---------------------------------------------|
|   `public`  | The member is accessible to all classes.    |
|  `private`  | The member is only accessible inside the    |
|             | same class                                  |
|   default   | When a modifier isn't specified, the member |
|             | is only accessible in the same package.     |
| `protected` | The member is accessible in the same        |
|             | package and in *subclasses*.                |

What can be accessed by each modifier?

| Location                       | Default | Private | Protected | Public |
|--------------------------------|---------|---------|-----------|--------|
| Same Class                     |   Yes   |   Yes   |    Yes    |   Yes  |
| Same Package Subclass          |   Yes   |   No    |    Yes    |   Yes  |
| Same Package Non-Subclass      |   Yes   |   No    |    Yes    |   Yes  |
| Different Package Subclass     |   No    |   No    |    Yes    |   Yes  |
| Different Package Non-Subclass |   No    |   No    |    No     |   Yes  |

You can only have at most one *access* modifier for something. \
If there are multiple other modifiers, the access modifier always goes first before the others.

For members, we almost always use only either `public` or `private` in our codebases. \
If you aren't sure which access modifier to use, then put `private`; it is easier to change it later to `public` if needed.

### Non-Access Modifiers
**Non-access** modifiers are used to customize other aspects of a class, method, or constructor's functionality. \
There are many such modifiers, but this course will only cover the common two, as the rest are rather obscure.

#### Final Modifier
**`final`** is used to stop something from changing, which can mean a few different things:
- For *fields and variables*, `final` indicates that they cannot be modified after its first assignment.
- For *classes*, `final` indicates that they cannot be *extended* (subclassed) by other classes (more on this in Unit 7!).
- For *methods*, `final` means it cannot be overridden (more on this in Unit 7!).

The last two uses of `final` are not very common.

Note that, like some of the access modifiers, `final` just makes Java more strict and has it enforce extra safeguards. This may seem unnecessary, but it helps minimize mistakes and improve code clarity.

Example for `final`:
```java
public class Main {
    private int normal;
    private final int ultimate;
    
    public Main(int normal, int ultimate) {
        this.normal = normal;
        this.ultimate = ultimate; // First assignment is fine
    }
    
    public static void main(String[] args) {
        // Creates a new object with fields normal = 10, ultimate = 99
        Main object = new Main(10, 99);
        object.normal++; // Assigns 11 to normal
        object.ultimate = 100; // Illegal: Java will not run the program
    }
}
```
In this example, an error is caused by attempting to *reassign* the field `ultimate`; because we declared it as final, we cannot change its value later in the program.

#### Static Modifier
**`static`** is used to declare that fields and methods belong to the class, rather than an instance. \

A static field is a field on the class itself. Since there is only one class, it is the only copy of the field. \
Static fields can be accessed through the class or through an instance of the class.
```
public class Main {
    private static int n = 2;
    
    public static void main(String[] args) {
        System.out.println(Main.n);
        n = 4;
        Main obj = new Main();
        System.out.println(obj.n);
    }
}
```
Output:
```
2
4
```
This is in contrast to non-static fields, or instance fields, that can only be accessed through an instance, either with `.` or inside instance methods that are associated with an object.

In Unit 5, all methods were declared as static so we could use them without an object.

Often, static fields are also made final and initialized with a value. This essentially makes them a **constant**, a variable whose value never changes over the program's execution. \
Examples include mathematical constants like pi, the max speed of a robot, and the number of days in a year. Constants are typically put as static fields so that they can be used without an instance, and in many places.

Constants are named in `UPPER_CASE` style, with underscores `_` to separate words. They don't use `camelCase` or `PascalCase`.

If both `static` and `final` are used, `static` goes before `final`. The access modifier goes before those. Modifiers are put at the start of declarations.

### >Exercise: Social Media App
You're currently developing a new social media app, and working on how to make user details secure.

[`Account.java`](<Social Media App/Account.java>) [`Main.java`](<Social Media App/Main.java>)
1. Start in `Account.java` Each user's account should have three fields, `username`, `displayName`, and `password`.
    - `username` should be accessible anywhere but unchangeable once
    initialized.
    - `displayName` should be accessible anywhere and can change 
    freely.
    - `password` shouldn't be accessible outside the class and can 
    change freely.
2. Additionally, add a variable to keep track of how many users you have, starting at 0. It should be private and be independent of individual accounts.
3. Add a parameterized constructor that initializes the three user fields. It should also increment your user count by 1 and print it.
4. In `Main.java`, create your `Account` in the `main` method. Add a `username`, `displayName`, and `password` of your choice.
    - Note: If creating an `Account` is not working, open the command palette and try `Java: Clean Java Language Server Workspace`. This goes for any future exercises with multiple files stored in one folder.
5. Print your `displayName`.
6. Add a statement that tries to print your `password`. If you try to run the code, you should get an error! Then, comment this line out.

<details><summary>Solution Code</summary>
Account.java:

```java
public class Account {
    public final String username;
    public String displayName;
    private String password;
    private static int userCount = 0;

    public Account(String username, String displayName, String password) {
        this.username = username;
        this.displayName = displayName;
        this.password = password;
        userCount++;
        System.out.println("Current user count: " + userCount);
    }
}
```
Main.java:

```java
public class Main {
    public static void main(String[] args) {
        Account myAccount = new Account("Mimikyu", "Pikachu", "password123");
        System.out.println("My name: " + myAccount.displayName);
        // System.out.println("My password: " + myAccount.password);
    }
}
```
Output:
```
Current user count: 1
My name: Pikachu
```
</details>

Expected output:
```
Current user count: 1
(your display name)
```

## Encapsulation
**Encapsulation** is the practice of 'bundling' data and behavior into a single class. It is a core principle of OOP. \
One part of encapsulation is **data hiding**, which means hiding or controlling access to sensitive data so that outside code doesn't meddle with or corrupt it. \
With data hiding, the programmer can be more confident that an object's data is secure and correct, and it allows them to change internal implementation without worrying much about other users.

Earlier, we talked about how the `private` modifier made something accessible only in the same class. \
In Java, fields are *usually* made private. Then, if they need to be exposed to other classes, we create public **getter** and **setter** methods.

Example:
```java
public class Person {
    private String name;

    // Getter method
    public String getName() {
        return name;
    }

    // Setter method
    public void setName(String newName) {
        name = newName;
    }
}
```
Even though the `name` field is `private`, we can use our new getter and setter methods to access and modify the value of `name`.

In another class, trying to access the `name` of a `Person` object will produce an error:
```java
public class Main {
    public static void main(String[] args) {
        Person guy = new Person();
        guy.name = "Bob"; // Error! name is private
    }
}
```

But if we use the `getName()` and `setName()` methods, `name` can be accessed.
```java
public class Main {
    public static void main(String[] args) {
        Person guy = new Person();
        guy.setName("Bob");
        System.out.println(guy.getName()); // Output: Bob
    }
}
```

In this way, we can control and customize *how* fields are accessed outside the class, instead of offering direct access to the field itself. For example, we could check that a new name being set is valid. \
It is conventional that most data-related instance fields are private and only exposed with getter and setter methods (if needed).

### >Exercise: Dog Shelter
You're recording data on all the dogs at the shelter you volunteer at, and want to make sure other volunteers can use this data easily but without direct access to it.

[`Dog.java`](<Dog Shelter/Dog.java>) [`Shelter.java`](<Dog Shelter/Shelter.java>)
1. Create an `Dog` class with fields `name`, `age`, and `breed`, with getter and setter methods for each field. Don't add a constructor.
2. In a separate `Main` class, create a new dog and set `name`, `age`, and `breed` to `Millie', `3`, and `beagle`.
3. Print Millie's name, age, and breed, as well as a short message to encourage visitors to adopt her.

<details><summary>Solution Code</summary>
Dog.java:

```java
public class Dog {
    String name;
    int age;
    String breed;

    public String getName() {
        return name;
    }

    public void setName(String newName) {
        name = newName;
    }

    public int getAge() {
        return age;
    }

    public void setAge(int newAge) {
        age = newAge;
    }

    public String getBreed() {
        return breed;
    }

    public void setBreed(String newBreed) {
        breed = newBreed;
    }
}
```
Shelter.java:

```java
public class Shelter {
    public static void main(String[] args) {
        Dog millie = new Dog();
        millie.setName("Millie");
        millie.setAge(3);
        millie.setBreed("beagle");

        System.out.println("This is " + millie.getName() + "!");
        System.out.println("She is a " + millie.getBreed() + " and " + millie.getAge() + " years old.");
        System.out.println("She would be so happy to have a loving home!");
    }
}

```
Output:
```
This is Millie!
She is a beagle and 3 years old.
She would be so happy to have a loving home!
```
</details>

## Recap
- Object-oriented programming (OOP) is the programming paradigm of Java, and involves classes of objects
- Classes are like templates or blueprints for creating objects
- Objects, or instances of a class, are individual things containing their own set of data, and the class is the type
- Create an object with the `new` keyword, class name, and a call: e.g. `new Person("Name")`
- Fields, or attributes, are variables attached to each object of a class
- Fields of the current object can be accessed in a method with just the name; fields of other objects use `.`, e.g. `person.name`
- The constructor of a class, declared with class name and no return type, is called when an instance is created to initialize it
- The `this` keyword refers to the current object in a method
- Modifiers are optionally added to declarations to change certain behavior
- The access modifiers are `public`, `private`, `protected`, and also a default for when it is omitted
- The `final` modifier prevents a variable or field from being assigned to after its first assignment, or that a class or method cannot be extended
- The `static` modifier declares a field or method belongs to the class and is not associated with instances
- The order of modifiers is `<access>`, `static`, `final`; these modifiers are the first things in a declaration
- Encapsulation involves data hiding, which is achieved with using `private` on fields and exposing getter and setter methods

## >>Project: Pokédex
Create a program to model interactions between *Pokémon*, creatures that can battle each other. \
[`Pokemon.java`](Pokemon.java)

A Pokémon is described by:
- Species: e.g. `Pikachu`. Use this to refer to the Pokémon.
- Type: e.g. `Water`, `Fire`
- Max health: integer e.g. `100`
- Health: current health, cannot go below `0` or above max health. Initially starts at max health.
- Attack: integer e.g. `50`, how much damage this Pokémon does to a Pokémon it attacks

A Pokémon has behavior:
- Take damage: a Pokémon can be damaged by some amount
- Check if it is unconscious; a Pokémon is unconscious if it's health is `0`
- Heal: a Pokémon can heal by some amount, but not over its max health
- Check if it is friends with another Pokémon: a Pokémon is friends with another if they have the same type
- Interact with another Pokémon

When a Pokémon interacts with another (this is one-way, not two-way), the following occurs:
- If self is unconscious, do nothing. Otherwise:
- If other is a friend:
    - Do nothing if other is conscious
    - Heal other for 1/4 of self's max health (rounded down) if other is unconscious
- If other isn't a friend:
    - Attack other for self's attack damage if other is conscious. Self is also attacked for 1/2 of other's attack damage, rounded down.
    - Do nothing if other is unconscious

Make sure the program outputs the actions of Pokémon when interacting and any changes to health and consciousness.

Also, track the total number of times any Pokémon has been knocked out (number of knockouts).

Four Pokémon were spawned, and their stats are given below:
| Species | Type | Max health | Attack |
| - | - | - | - |
| `Pikachu` | `Electric` | `35` | `28` |
| `Charizard` | `Fire` | `78` | `42` |
| `Squirtle` | `Water` | `44` | `25` |
| `Charmander` | `Fire` | `38` | `26` |

Then, the following interactions occurred, in order: \
Charmander interacts with Pikachu \
Squirtle interacts with Charmander \
Charizard interacts with Squirtle \
Pikachu interacts with Squirtle \
Charizard interacts with Charmander \
Charmander interacts with Charizard \
Pikachu interacts with Charmander

Print the number of knockouts that have occurred, at the end.

<details><summary>Example output (wording may differ)</summary>

```
Charmander attacks Pikachu
Pikachu took 26 damage
Pikachu has 9 health left
Charmander took 14 damage
Charmander has 24 health left
Squirtle attacks Charmander
Charmander took 25 damage
Charmander was knocked unconscious
Squirtle took 13 damage
Squirtle has 31 health left
Charizard attacks Squirtle
Squirtle took 42 damage
Squirtle was knocked unconscious
Charizard took 12 damage
Charizard has 66 health left
Pikachu leaves the unconscious Squirtle alone
Charizard helps the unconscious Charmander
Charmander healed by 19
Charmander has 19 health left
Charmander is friends with Charizard
Pikachu attacks Charmander
Charmander took 28 damage
Charmander was knocked unconscious
Pikachu took 13 damage
Pikachu was knocked unconscious
Total knockouts: 4
```
</details>

## Feedback
Please provide feedback if you have any.
<details><summary>Possible feedback points</summary>

- Confusing explanations
- Knowledge, skills, or procedures that were required but weren't taught
- Too fast or too slow explanations; pacing
- Too hard or too easy exercises
- Step-by-step instructions that are not comprehensive/thorough enough, or didn't work
- Seemingly unnecessary or ineffective information or exercises
- Any improvements (e.g. wording) or more effective ways/formats to teach
</details>

___



## License
© 2025 @aatle, @spacepotatoes3, @gjgarson, @KaitoTLex

This work is licensed under a [Creative Commons Attribution 4.0 International License](https://creativecommons.org/licenses/by/4.0/).
