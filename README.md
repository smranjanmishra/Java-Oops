## Java OOP Concepts
This README provides a concise overview of Object-Oriented Programming (OOP) concepts in Java, with examples for beginners and intermediate learners. Topics include objects, classes, access modifiers, encapsulation, constructors, inheritance, polymorphism, packages, abstraction, and keywords like static and super.

## Table of Contents

Objects and Classes </br>
Access Modifiers </br>
Encapsulation </br>
Constructors </br>
Destructors </br>
Inheritance </br>
Polymorphism </br>
Packages </br>
Abstraction </br>
Static Keyword </br>
Super Keyword </br>


## Objects and Classes

Objects : Entities in the real world
Classes : Group of these Entities

Note : Class is a blueprint from Objects are getting created.

Class : Attributes(Properties) + Functions(Behaviours)
        Objects are stored on Heap memory.

## Note: Objects are stored in heap memory.

class Student {
    String name;
    int roll;

    void display() {
        System.out.println("Name: " + name + ", Roll: " + roll);
    }
}


## Access Modifiers
Control the accessibility of classes and their members:

public: Accessible everywhere.
protected: Accessible in the same package and subclasses.
default (no modifier): Accessible in the same package.
private: Accessible only within the class.

class Student {
    private String name;
    public int roll;

    public String getName() {
        return name;
    }

    public void setName(String name) {
        this.name = name; // 'this' refers to current object
    }
}


## Encapsulation
Encapsulation wraps data and methods together, restricting access to fields via getters and setters.

Purpose: Protect data and expose only necessary functionality.
Implementation: Use private fields with public getter/setter methods.

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


## Constructors
Constructors initialize objects. They have the same name as the class, no return type, and are called once during object creation.

## Types
Non-Parameterized: Sets default values.
Parameterized: Initializes with specific values.
Copy Constructor: Copies data from an existing object.

class Student {
    String name;
    int age;

    // Non-Parameterized
    Student() {
        name = "Unknown";
        age = 0;
    }

    // Parameterized
    Student(String name, int age) {
        this.name = name;
        this.age = age;
    }

    // Copy Constructor
    Student(Student s) {
        this.name = s.name;
        this.age = s.age;
    }

    void display() {
        System.out.println(name + " " + age);
    }

    public static void main(String[] args) {
        Student s1 = new Student();
        Student s2 = new Student("Soumya", 24);
        Student s3 = new Student(s2);
        s1.display(); // Unknown 0
        s2.display(); // Soumya 24
        s3.display(); // Soumya 24
    }
}

## Copy Types

Shallow Copy: Copies references (changes affect both objects).
Deep Copy: Duplicates data (independent objects).
Lazy Copy: Delays copying until modification, combining shallow and deep copy.

class Student {
    String name;
    int[] marks;

    // Shallow Copy
    Student(Student s) {
        this.name = s.name;
        this.marks = s.marks; // Reference copy
    }

    // Deep Copy
    Student(Student s, boolean deep) {
        this.name = s.name;
        this.marks = new int[s.marks.length];
        for (int i = 0; i < s.marks.length; i++) {
            this.marks[i] = s.marks[i]; // Value copy
        }
    }
}


## Destructors
Java does not use explicit destructors. The Garbage Collector automatically manages memory by deallocating unused objects.

## Inheritance
Inheritance allows a class to inherit properties and methods from another class.

Types :

Single Level: One class inherits another.
Multilevel: A chain of inheritance (e.g., C → B → A).
Hierarchical: Multiple classes inherit from one parent.
Hybrid: Combines hierarchical and multiple inheritance (via interfaces).
Multiple: Achieved using interfaces (Java doesn't support multiple class inheritance).

## Single Level
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
        b.show(); // A
        b.display(); // B
    }
}

## Multiple Inheritance (Interfaces)
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
        c.show(); // A
        c.display(); // B
    }
}


## Polymorphism
Polymorphism allows methods to take multiple forms.
## 1. Compile-Time (Method Overloading)

Same method name, different parameters in a single class.
Resolved at compile time.

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

public class Main {
    public static void main(String[] args) {
        Calculator calc = new Calculator();
        System.out.println(calc.sum(1, 2)); // 3
        System.out.println(calc.sum(1.5f, 2.5f)); // 4.0
        System.out.println(calc.sum(1, 2, 3)); // 6
    }
}

## 2. Runtime (Method Overriding)

Child class redefines a parent class method with the same signature.
Resolved at runtime.

class Animal {
    void eat() {
        System.out.println("Eats Anything");
    }
}

class Deer extends Animal {
    void eat() {
        System.out.println("Eats Grass");
    }
}

public class Main {
    public static void main(String[] args) {
        Deer d = new Deer();
        d.eat(); // Eats Grass
    }
}


## Packages
Packages group related classes, interfaces, and sub-packages for organization and to avoid naming conflicts.
package com.example;

public class MyClass {
    public static void main(String[] args) {
        System.out.println("Inside com.example package");
    }
}


## Abstraction
Abstraction hides unnecessary details and shows only essential features.
## 1. Abstract Classes

Cannot be instantiated.
Can have abstract (no body) and non-abstract methods.
Can include constructors.

abstract class Animal {
    abstract void sound();

    void sleep() {
        System.out.println("Sleeping...");
    }
}

class Dog extends Animal {
    void sound() {
        System.out.println("Bark");
    }
}

public class Main {
    public static void main(String[] args) {
        Dog d = new Dog();
        d.sound(); // Bark
        d.sleep(); // Sleeping...
    }
}

## 2. Interfaces

Blueprint for classes, enforcing total abstraction.
Methods are public, abstract by default.
Variables are public, static, final.
Supports multiple inheritance.

interface Animal {
    void sound();
}

class Dog implements Animal {
    public void sound() {
        System.out.println("Bark");
    }
}

public class Main {
    public static void main(String[] args) {
        Dog d = new Dog();
        d.sound(); // Bark
    }
}


## Static Keyword
The static keyword makes variables, methods, blocks, or nested classes belong to the class, not instances.
class Student {
    static int count = 0;

    Student() {
        count++;
    }

    static void showCount() {
        System.out.println("Total Students: " + count);
    }
}

public class Main {
    public static void main(String[] args) {
        Student s1 = new Student();
        Student s2 = new Student();
        Student.showCount(); // Total Students: 2
    }
}


## Super Keyword
The super keyword refers to the immediate parent class. It is used to:

Access parent class fields.
Call parent class methods.
Invoke parent class constructors.

class Animal {
    String name = "Animal";

    void eat() {
        System.out.println("Eating...");
    }
}

class Dog extends Animal {
    String name = "Dog";

    Dog() {
        super(); // Calls parent constructor
    }

    void display() {
        System.out.println("Child: " + name); // Dog
        System.out.println("Parent: " + super.name); // Animal
        super.eat(); // Eating...
    }
}

public class Main {
    public static void main(String[] args) {
        Dog d = new Dog();
        d.display();
    }
}


Resources

Oracle Java Documentation
Experiment with the code examples in your IDE to deepen your understanding!
