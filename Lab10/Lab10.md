# Lab: Understanding Advanced Inheritance and Composition in C++
---

## 🔹 1. Private Inheritance

### What is Private Inheritance?

Private inheritance means when one class (child) inherits from another class (parent), all public and protected members of the parent become **private** in the child.

This means the child class can use the parent’s features, but no one outside the child class can use them.

###  Why Use It?

Use private inheritance when you **don’t want to expose** the parent’s features directly but still want to **reuse its functionality**.

It’s like borrowing something from your elder brother but not letting your friends use it.

###  How It Works?

#### Simple Example:

```cpp
#include <iostream>
using namespace std;

class Animal {
public:
    void sound() {
        cout << "Animals make sound" << endl;
    }
};

class Dog : private Animal {
public:
    void makeSound() {
        sound();
    }
};

int main() {
    Dog d;
    d.makeSound();
    // d.sound(); // ❌ Error: private in Dog
    return 0;
}
```

####  Dry Run:

* `main()` creates object `d`
* `d.makeSound()` is called
* Inside `makeSound()`, `sound()` is used (private now)

#### Example 2:

```cpp
#include <iostream>
using namespace std;

class Printer {
protected:
    void showReady() {
        cout << "Printer is ready" << endl;
    }
};

class OfficePrinter : private Printer {
public:
    void printDocument() {
        showReady();
        cout << "Printing document..." << endl;
    }
};

int main() {
    OfficePrinter op;
    op.printDocument();
    return 0;
}
```

####  Dry Run:

* `OfficePrinter` can use `showReady()` but user cannot

---

## 🔹 2. Protected Inheritance

###  What is Protected Inheritance?

Public and protected members of base class become **protected** in derived class.

This means child class and its own children can use them, but outside world cannot.

###  Why Use It?

Use it when you want to allow **only your child classes** to access the features, but **not the outside world**.

### How It Works?

####  Example:

```cpp
class Vehicle {
public:
    void start() {
        cout << "Vehicle started" << endl;
    }
};

class Car : protected Vehicle {
public:
    void drive() {
        start();
    }
};

int main() {
    Car c;
    c.drive();
    return 0;
}
```

####  Dry Run:

* `Car` uses `start()` from `Vehicle` but user can’t

####  Example 2:

```cpp
class Machine {
protected:
    void powerOn() {
        cout << "Machine powered on" << endl;
    }
};

class WashingMachine : protected Machine {
public:
    void startWash() {
        powerOn();
        cout << "Washing clothes..." << endl;
    }
};

int main() {
    WashingMachine wm;
    wm.startWash();
    return 0;
}
```

####  Dry Run:

* `WashingMachine` can use `powerOn()` but not accessible outside

---

## 🔹 3. Composition (Has-A Relationship)

###  What is Composition?

Composition means putting one class **inside** another class as an object. It’s also called “**has-a**” relationship.

Example: Car has an Engine.

###  Why Use It?

When two things are not related like parent-child, but one **uses** another.

###  How It Works?

#### Example:

```cpp
class Engine {
public:
    void startEngine() {
        cout << "Engine started" << endl;
    }
};

class Car {
    Engine e;
public:
    void drive() {
        e.startEngine();
        cout << "Car is driving" << endl;
    }
};
```

####  Dry Run:

* Car uses Engine’s function

####  Complex Example:

```cpp
class Battery {
public:
    void charge() {
        cout << "Battery charging" << endl;
    }
};

class Smartphone {
private:
    Battery battery; // Composition
public:
    void usePhone() {
        battery.charge();
        cout << "Phone is working!" << endl;
    }
};
```

---

## 🔹 4. Composite Objects

###  What is It?

A **composite object** is just an object that contains other objects (just like Composition).

###  Why Use It?

To break large functionality into smaller classes.

####  Example:

```cpp
class Screen {
public:
    void display() {
        cout << "Showing screen" << endl;
    }
};

class Laptop {
    Screen screen; // composite object
public:
    void turnOn() {
        screen.display();
        cout << "Laptop is on!" << endl;
    }
};
```

---

## 🔹 5. Single Inheritance

###  What is It?

One base class, one child class. Classic parent-child relation.

###  Why Use It?

To reuse code and add more features in derived class.

####  Simple Example:

```cpp
class Animal {
public:
    void eat() {
        cout << "Animal eating" << endl;
    }
};

class Cat : public Animal {
public:
    void meow() {
        cout << "Meow!" << endl;
    }
};
```

####  Complex Example:

```cpp
class Person {
protected:
    string name;
public:
    Person(string n) : name(n) {}
};

class Student : public Person {
private:
    int id;
public:
    Student(string n, int i) : Person(n), id(i) {}
    void display() {
        cout << "Name: " << name << ", ID: " << id << endl;
    }
};
```

---

## 🔹 6. Multiple Inheritance

###  What is It?

One class inherits from **two or more** classes.

###  Why Use It?

To **combine features** from different classes.

####  Example:

```cpp
class Father {
public:
    void house() {
        cout << "Father's house" << endl;
    }
};

class Mother {
public:
    void car() {
        cout << "Mother's car" << endl;
    }
};

class Child : public Father, public Mother {
public:
    void ownProperty() {
        cout << "Child has both!" << endl;
    }
};
```

####  Example 2:

```cpp
class Developer {
protected:
    string language = "C++";
};

class Writer {
protected:
    string tool = "Word";
};

class TechBlogger : public Developer, public Writer {
public:
    void blog() {
        cout << "Writes blog in " << language << " using " << tool << endl;
    }
};
```

---

##  Summary Table

| Concept               | Inherits from | Access Level in Derived  | Use Case Example |
| --------------------- | ------------- | ------------------------ | ---------------- |
| Private Inheritance   | Base class    | Members become private   | Dog-Animal       |
| Protected Inheritance | Base class    | Members become protected | Car-Vehicle      |
| Composition           | Has object    | Use another class        | Car-Engine       |
| Single Inheritance    | One base      | Standard inheritance     | Student-Person   |
| Multiple Inheritance  | Two or more   | Combine features         | TechBlogger      |

---

##  Practice Tasks

1. Create a class `Book` and a class `Library` using composition.
2. Create a base class `Appliance` and a class `Fridge` using single inheritance.
3. Create classes `Painter`, `Musician`, and `Artist` using multiple inheritance.
4. Create a class `Device` with a protected method, and a class `Phone` that inherits it using protected inheritance.
5. Use private inheritance with `Building` and `Apartment` classes.

---

