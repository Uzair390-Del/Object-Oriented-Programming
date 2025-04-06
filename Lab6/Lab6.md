# Week 6: # OOP Lab - C++ -- Const/Volatile, Object Passing, and Arrays of Objects

## Lab Objectives
This lab will help you understand and implement:
1. Constant and volatile member functions
2. Passing objects to functions
3. Returning objects from functions
4. Arrays of objects

---
### 🔹 Constant Member Functions
- Declared using the `const` keyword after the function definition.
- These functions **cannot modify any data members** of the class.
- They are **read-only** functions and can only access constant data.

### 🔸 Syntax
```cpp
class A {
    int x;
public:
    void show() const;  // This function cannot modify x
};
```

### 🔸 Example
```cpp
#include <iostream>
using namespace std;

class Sample {
    int value;
public:
    Sample(int v) { value = v; }

    void show() const {
        // value++;  ❌ Not allowed
        cout << "Value is: " << value << endl;
    }
};

int main() {
    Sample s(10);
    s.show();
    return 0;
}
```

### 🔸 Output
```
Value is: 10
```

---

### 🔹 Volatile Keyword
- Used for variables that **can be changed unexpectedly**, like **hardware registers** or **interrupts**.
- Prevents the compiler from **optimizing** code that assumes the value remains unchanged.
  
### 🔸 Syntax
```cpp
volatile int temp;
```

> ⚠️ Note: `volatile` is mostly used in embedded systems programming.

---

- **const functions**: Member functions that promise not to modify the object's state
- **volatile functions**: Member functions for objects that may change unexpectedly (e.g., hardware registers)
- **mutable members**: Data members that can be modified even in const functions

### Example Code: Sensor Class
```cpp
#include <iostream>
using namespace std;

class Sensor {
    mutable int readCount;  // Can be modified in const functions
    int value;
    
public:
    Sensor() : readCount(0), value(0) {}
    
    void simulateReading() {
        value = rand() % 100;  // Simulate sensor reading
    }
    
    // Constant member function
    int getValue() const {
        readCount++;
        return value;
    }
    
    // Volatile member function
    void volatileUpdate() volatile {
        value = rand() % 100;
    }
};

int main() {
    Sensor normalSensor;
    const Sensor constSensor;
    volatile Sensor volatileSensor;
    
    normalSensor.simulateReading();
    cout << "Normal sensor: " << normalSensor.getValue() << endl;
    
    // constSensor.simulateReading(); // Error - const object
    cout << "Const sensor: " << constSensor.getValue() << endl;
    
    volatileSensor.volatileUpdate();
    // cout << volatileSensor.getValue(); // Needs const volatile version
    
    return 0;
}
```

### Dry Run Explanation
**Object Creation:**

