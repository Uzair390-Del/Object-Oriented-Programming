#  Lab: Understanding Polymorphism in C++ 
---

## 1. What is Polymorphism?

###  What?

Polymorphism means "**many shapes or forms**." In programming, it means the **same thing can act differently** depending on the situation. In C++, it means the same function name can behave differently depending on the situation.

Think of a remote control. The same button (say "Play") does different things:

- On a TV, it plays a video.

- On a music player, it plays a song.

- On a game console, it starts the game.

In programming, polymorphism allows the same function to work in different ways based on the object.

###  Why?

It helps us **reuse the same name** for different things. So we don’t need to remember many names for similar tasks.

###  How?

There are two main types:

* **Compile-time polymorphism** (function overloading)
* **Run-time polymorphism** (function overriding using virtual functions)

---

## 🔹 2. Compile-Time Polymorphism (Function Overloading)

###  What?

Using the **same function name** but with **different types or numbers of inputs**.

###  Why?

To make code **cleaner** and **easier to understand**.

###  How?

You create functions with the same name but different parameters.

###  Example Code:

```cpp
#include <iostream>
using namespace std;

class Printer {
public:
    void print(int num) {
        cout << "Printing number: " << num << endl;
    }

    void print(string text) {
        cout << "Printing text: " << text << endl;
    }
};

int main() {
    Printer p;
    p.print(123);
    p.print("Hello");
    return 0;
}
```

###  Dry Run:

* `p.print(123)` calls the version that takes an integer.
* `p.print("Hello")` calls the version that takes a string.

---

##  3. Function Overriding (Runtime Polymorphism)

###  What?

When a **child class** creates a function with the **same name** as in the **parent class** and **replaces** it.

###  Why?

So that different objects can have **different behaviors** even when using the same name.

###  How?

* Create a function in the base class.
* Create the **same** function in the child class.

###  Example:

```cpp
#include <iostream>
using namespace std;

class Animal {
public:
    void sound() {
        cout << "Some generic animal sound" << endl;
    }
};

class Dog : public Animal {
public:
    void sound() {
        cout << "Bark!" << endl;
    }
};

int main() {
    Dog d;
    d.sound(); // Will call Dog's version
    return 0;
}
```
```cpp
#include <iostream>
using namespace std;

// Base class
class Animal {
public:
    virtual void makeSound() {
        cout << "Some generic animal sound" << endl;
    }
};

// Derived class
class Dog : public Animal {
public:
    void makeSound() override {
        cout << "Woof! Woof!" << endl;
    }
};

// Another derived class
class Cat : public Animal {
public:
    void makeSound() override {
        cout << "Meow!" << endl;
    }
};

int main() {
    Animal* a1 = new Dog();
    Animal* a2 = new Cat();

    a1->makeSound();    // Output: Woof! Woof!
    a2->makeSound();    // Output: Meow!

    delete a1;
    delete a2;
    return 0;
}
```

###  Dry Run:

* `d.sound()` checks in Dog first. Finds `Bark!`, and prints it.

---

##  4. Virtual Functions

###  What?

A **virtual function** lets the program decide **which version to run at runtime**, using a base class pointer.

###  Why?

To achieve **true polymorphism**, especially when working with **base class pointers**.

###  How?

* Use the `virtual` keyword in base class function.
* Use base class pointer to point to derived class object.

###  Example:

```cpp
#include <iostream>
using namespace std;

class Payment {
public:
    virtual void pay() {
        cout << "Paying with cash" << endl;
    }
};

class CreditCard : public Payment {
public:
    void pay() {
        cout << "Paying with credit card" << endl;
    }
};

int main() {
    Payment* p;
    CreditCard cc;
    p = &cc;
    p->pay(); // Calls derived class function
    return 0;
}
```

###  Dry Run:

* `p` is a pointer to `Payment`, but points to a `CreditCard` object.
* Since `pay()` is virtual, it calls the `CreditCard` version.

---

##  5. Abstract Classes & Pure Virtual Functions

###  What?

An **abstract class** cannot make objects. It has at least one **pure virtual function**. A **pure virtual function** has `= 0` at the end.


