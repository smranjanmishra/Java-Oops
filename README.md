# Java Object-Oriented Programming Concepts

## Table of Contents
- [Introduction to OOP](#introduction-to-oop)
- [Access Modifiers](#access-modifiers)
- [Getters and Setters](#getters-and-setters)
- [Encapsulation](#encapsulation)
- [Constructors](#constructors)
  - [Types of Constructors](#types-of-constructors)
  - [Copy Constructor](#copy-constructor)
  - [Shallow vs Deep Copy](#shallow-vs-deep-copy)
- [Inheritance](#inheritance)
  - [Types of Inheritance](#types-of-inheritance)
- [Polymorphism](#polymorphism)
  - [Method Overloading](#method-overloading)
  - [Method Overriding](#method-overriding)
- [Packages](#packages)
- [Abstraction](#abstraction)
  - [Abstract Classes](#abstract-classes)
  - [Interfaces](#interfaces)
- [Static Keyword](#static-keyword)
- [Super Keyword](#super-keyword)

## Introduction to OOP

**Objects:** Entities in the real world  
**Classes:** Groups of these entities

> **Note:** A class is a blueprint from which objects are created.

**Class Structure:** Attributes (Properties) + Functions (Behaviors)  
Objects are stored in heap memory.

## Access Modifiers

Access modifiers are keywords that define the accessibility of a class and its members.

| Modifier | Class | Package | Subclass | World |
|----------|-------|---------|----------|-------|
| public | ✓ | ✓ | ✓ | ✓ |
| protected | ✓ | ✓ | ✓ | ✗ |
| default | ✓ | ✓ | ✗ | ✗ |
| private | ✓ | ✗ | ✗ | ✗ |

## Getters and Setters

- **Get:** To return the value
- **Set:** To modify the value
- **this:** Keyword used to refer to the current object

## Encapsulation

It is the process of binding or wrapping data along with its data holders (through Getter and Setter methods) known as Encapsulation.
- **Purpose:** Protect data and expose only necessary functionality.
- **Implementation:** Use private fields with public getter/setter methods.

```java
  class Student {
    private String name;
    private int age;

    public String getName() {
        return name;
    }

    public void setName(String name) {
        this.name = name;
    }
}
```

## Constructors

- A special method in Java
- Constructor name is always the same as the class name
- It does not have a return type
- Used for initialization and object creation
- Constructors are only called once at object creation
- Memory allocation happens when a constructor is called

**Example:**

```java
public class Constructor {
    public static void main(String[] args) {
        Student s1 = new Student();
    }
}

class Student {
    String name;
    int roll;

    Student(String name) {
        this.name = name;
    }
}
```

### Types of Constructors

1. **Non-Parameterized Constructor**
2. **Parameterized Constructor**

**Example:**

```java
class Student {
    String name;
    int age;

    // Non-parameterized constructor
    Student() {
        name = "Unknown";
        age = 0;
    }

    // Parameterized constructor
    Student(String n, int a) {
        name = n;
        age = a;
    }

    void display() {
        System.out.println(name + " " + age);
    }

    public static void main(String[] args) {
        Student s1 = new Student();
        Student s2 = new Student("Soumya", 24);
        s1.display();
        s2.display();
    }
}
```

### Copy Constructor
A copy constructor creates a new object by copying the data from an existing object of the same class.

**Example:**

```java
class Student {
    String name;
    int age;

    Student(String n, int a) {
        name = n;
        age = a;
    }

    Student(Student s) {
        name = s.name;
        age = s.age;
    }

    void display() {
        System.out.println(name + " " + age);
    }

    public static void main(String[] args) {
        Student s1 = new Student("Soumya", 24);
        Student s2 = new Student(s1);
        s2.display();
    }
}
```

### Shallow vs Deep Copy

#### Shallow Copy
Only copies references, not the actual objects.

```java
Student(Student s1) {
    marks = new int[3];
    this.name = s1.name;
    this.roll = s1.roll;
    this.marks = s1.marks;  // Only copies the reference
}
```

#### Deep Copy
Duplicates everything, including the objects being referenced.

```java
Student(Student s1) {
    marks = new int[3];
    this.name = s1.name;
    this.roll = s1.roll;
    for(int i = 0; i < marks.length; i++) {
        this.marks[i] = s1.marks[i];  // Copies each element
    }
}
```

#### Lazy Copy
Delays copying until a modification is needed. Initially shares the reference (like shallow copy) but creates a deep copy only when one object changes.

### Destructors
We do not use destructors in Java because Java has Garbage Collection.

## Inheritance

- Acquiring the properties of one class into another class is known as Inheritance.

### Types of Inheritance

Java supports 5 types of inheritance:

1. **Single Level**
2. **Multilevel**
3. **Hierarchical**
4. **Hybrid (using interfaces)**
5. **Multiple (using interfaces)**

#### 1. Single Level Inheritance

```java
class A {
    void show() {
        System.out.println("A");
    }
}

class B extends A {
    void display() {
        System.out.println("B");
    }
}

public class Main {
    public static void main(String[] args) {
        B b = new B();
        b.show();
        b.display();
    }
}
```

#### 2. Multilevel Inheritance

```java
class A {
    void show() {
        System.out.println("A");
    }
}

class B extends A {
    void display() {
        System.out.println("B");
    }
}

class C extends B {
    void print() {
        System.out.println("C");
    }
}

public class Main {
    public static void main(String[] args) {
        C c = new C();
        c.show();
        c.display();
        c.print();
    }
}
```

#### 3. Hierarchical Inheritance

```java
class A {
    void show() {
        System.out.println("A");
    }
}

class B extends A {
    void display() {
        System.out.println("B");
    }
}

class C extends A {
    void print() {
        System.out.println("C");
    }
}

public class Main {
    public static void main(String[] args) {
        B b = new B();
        C c = new C();
        b.show();
        b.display();
        c.show();
        c.print();
    }
}
```

#### 4. Hybrid Inheritance (using interface)

```java
interface A {
    void show();
}

class B {
    void display() {
        System.out.println("B");
    }
}

class C extends B implements A {
    public void show() {
        System.out.println("A");
    }
    
    void print() {
        System.out.println("C");
    }
}

public class Main {
    public static void main(String[] args) {
        C c = new C();
        c.show();
        c.display();
        c.print();
    }
}
```

#### 5. Multiple Inheritance (using interfaces)

```java
interface A {
    void show();
}

interface B {
    void display();
}

class C implements A, B {
    public void show() {
        System.out.println("A");
    }
    
    public void display() {
        System.out.println("B");
    }
}

public class Main {
    public static void main(String[] args) {
        C c = new C();
        c.show();
        c.display();
    }
}
```

## Polymorphism

- "Poly" means many and "Morph" means forms
- There are 2 types of Polymorphism:
  1. Compile-time Polymorphism (Method Overloading) - static
  2. Runtime Polymorphism (Method Overriding) - dynamic

### Method Overloading

In a single class, multiple functions with the same name but different parameters is called Method Overloading.

**Example:**

```java
public class MethodOverloading {
    public static void main(String[] args) {
        Calculator calc = new Calculator();
        System.out.println(calc.sum(1, 2));
        System.out.println(calc.sum((float)1.5, (float)2.5));
        System.out.println(calc.sum(1, 2, 3));
    }
}

class Calculator {
    int sum(int a, int b) {
        return a + b;
    }
    
    float sum(float a, float b) {
        return a + b;
    }
    
    int sum(int a, int b, int c) {
        return a + b + c;
    }
}
```

### Method Overriding

- In two different classes having the same method name and same parameters is called Method Overriding
- Parent and child classes both contain the same function with a different definition

**Example:**

```java
public class Oops {
    public static void main(String[] args) {
        Deer d = new Deer();
        d.eat();
    }
}

class Animal {
    void eat() {
        System.out.println("Eats Anything");
    }
}

class Deer extends Animal {
    void eat() {
        System.out.println("Eats grass");
    }
}
```

## Packages

Packages are groups of similar types of classes, interfaces, and sub-packages.

## Abstraction

- Hiding all the unnecessary details and showing only the important parts to the user
- It is of 2 types:
  1. Abstract classes
  2. Interfaces

### Abstract Classes

- Cannot create an instance of an abstract class
- Can have abstract and non-abstract methods
- Can have constructors

### Interfaces

- Interface is a blueprint of a class
- Implements multiple inheritance
- Used to achieve total abstraction
- All methods are public, abstract, and without implementation
- Variables in the interface are final, public, and static

## Static Keyword

- Static keyword in Java is used to share the same variable or method across all instances of a given class
- We can make static: properties, functions, blocks, nested classes

## Super Keyword

- Super keyword is used to refer to the immediate parent class object
- Basically, it is used for:
  1. To access parent's properties
  2. To access parent's functions
  3. To access parent's constructor
