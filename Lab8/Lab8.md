
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

## 🔧 Binary and Comparison Operator Overloading in C++

### 2. Overloading `-` (Subtraction)
```cpp
#include <iostream>
using namespace std;

class Balance {
    int amount;

public:
    Balance(int a) : amount(a) {}

    Balance operator-(Balance b) {
        return Balance(amount - b.amount);
    }

    void show() { cout << "Balance: " << amount << endl; }
};

int main() {
    Balance b1(100), b2(40), b3(0);
    b3 = b1 - b2;
    b3.show(); // Output: Balance: 60
    return 0;
}
```
🧠 **Dry Run:**
- `b1 = 100`, `b2 = 40`
- `b3 = b1 - b2` → `100 - 40 = 60`
- Shows: `Balance: 60`

---

### 3. Overloading `*` (Multiplication)
```cpp
#include <iostream>
using namespace std;

class Box {
    int volume;

public:
    Box(int v) : volume(v) {}

    Box operator*(Box b) {
        return Box(volume * b.volume);
    }

    void show() { cout << "Volume: " << volume << endl; }
};

int main() {
    Box b1(2), b2(3), b3(0);
    b3 = b1 * b2;
    b3.show(); // Output: Volume: 6
    return 0;
}
```
🧠 **Dry Run:**
- `b1 = 2`, `b2 = 3`
- `b3 = b1 * b2` → `2 * 3 = 6`
- Output: `Volume: 6`

---

### 4. Overloading `/` (Division)
```cpp
#include <iostream>
using namespace std;

class Score {
    int points;

public:
    Score(int p) : points(p) {}

    Score operator/(Score s) {
        return Score(points / s.points);
    }

    void show() { cout << "Score: " << points << endl; }
};

int main() {
    Score s1(20), s2(4), s3(0);
    s3 = s1 / s2;
    s3.show(); // Output: Score: 5
    return 0;
}
```
🧠 **Dry Run:**
- `s1 = 20`, `s2 = 4`
- `s3 = s1 / s2` → `20 / 4 = 5`
- Output: `Score: 5`

---

### 5. Overloading `%` (Modulo)
```cpp
#include <iostream>
using namespace std;

class Modulo {
    int num;

public:
    Modulo(int n) : num(n) {}

    Modulo operator%(Modulo m) {
        return Modulo(num % m.num);
    }

    void show() { cout << "Remainder: " << num << endl; }
};

int main() {
    Modulo m1(10), m2(3), m3(0);
    m3 = m1 % m2;
    m3.show(); // Output: Remainder: 1
    return 0;
}
```
🧠 **Dry Run:**
- `m1 = 10`, `m2 = 3`
- `m3 = m1 % m2` → `10 % 3 = 1`
- Output: `Remainder: 1`

---

### 6. Overloading `=` (Assignment - Custom Copy)
```cpp
#include <iostream>
using namespace std;

class Book {
    int pages;

public:
    Book(int p = 0) : pages(p) {}

    Book& operator=(const Book& b) {
        pages = b.pages;
        return *this;
    }

    void show() { cout << "Pages: " << pages << endl; }
};

int main() {
    Book b1(100), b2;
    b2 = b1;
    b2.show(); // Output: Pages: 100
    return 0;
}
```
🧠 **Dry Run:**
- `b1 = Book(100)`
- `b2 = b1;` → `b2.pages = b1.pages`
- Output: `Pages: 100`

---



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



### 1. Overloading `==` (Equal To)
```cpp
#include <iostream>
using namespace std;

class Coin {
    int value;

public:
    Coin(int v) : value(v) {}

    bool operator==(Coin c) {
        return value == c.value;
    }
};

int main() {
    Coin c1(5), c2(5);
    if (c1 == c2)
        cout << "Coins are equal" << endl;
    else
        cout << "Coins are not equal" << endl;
    return 0;
}
```
🧠 **Dry Run:** `5 == 5` → `true`

---

### 2. Overloading `!=` (Not Equal To)
```cpp
#include <iostream>
using namespace std;

class Coin {
    int value;

public:
    Coin(int v) : value(v) {}

    bool operator!=(Coin c) {
        return value != c.value;
    }
};

int main() {
    Coin c1(10), c2(5);
    if (c1 != c2)
        cout << "Coins are not equal" << endl;
    else
        cout << "Coins are equal" << endl;
    return 0;
}
```
🧠 **Dry Run:** `10 != 5` → `true`

---

### 3. Overloading `>` (Greater Than)
```cpp
#include <iostream>
using namespace std;

class Height {
    int cm;

public:
    Height(int c) : cm(c) {}

    bool operator>(Height h) {
        return cm > h.cm;
    }
};

int main() {
    Height h1(180), h2(170);
    if (h1 > h2)
        cout << "h1 is taller" << endl;
    else
        cout << "h2 is taller or equal" << endl;
    return 0;
}
```
🧠 **Dry Run:** `180 > 170` → `true`

---

### 4. Overloading `<` (Less Than)
```cpp
#include <iostream>
using namespace std;

class Weight {
    int kg;

public:
    Weight(int k) : kg(k) {}

    bool operator<(Weight w) {
        return kg < w.kg;
    }
};

int main() {
    Weight w1(40), w2(60);
    if (w1 < w2)
        cout << "w1 is lighter" << endl;
    else
        cout << "w2 is lighter or equal" << endl;
    return 0;
}
```
🧠 **Dry Run:** `40 < 60` → `true`

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
