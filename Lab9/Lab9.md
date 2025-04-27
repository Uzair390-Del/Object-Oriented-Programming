# Lab: Understanding Inheritance in C++

**Topics Covered:**
- What is Inheritance?
- Base Class and Derived Class
- Protected Access Specifier
- Public Inheritance
- Example Codes
- Dry Runs (Step-by-Step Explanations)

---

# 1. What is Inheritance? 

Imagine you have a **parent**  and a **child** .  
The child **inherits** (gets) some things from the parent, like **eyes**, **hair**, **height**!

Similarly, in C++, **one class** (child class) can **inherit** features (data and functions) from **another class** (parent class).

This helps to **reuse** code and **save time**! 

---

# 2. What is a Base Class and a Derived Class? 

- **Base Class**: The parent class. It has common features.
- **Derived Class**: The child class. It inherits from the base class.

**Example:**  
- **Animal** is a base class.
- **Dog** is a derived class.

---

# 3. What is Protected Access Specifier? 

When we write **protected**, it means:
- It is **private** to the outside world.
- But the **derived class** (child) can still **use** it.

Think of it like a **family secret** — outsiders can't know it, but family members do! 

---

# 4. What is Public Inheritance? 

When you use **public inheritance**, it means:
- Whatever is **public** in the base class stays **public** in the child class.
- Whatever is **protected** stays **protected**.

**Syntax:**
```cpp
class DerivedClass : public BaseClass
{
    // New things or changed things
};
```

---

# 5. Example Code 1:

```cpp
#include<iostream>
using namespace std;

// Base class
class Animal {
protected:
    string name;
public:
    void setName(string n) {
        name = n;
    }
    void display() {
        cout << "I am an animal. My name is " << name << endl;
    }
};

// Derived class
class Dog : public Animal {
public:
    void bark() {
        cout << name << " says: Woof! Woof!" << endl;
    }
};

int main() {
    Dog d1;
    d1.setName("Buddy");
    d1.display();
    d1.bark();
    return 0;
}
```

### Dry Run:
- `setName("Buddy")` sets `name` to "Buddy".
- `display()` prints: `I am an animal. My name is Buddy`
- `bark()` prints: `Buddy says: Woof! Woof!`

**Output:**
```
I am an animal. My name is Buddy
Buddy says: Woof! Woof!
```

---

# 6. Example Code 2: 

```cpp
#include<iostream>
using namespace std;

// Base class
class Vehicle {
protected:
    int wheels;
public:
    void setWheels(int w) {
        wheels = w;
    }
    void showWheels() {
        cout << "This vehicle has " << wheels << " wheels." << endl;
    }
};

// Derived class
class Car : public Vehicle {
public:
    void drive() {
        cout << "Driving a car with " << wheels << " wheels!" << endl;
    }
};

int main() {
    Car c1;
    c1.setWheels(4);
    c1.showWheels();
    c1.drive();
    return 0;
}
```

### Dry Run:
- `setWheels(4)` sets `wheels` to 4.
- `showWheels()` prints: `This vehicle has 4 wheels.`
- `drive()` prints: `Driving a car with 4 wheels!`

**Output:**
```
This vehicle has 4 wheels.
Driving a car with 4 wheels!
```

---

# 7. Example Code 3:

```cpp
#include<iostream>
using namespace std;

// Base class
class Person {
protected:
    string name;
public:
    void setName(string n) {
        name = n;
    }
    void introduce() {
        cout << "Hello, my name is " << name << endl;
    }
};

// Derived class
class Student : public Person {
public:
    void study() {
        cout << name << " is studying OOP." << endl;
    }
};

int main() {
    Student s1;
    s1.setName("Alice");
    s1.introduce();
    s1.study();
    return 0;
}
```

### Dry Run:
- `setName("Alice")` sets `name` to "Alice".
- `introduce()` prints: `Hello, my name is Alice`
- `study()` prints: `Alice is studying OOP.`

**Output:**
```
Hello, my name is Alice
Alice is studying OOP.
```

---

# 8. Example Code 4:

```cpp
#include<iostream>
using namespace std;

// Base class
class Shape {
protected:
    string color;
public:
    void setColor(string c) {
        color = c;
    }
    void showColor() {
        cout << "Shape color: " << color << endl;
    }
};

// Derived class
class Circle : public Shape {
public:
    void draw() {
        cout << "Drawing a " << color << " circle." << endl;
    }
};

int main() {
    Circle cir1;
    cir1.setColor("Red");
    cir1.showColor();
    cir1.draw();
    return 0;
}
```

### Dry Run:
- `setColor("Red")` sets `color` to "Red".
- `showColor()` prints: `Shape color: Red`
- `draw()` prints: `Drawing a Red circle.`

**Output:**
```
Shape color: Red
Drawing a Red circle.
```

---

# 9. Example Code 5: 

```cpp
#include<iostream>
using namespace std;

// Base class
class Employee {
protected:
    string name;
    int id;
public:
    Employee(string n, int i) {
        name = n;
        id = i;
    }
    void showInfo() {
        cout << "Employee: " << name << ", ID: " << id << endl;
    }
};

// Derived class
class Manager : public Employee {
private:
    int teamSize;
public:
    Manager(string n, int i, int t) : Employee(n, i) {
        teamSize = t;
    }
    void display() {
        showInfo();
        cout << "Manages a team of " << teamSize << " members." << endl;
    }
};

int main() {
    Manager m1("John", 101, 5);
    m1.display();
    return 0;
}
```

### Dry Run:
- `Employee("John", 101)` initializes name as "John" and id as 101.
- `Manager("John", 101, 5)` initializes `teamSize` as 5.
- `display()` calls `showInfo()` and prints employee info and team size.

**Output:**
```
Employee: John, ID: 101
Manages a team of 5 members.
```

---

# 10. Example Code 6: 

```cpp
#include<iostream>
using namespace std;

// Base class
class Appliance {
protected:
    string brand;
public:
    Appliance(string b) {
        brand = b;
    }
    void showBrand() {
        cout << "Brand: " << brand << endl;
    }
};

// Derived class
class WashingMachine : public Appliance {
private:
    int capacity;
public:
    WashingMachine(string b, int c) : Appliance(b) {
        capacity = c;
    }
    void showDetails() {
        showBrand();
        cout << "Capacity: " << capacity << " kg" << endl;
    }
};

int main() {
    WashingMachine wm("Samsung", 7);
    wm.showDetails();
    return 0;
}
```

### Dry Run:
- `Appliance("Samsung")` initializes brand as "Samsung".
- `WashingMachine("Samsung", 7)` sets `capacity` to 7 kg.
- `showDetails()` prints brand and capacity.

**Output:**
```
Brand: Samsung
Capacity: 7 kg
```

---

# 11. Important Points to Remember 

- **Protected** members are **hidden** from the outside world but **accessible** in the child class.
- **Public inheritance** keeps things public and protected as they are.
- Inheritance helps to **reuse** code and **extend** functionalities easily.

---

#  Your Tasks:

1. Create another class called **Cat** which inherits from **Animal**.
2. Create a **Bike** class that inherits from **Vehicle** and shows its wheels.
3. Create a **Teacher** class that inherits from **Person**.


---

# Small Diagram to Understand Inheritance:

```
      Animal (Base Class)
         |
       public
         |
        Dog (Derived Class)
```

