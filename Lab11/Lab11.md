# Lab:

This lab covers the following important OOP concepts in C++:

* Multilevel Inheritance
* Hierarchical Inheritance
* Hybrid Inheritance
* Pointers
* Pointer to Objects
* `this` Pointer
* Pointer to Derived Class

---

## 1. Multilevel Inheritance

### What:

When a class is derived from a class, and then another class is derived from that derived class, it’s called multilevel inheritance. It’s like a family where a grandfather has a son, and the son has a son (grandchild).

### Why:

To reuse and build upon previously written classes.

### How:

A -> B -> C (A is base, B derived from A, C derived from B)

### Simple Example:

```cpp
#include<iostream>
using namespace std;

class Animal {
public:
    void eat() {
        cout << "Eating...\n";
    }
};

class Dog : public Animal {
public:
    void bark() {
        cout << "Barking...\n";
    }
};

class Puppy : public Dog {
public:
    void weep() {
        cout << "Weeping...\n";
    }
};

int main() {
    Puppy p;
    p.eat();    // from Animal
    p.bark();   // from Dog
    p.weep();   // from Puppy
    return 0;
}
```

### Dry Run:

* `p.eat()` prints "Eating..."
* `p.bark()` prints "Barking..."
* `p.weep()` prints "Weeping..."

### Example :

```cpp
class Person {
protected:
    string name;
public:
    void setName(string n) {
        name = n;
    }
};

class Student : public Person {
protected:
    int roll;
public:
    void setRoll(int r) {
        roll = r;
    }
};

class Result : public Student {
private:
    int marks;
public:
    void setMarks(int m) {
        marks = m;
    }
    void show() {
        cout << "Name: " << name << ", Roll: " << roll << ", Marks: " << marks << endl;
    }
};

int main() {
    Result r;
    r.setName("Ali");
    r.setRoll(101);
    r.setMarks(95);
    r.show();
    return 0;
}
```

### Dry Run:

* `setName("Ali")` sets `name = "Ali"`
* `setRoll(101)` sets `roll = 101`
* `setMarks(95)` sets `marks = 95`
* `show()` prints: Name: Ali, Roll: 101, Marks: 95

---

## 2. Hierarchical Inheritance

### What:

One base class has multiple derived classes.

### Why:

Common properties in one base class and different behaviors in multiple derived classes.

### How:

A -> B and A -> C

### Simple Example:

```cpp
class Animal {
public:
    void eat() {
        cout << "Eating...\n";
    }
};

class Dog : public Animal {
public:
    void bark() {
        cout << "Barking...\n";
    }
};

class Cat : public Animal {
public:
    void meow() {
        cout << "Meowing...\n";
    }
};

int main() {
    Dog d;
    d.eat(); d.bark();
    Cat c;
    c.eat(); c.meow();
    return 0;
}
```

### Dry Run:

* `Dog` object calls `eat` and `bark`
* `Cat` object calls `eat` and `meow`

###  Example :

```cpp
class Employee {
protected:
    string name;
    int id;
public:
    void setData(string n, int i) {
        name = n;
        id = i;
    }
};

class Manager : private Employee {
private:
    int teamSize;
public:
    void setManager(string n, int i, int t) {
        setData(n, i);  // allowed since it's private inheritance
        teamSize = t;
    }
    void show() {
        cout << "Manager: " << name << ", ID: " << id << ", Team: " << teamSize << endl;
    }
};

class Developer : protected Employee {
private:
    string language;
public:
    void setDev(string n, int i, string lang) {
        setData(n, i);
        language = lang;
    }
    void show() {
        cout << "Developer: " << name << ", ID: " << id << ", Lang: " << language << endl;
    }
};

int main() {
    Manager m;
    m.setManager("Adeel", 1, 5);
    m.show();

    Developer d;
    d.setDev("Sara", 2, "C++");
    d.show();
    return 0;
}
```

### Dry Run:

* Manager sets name="Adeel", id=1, teamSize=5 → outputs all details
* Developer sets name="Sara", id=2, language="C++" → outputs all details

---


# 3. Hybrid Inheritance

**What:**  
A combination of more than one type of inheritance (like hierarchical + multilevel) is called hybrid inheritance.

