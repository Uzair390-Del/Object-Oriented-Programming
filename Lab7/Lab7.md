# Lab: Operator Overloading and Unary Operator Overloading in C++

## Objective:
## Lab Objectives
This lab will help you understand and implement:
1. operator overloading
2. unary operator overloading in C++.


---

## 1. What is Operator Overloading?

**Operator Overloading** allows you to redefine the way operators work for user-defined types (like classes). Instead of only using operators with built-in types, you can make them work with your own custom classes.

### Example Use Case:
If you have a class `Box`, and you want to add two boxes using `box1 + box2`, operator overloading allows that.

---

## 2. Why Do We Need Operator Overloading?
- It makes objects behave like primitive types.
- Makes code more readable and natural.
- Helpful when creating mathematical or logical classes (like complex numbers, vectors, etc.).

---

## 3. Syntax of Operator Overloading
```cpp
return_type operator op (argument_list) {
    // code
}
```
Where `op` is the operator you want to overload.

---

## 4. Unary Operator Overloading
Unary operators work with **only one operand**. Examples:
- `-` (negation)
- `++` (increment)
- `--` (decrement)
- `!` (logical NOT)
- `~` (bitwise NOT)

---

## 5. Example: Overloading Unary `-` Operator

### Code:
```cpp
#include <iostream>
using namespace std;

class Number {
    int value;

public:
    Number(int v) : value(v) {}

    Number operator-() {
        return Number(-value);
    }

    void display() {
        cout << "Value: " << value << endl;
    }
};

int main() {
    Number n1(10);
    Number n2 = -n1;
    n2.display(); // Output: Value: -10
    return 0;
}
```

### Dry Run:
- `n1` has value `10`
- `-n1` calls the overloaded operator and returns a new Number with value `-10`

---

## 6. Example: Overloading Prefix `++` Operator

### Code:
```cpp
class Counter {
    int value;

public:
    Counter(int v = 0) : value(v) {}

    Counter operator++() {
        ++value;
        return *this;
    }

    void display() {
        cout << "Value: " << value << endl;
    }
};

int main() {
    Counter c(5);
    ++c;
    c.display(); // Output: Value: 6
    return 0;
}
```

### Dry Run:
- `c` starts at `5`
- `++c` increments it to `6`

---

## 7. Example: Overloading Postfix `++` Operator

### Code:
```cpp
class Counter {
    int value;

public:
    Counter(int v = 0) : value(v) {}

    Counter operator++(int) {
        Counter temp = *this;
        value++;
        return temp;
    }

    void display() {
        cout << "Value: " << value << endl;
    }
};

int main() {
    Counter c(5);
    c++;
    c.display(); // Output: Value: 6
    return 0;
}
```

### Dry Run:
- `c` starts at `5`
- `c++` saves `5`, then increments to `6`

---

## 8. Overloading Logical NOT `!` Operator

### Code:
```cpp
class Light {
    bool isOn;

public:
    Light(bool status) : isOn(status) {}

    bool operator!() {
        return !isOn;
    }

    void display() {
        cout << (isOn ? "Light is ON" : "Light is OFF") << endl;
    }
};

int main() {
    Light bulb(true);
    bulb.display();            // Output: Light is ON
    cout << !bulb << endl;     // Output: 0 (false)
    return 0;
}
```

---

## 9. Overloading Bitwise NOT `~` Operator

### Code:
```cpp
class BitNumber {
    int value;

public:
    BitNumber(int v) : value(v) {}

    BitNumber operator~() {
        return BitNumber(~value);
    }

    void display() {
        cout << "Value: " << value << endl;
    }
};

int main() {
    BitNumber b(5);  // binary: 0101
    BitNumber flipped = ~b;
    flipped.display();  // Output: Value: -6
    return 0;
}
```

---

## 10. Practice Exercises for Students

1. Create a class `Distance` that stores distance in meters and overload `+` to add two distances.
2. Create a class `Temperature` and overload unary `-` to convert from positive to negative temperature.
3. Implement both prefix and postfix `--` operator for a `Counter` class.

---

## 11. Conclusion
Operator overloading makes our custom types behave like built-in types. Unary operator overloading helps define behavior for operations on a single object. With this power, we can make our code cleaner, intuitive, and easier to read!

> Happy Coding! 😊

