
# 🧪 Lab: Operator Overloading in C++ (Binary and Comparison Operators)

## 🔍 Objective
In this lab, you’ll learn:

- What is operator overloading in C++?
- How to overload binary operators like `+` and `-`
- How to overload comparison operators like `==`, `!=`, `<`, and `>`
- Dry runs and simple examples for each operator
- Step-by-step explanation like you’re learning magic tricks! 🪄

## ✨ What is Operator Overloading?
Operator overloading means giving new meaning to an operator (like `+`, `==`) when used with user-defined data types (like a class or object).

Think of it as teaching a robot how to understand new rules. For example:

> If you say "add these two persons", the robot doesn’t know what that means. You have to teach it how to do that.

## 📌 Part 1: Binary Operator Overloading

### 🚀 Example: Overloading the `+` operator for a class `Distance`
```cpp
#include <iostream>
using namespace std;

class Distance {
    int meters;

public:
    Distance() : meters(0) {}
    Distance(int m) : meters(m) {}

    // Binary operator overloading
    Distance operator+(Distance d) {
        Distance temp;
        temp.meters = meters + d.meters;
        return temp;
    }

    void display() {
        cout << "Distance: " << meters << " meters" << endl;
    }
};

int main() {
    Distance d1(5), d2(10), d3;

    d3 = d1 + d2;  // We are using overloaded + here
    d3.display();  // Should show: Distance: 15 meters

    return 0;
}
```

### 🧠 Dry Run (Step-by-Step)
- `d1` is 5 meters.
- `d2` is 10 meters.
- `d3 = d1 + d2;`
- Calls the `operator+` function.
- Adds `d1.meters (5)` + `d2.meters (10)` = 15.
- Returns a new `Distance` object with 15 meters.
- `d3.display()` shows: `Distance: 15 meters`

## 📌 Part 2: Comparison Operator Overloading

### 🚀 Example: Overloading the `==` operator for class `Box`
```cpp
#include <iostream>
using namespace std;

class Box {
    int length;

public:
    Box(int l) : length(l) {}

    // Comparison operator overloading
    bool operator==(Box b) {
        return length == b.length;
    }
};

int main() {
    Box b1(10), b2(10), b3(5);

    if (b1 == b2)
        cout << "b1 and b2 are equal." << endl;
    else
        cout << "b1 and b2 are not equal." << endl;

    if (b1 == b3)
        cout << "b1 and b3 are equal." << endl;
    else
        cout << "b1 and b3 are not equal." << endl;

    return 0;
}
```

### 🧠 Dry Run (Step-by-Step)
- `b1` and `b2` both have length 10 → `b1 == b2` is true
- `b3` has length 5 → `b1 == b3` is false

### 🧠 Easy Explanation
Imagine two boxes: if they are the same size (same length), we say they are equal.

If they’re different sizes, we say they’re not equal.

With comparison operator overloading, we teach C++ how to check "same size" for our custom class.

## 📚 Lab Tasks

**Task 1:**  
Create a class `ComplexNumber` and overload the `+` operator to add two complex numbers.

**Task 2:**  
Create a class `Student` with a `marks` attribute and overload the `>` operator to compare which student has higher marks.

## ✅ Conclusion
By the end of this lab, you now:

- Know how to make your own meaning of operators (`+`, `==`, `>`, etc.)
- Understand how to overload binary and comparison operators in C++
- Can explain it to your friends like a pro 😎