**Why:**  
To combine features of multiple base classes and create flexible and powerful class designs.

**How:**  
A base class is inherited in two different paths, eventually merging in a derived class.

**Simple Example:**
```cpp
#include<iostream>
using namespace std;

class A {
public:
    void displayA() {
        cout << "Class A\n";
    }
};

class B : public A {
public:
    void displayB() {
        cout << "Class B\n";
    }
};

class C : public A {
public:
    void displayC() {
        cout << "Class C\n";
    }
};

class D : public B, public C {
public:
    void displayD() {
        cout << "Class D\n";
    }
};

int main() {
    D obj;
    obj.displayB();
    obj.displayC();
    obj.displayD();
    // obj.displayA();  // Ambiguous
    obj.B::displayA(); // Resolving ambiguity
    return 0;
}
```

**Dry Run:**  
- Calls from B, C, D work directly.  
- `displayA()` causes ambiguity since both B and C inherit A.  
- Use `obj.B::displayA()` to resolve ambiguity.

**Important Note:**  
To avoid ambiguity in hybrid inheritance, virtual inheritance can be used (covered in advanced topics).

---

# 4. Pointers in C++

**What:**  
A pointer is a variable that stores the address of another variable.

**Why:**  
Used for dynamic memory, arrays, and especially for managing objects in OOP.

**How:**  
Declared using `*` and initialized using `&`.

**Example:**
```cpp
int x = 10;
int* p = &x;
cout << *p; // prints 10
```

---

# 5. Pointer to Objects

**What:**  
A pointer can point to an object, just like it points to a variable.

**Why:**  
Used in dynamic object creation and passing objects efficiently.

**Example:**
```cpp
class Demo {
public:
    void show() {
        cout << "Hello from object pointer\n";
    }
};

int main() {
    Demo d;
    Demo* ptr = &d;
    ptr->show(); // using -> to access members
    return 0;
}
```

**Dry Run:**  
- `ptr` holds address of object `d`.  
- `ptr->show()` calls the function of `d`.

---

# 6. this Pointer

**What:**  
`this` is an implicit pointer that points to the current object.

**Why:**  
Helps resolve conflicts when local variable name hides a class member.

**Example:**
```cpp
class Demo {
private:
    int x;
public:
    void setX(int x) {
        this->x = x; // Resolves conflict
    }
    void show() {
        cout << "Value: " << x << endl;
    }
};

int main() {
    Demo d;
    d.setX(5);
    d.show(); // prints Value: 5
    return 0;
}
```

**Dry Run:**  
`setX(5)` assigns 5 to class member using `this->x`.

---

# 7. Pointer to Derived Class

**What:**  
A base class pointer can point to a derived class object.

**Why:**  
Used in polymorphism, especially for dynamic function calls (virtual functions).

**Example:**
```cpp
class Base {
public:
    void show() {
        cout << "Base class\n";
    }
};

class Derived : public Base {
public:
    void show() {
        cout << "Derived class\n";
    }
};

int main() {
    Base* ptr;
    Derived d;
    ptr = &d;
    ptr->show(); // prints Base class (not derived)
    return 0;
}
```

**Dry Run:**  
- `ptr` points to `d`, but since `show()` is not virtual, base version is called.

**With virtual:**
```cpp
class Base {
public:
    virtual void show() {
        cout << "Base class\n";
    }
};

class Derived : public Base {
public:
    void show() override {
        cout << "Derived class\n";
    }
};

int main() {
    Base* ptr;
    Derived d;
    ptr = &d;
    ptr->show(); // prints Derived class
    return 0;
}
```

---

# Practice Tasks

1. Create a multilevel inheritance example with `Vehicle → Car → SportsCar`. Add attributes in each and print them.
2. Build a hierarchical inheritance for `Shape → Rectangle` and `Shape → Circle`. Include area calculation in each.
3. Write a program using a pointer to an object. Create a class `Book` and print its title and price using a pointer.
4. Use `this` pointer to differentiate between local and member variables with the same name.
5. Write a base class `Person` and a derived class `Teacher`. Use a base class pointer to point to `Teacher` and call a virtual function `display()`.