- `normalSensor`: Regular object
- `constSensor`: Constant object (can't be modified)
- `volatileSensor`: Volatile object (may change unexpectedly)

**normalSensor Operations:**

- `simulateReading()`: Sets value to random number (e.g., 42)
- `getValue()`: Returns 42 and increments readCount to 1

**constSensor Operations:**

- Can only call const member functions
- `getValue()`: Returns 0 (default) and increments readCount to 1

**volatileSensor Operations:**

- `volatileUpdate()`: Changes value to new random number (e.g., 75)
- Regular `getValue()` can't be called (needs volatile version)

**Key Points**
- Const objects can only call const member functions
- Volatile objects need volatile member functions
- Mutable members can be modified even in const functions

---

## 2. Passing and Returning Objects

### Example Code: Matrix Operations
```cpp
#include <iostream>
using namespace std;

class Matrix {
    int data[2][2];
    
public:
    void fill() {
        cout << "Enter 4 elements:\n";
        for(int i=0; i<2; i++)
            for(int j=0; j<2; j++)
                cin >> data[i][j];
    }
    
    void display() const {
        for(int i=0; i<2; i++) {
            for(int j=0; j<2; j++)
                cout << data[i][j] << " ";
            cout << endl;
        }
    }
    
    // Pass by reference
    Matrix add(const Matrix& m) {
        Matrix result;
        for(int i=0; i<2; i++)
            for(int j=0; j<2; j++)
                result.data[i][j] = data[i][j] + m.data[i][j];
        return result;  // Return by value
    }
};

int main() {
    Matrix m1, m2;
    m1.fill();  // Assume user enters: 1 2 3 4
    m2.fill();  // Assume user enters: 5 6 7 8
    
    Matrix sum = m1.add(m2);
    cout << "Sum matrix:\n";
    sum.display();
    
    return 0;
}
```

### Dry Run Explanation
**Matrix Input:**

- `m1` becomes: [1 2; 3 4]
- `m2` becomes: [5 6; 7 8]

**Addition Operation:**

- `m1.add(m2)` creates a temporary result matrix
- Element-wise addition:
  - result[0][0] = 1 + 5 = 6
  - result[0][1] = 2 + 6 = 8
  - result[1][0] = 3 + 7 = 10
  - result[1][1] = 4 + 8 = 12

**Output:**
```
Sum matrix:
6 8 
10 12
```

**Key Points**
- Passing by reference avoids object copying
- Returning by value creates a copy (consider move semantics for optimization)
- Const reference prevents modification of passed object

---

## 3. Arrays of Objects

### Example Code: Student Database
```cpp
#include <iostream>
#include <string>
using namespace std;

class Student {
    string name;
    float gpa;
    
public:
    void setData(const string& n, float g) {
        name = n;
        gpa = g;
    }
    
    void display() const {
        cout << "Name: " << name << ", GPA: " << gpa << endl;
    }
    
    float getGPA() const { return gpa; }
};

int main() {
    const int SIZE = 3;
    Student class2023[SIZE];
    
    for(int i=0; i<SIZE; i++) {
        string name;
        float gpa;
        cout << "Enter name and GPA for student " << i+1 << ": ";
        cin >> name >> gpa;
        class2023[i].setData(name, gpa);
    }
    
    int topIndex = 0;
    for(int i=1; i<SIZE; i++) {
        if(class2023[i].getGPA() > class2023[topIndex].getGPA()) {
            topIndex = i;
        }
    }
    
    cout << "\nTop student:\n";
    class2023[topIndex].display();
    
    return 0;
}
```

### Dry Run Explanation
**Array Initialization:**

- Creates array of 3 Student objects

**Data Input:**

- `class2023[0]`: Name="Alice", GPA=3.8
- `class2023[1]`: Name="Bob", GPA=3.5
- `class2023[2]`: Name="Charlie", GPA=3.9

**Finding Top Student:**

- Initial topIndex = 0 (Alice, 3.8)
- Compare with Bob (3.5) → no change
- Compare with Charlie (3.9) → topIndex becomes 2

**Output:**
```
Top student:
Name: Charlie, GPA: 3.9
```

**Key Points**
- Arrays store objects contiguously in memory
- Can initialize using constructors
- Useful for managing collections of related objects

---

## Lab Exercises

### Exercise 1: Const/Volatile
Create a `SecureData` class that:
- Stores sensitive data (e.g., password)
- Has constant methods for validation
- Has volatile methods for secure wipe
- Demonstrate usage with const and volatile objects

**Sample Solution Approach:**
- Create class with private string member for data
- Implement `validate()` as const member function
- Implement `secureWipe()` as volatile function
- Demonstrate with const and volatile objects

### Exercise 2: Object Passing
Create a `ComplexNumber` class with:
- Methods to add/subtract (passing objects by reference)
- Method to multiply (returning new object)
- Demonstrate all operations

**Sample Solution Approach:**
- Class with real and imaginary parts
- `add()` and `subtract()` taking const references
- `multiply()` returning new ComplexNumber
- Show all operations in `main()`

### Exercise 3: Array of Objects
Create a `Book` class and:
- Create array of 5 Book objects
- Implement functions to:
  - Find books by author
  - Calculate average price
  - Display all books sorted by price

**Sample Solution Approach:**
- Book class with title, author, price
- Create and populate array
- Write functions for required operations
- Demonstrate all functionality

---

## Conclusion
This lab covered essential OOP concepts in C++:
- `const`/`volatile` for object access control
- Object passing (by value, reference, const reference)
- Returning objects from functions
- Arrays of objects for collection management