###  Why?

To create a **template or blueprint** that other classes must follow.
To provide shared functionality to all derived classes.
To avoid rewriting common code in every derived class.

###  How?

* Use `virtual void function() = 0;`
* Child classes must write their own version of the function.

###  Example:

```cpp
#include <iostream>
using namespace std;

class Shape {
public:
    virtual void draw() = 0; // Pure virtual function
};

class Circle : public Shape {
public:
    void draw() {
        cout << "Drawing Circle" << endl;
    }
};

int main() {
    Circle c;
    c.draw();
    return 0;
}
```

###  Dry Run:

* `Shape` has a rule: "All shapes must draw themselves."
* `Circle` obeys and creates its own version.
* `c.draw()` prints "Drawing Circle".

- In an abstract class in C++, you can include both normal (regular) functions and pure virtual functions.
An abstract class cannot be instantiated directly, but it can:
- Provide function implementations (normal functions).
- Be used as a base class.
- Force derived classes to implement pure virtual functions. 

#  Why do we need Abstract Classes in C++?

An abstract class is used when:

- You want to define a **common interface** for a group of related classes.
- You want to ensure that **certain functions must be implemented** by every derived class.
- You want to **avoid creating objects** of the base class because it's only a **concept**, not a real object.

---

###  Situation:

Imagine you are making a drawing app. You have different shapes: **Circle**, **Rectangle**, **Triangle**, etc. All shapes must have a `draw()` function.

But:

- Each shape draws differently.
- You don’t want to create a generic “Shape” object because a "Shape" by itself doesn't exist—only specific shapes do.

---

##  Solution: Use an Abstract Class

```cpp
#include <iostream>
using namespace std;

// Abstract class
class Shape {
public:
    // Pure virtual function
    virtual void draw() = 0;

    // Normal function
    void printType() {
        cout << "I am a shape" << endl;
    }
};

// Derived class
class Circle : public Shape {
public:
    void draw() override {
        cout << "Drawing a circle" << endl;
    }
};

// Another derived class
class Rectangle : public Shape {
public:
    void draw() override {
        cout << "Drawing a rectangle" << endl;
    }
};

int main() {
    Shape* s1 = new Circle();
    Shape* s2 = new Rectangle();

    s1->draw();         // Output: Drawing a circle
    s2->draw();         // Output: Drawing a rectangle

    s1->printType();    // Output: I am a shape
    s2->printType();    // Output: I am a shape

    delete s1;
    delete s2;
    return 0;
}


---

##  6.  Notification System

###  Code:

```cpp
#include <iostream>
using namespace std;

class Notification {
public:
    virtual void send() = 0;
};

class Email : public Notification {
public:
    void send() {
        cout << "Sending Email..." << endl;
    }
};

class SMS : public Notification {
public:
    void send() {
        cout << "Sending SMS..." << endl;
    }
};

int main() {
    Notification* n;
    Email e;
    SMS s;

    n = &e;
    n->send(); // Email

    n = &s;
    n->send(); // SMS
    return 0;
}
```

###  Dry Run:

* `n` is a pointer to `Notification`
* It first points to `Email`, calls email's send.
* Then it points to `SMS`, calls sms's send.

---

##  Summary Table

| Topic                | What?                              | Why?                               | How?                                   |
| -------------------- | ---------------------------------- | ---------------------------------- | -------------------------------------- |
| Function Overloading | Same name, different inputs        | Cleaner code                       | Defined multiple times with variations |
| Function Overriding  | Same name in child replaces parent | Specific behavior per object       | Same name, redefined in child          |
| Virtual Functions    | Decide at runtime which to call    | Dynamic behavior from base pointer | Use `virtual` in base class            |
| Abstract Class       | Can't create objects, has rules    | Standard structure for others      | Contains pure virtual function         |

---

##  Practice Tasks for Students

1. Create a `Calculator` class that uses function overloading for add(), subtract(), etc.
2. Create an abstract `MediaPlayer` class and implement `AudioPlayer` and `VideoPlayer`.
3. Write a program using base class pointer to call overridden methods in different child classes.

---


