# Lab 1: Introduction to C++ and Object-Oriented Programming (OOP)

## **1. Basic C++ Programs**
Before diving into OOP, let's assess your understanding of fundamental C++ concepts. Complete the following tasks:

### **Task 1: Hello World Program**
Write a C++ program that prints `"Hello, World!"` on the screen.

### **Task 2: Simple Calculator**
Write a program that takes **two numbers** as input and performs **addition, subtraction, multiplication, and division**.

### **Task 3: Even or Odd Number Checker**
Write a program that takes an integer as input and checks if it is **even** or **odd** using an `if-else` statement.

### **Task 4: Sum of First N Natural Numbers (Using Loops)**
Write a program that uses a **for loop** to find the sum of the first `N` natural numbers.

### **Task 5: Find the Largest Number (Using If-Else)**
Write a program that takes three numbers as input and prints the **largest number** among them.

### **Task 6:**
Write a C++ program that implements a **simple calculator** using **functions** and a **switch-case statement**. The calculator should perform the following operations:

- **Addition (`+`)**
- **Subtraction (`-`)**
- **Multiplication (`*`)**
- **Division (`/`)**

## Requirements
Your program should:

1. Take two numbers as input from the user.
2. Ask the user to choose an operation (`+`, `-`, `*`, `/`).
3. Use a **switch-case** to handle the operation.
4. Implement each operation inside a **separate function**.
5. Display the result after performing the operation.
6. Handle division by zero appropriately.

## Expected Learning Outcomes
By completing this task, students will:
- Understand the use of **functions** in C++.
- Learn how to use **switch-case** statements.
- Gain experience in handling **user input** and **basic arithmetic operations**.
- Implement **error handling** (e.g., division by zero).

## **2. Introduction to Object-Oriented Programming (OOP)**

### **Why Do We Need OOP?**
- Traditional programming (**procedural programming**) works fine for small programs, but as complexity increases, it becomes harder to manage.
- Code **reusability, maintenance, and scalability** become difficult in procedural programming.
- OOP helps in organizing code efficiently by using **objects and classes**, making it **modular, reusable, and easy to debug**.

### **Basic Idea of OOP**
- **Objects**: Real-world entities (e.g., Car, Person, Animal)
- **Classes**: Blueprint/template for creating objects
- **Encapsulation**: Wrapping data and functions together
- **Abstraction**: Hiding implementation details and showing only the necessary parts
- **Inheritance**: Reusing properties and behaviors from another class
- **Polymorphism**: One function behaving differently in different contexts

### **Example to Explain OOP**
#### **Real-world Example: A Car 🚗**
- The **Car** has attributes: **brand, color, speed** (data members).
- The **Car** has behaviors: **start(), accelerate(), brake()** (functions).

#### **Example Code in C++**
```cpp
#include <iostream>
using namespace std;

class Car {
public:
    string brand;
    string color;
    int speed;

    void start() {
        cout << brand << " is starting." << endl;
    }

    void accelerate() {
        cout << brand << " is accelerating." << endl;
    }
};

int main() {
    Car car1; // Creating an object of Car class
    car1.brand = "Toyota";
    car1.color = "Red";
    car1.speed = 120;

    car1.start();
    car1.accelerate();

    return 0;
}
```

### **Explanation:**
- `class Car {}` → Defines a class named `Car`.
- `brand, color, speed` → Attributes (Data Members).
- `start(), accelerate()` → Functions (Methods).
- `car1` → Object created from `Car` class.

### **Key Takeaways**
- OOP organizes code efficiently.
- Classes help structure programs based on real-world objects.
- Objects are instances of classes with unique attributes and behaviors.

---

## **Lab Task for Students**
💡 **Write a simple class `Student` with attributes `name`, `age`, and a function `displayDetails()`**.
- Create an object of `Student` and display its details.

This lab will help you understand the basics of **C++ fundamentals** and introduce you to **OOP concepts**.
