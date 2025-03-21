# Week 4: C++ Lab - Member Functions, Constructors, and Destructors

## Objectives
In this lab, students will learn:
- Defining Member Functions inside and outside the class.
- Understanding and implementing Constructors and Destructors.
- Why we need Constructors and Destructors.
- Why we define functions outside the class.
- Hands-on practice with structured tasks.

---

## **1. Defining Member Functions in C++**

### **Inside the Class**
Member functions can be defined within the class definition itself.

**Example:**
```cpp
#include <iostream>
using namespace std;

class Rectangle {
public:
    int length, width;
    
    void setValues(int l, int w) {  // Defined inside the class
        length = l;
        width = w;
    }
    
    int area() {  // Defined inside the class
        return length * width;
    }
};

int main() {
    Rectangle rect;
    rect.setValues(10, 5);
    cout << "Area: " << rect.area() << endl;
    return 0;
}
```

### **Outside the Class**
Defining functions outside the class improves code readability and reduces clutter within the class definition. This is done using the scope resolution operator `::`.

**Example:**
```cpp
#include <iostream>
using namespace std;

class Rectangle {
public:
    int length, width;
    void setValues(int, int);
    int area();
};

void Rectangle::setValues(int l, int w) {  // Defined outside the class
    length = l;
    width = w;
}

int Rectangle::area() {  // Defined outside the class
    return length * width;
}

int main() {
    Rectangle rect;
    rect.setValues(10, 5);
    cout << "Area: " << rect.area() << endl;
    return 0;
}
```

### **Why Define Functions Outside the Class?**
- Keeps the class definition clean and readable.
- Improves maintainability by separating interface and implementation.
- Reduces compile-time dependencies when working with large projects.

---

## **2. Constructors in C++**
A constructor is a special member function that is automatically called when an object is created. It initializes object properties and helps avoid uninitialized values.

### **Types of Constructors**
#### **1. Default Constructor**
A constructor with no parameters, automatically invoked when an object is created.
```cpp
class Car {
public:
    string brand;
    Car() {  // Default Constructor
        brand = "Unknown";
    }
};
int main() {
    Car myCar;
    cout << "Car brand: " << myCar.brand << endl;
    return 0;
}
```

#### **2. Parameterized Constructor**
Allows passing arguments during object creation to initialize values.
```cpp
class Car {
public:
    string brand;
    Car(string b) {  // Parameterized Constructor
        brand = b;
    }
};
int main() {
    Car myCar("Toyota");
    cout << "Car brand: " << myCar.brand << endl;
    return 0;
}
```


#### **3. Copy Constructor**
Creates a new object as an exact copy of an existing object.
```cpp
class Car {
public:
    string brand;
    Car(string b) {
        brand = b;
    }
    Car(const Car &c) {  // Copy Constructor
        brand = c.brand;
    }
};
int main() {
    Car car1("Honda");
    Car car2 = car1;  // Calls Copy Constructor
    cout << "Car brand: " << car2.brand << endl;
    return 0;
}

```
Counter Example with Different Constructors
This example demonstrates a counter that increases its value upon creation.

## **4. Counter Example with Different Constructors**
This example demonstrates a counter that increases its value upon creation.

### **C++ Code Implementation**
```cpp
#include <iostream>
using namespace std;

class Counter {
    int count;
    
public:
    Counter() {  // Default Constructor
        count = 0;
        cout << "Counter initialized to 0" << endl;
    }

    Counter(int c) {  // Parameterized Constructor
        count = c;
        cout << "Counter initialized to " << count << endl;
    }

    Counter(const Counter &obj) {  // Copy Constructor
        count = obj.count;
        cout << "Counter copied with value " << count << endl;
    }
    ~Counter() {  // Destructor
        cout << "Counter with value " << count << " is destroyed" << endl;
    }
    void increment() {
        count++;
    }

    void display() {
        cout << "Current count: " << count << endl;
    }
};

int main() {
    Counter c1;          // Default constructor
    Counter c2(10);      // Parameterized constructor
    Counter c3 = c2;     // Copy constructor
    
    c1.increment();
    c2.increment();
    c3.increment();
    
    c1.display();
    c2.display();
    c3.display();
    
    return 0;
}
```
## Step-by-Step Explanation

1. **Counter c1;**
   - Calls the default constructor.
   - Sets `count` to `0`.
   - Displays: `"Counter initialized to 0"`.

2. **Counter c2(10);**
   - Calls the parameterized constructor.
   - Sets `count` to `10`.
   - Displays: `"Counter initialized to 10"`.

3. **Counter c3 = c2;**
   - Calls the copy constructor.
   - Copies `c2`'s `count` value (`10`) into `c3`.
   - Displays: `"Counter copied with value 10"`.

4. **c1.increment();**
   - Increases `c1.count` from `0` → `1`.

5. **c2.increment();**
   - Increases `c2.count` from `10` → `11`.

6. **c3.increment();**
   - Increases `c3.count` from `10` → `11`.

7. **display() function for each object prints:**
   - `"Current count: 1"` (for `c1`).
   - `"Current count: 11"` (for `c2`).
   - `"Current count: 11"` (for `c3`).

---

## Dry Run of the Program

| Step | Operation            | count (c1) | count (c2) | count (c3) | Output                              |
|------|----------------------|------------|------------|------------|-------------------------------------|
| 1    | Create `c1`          | 0          | -          | -          | `"Counter initialized to 0"`        |
| 2    | Create `c2(10)`      | 0          | 10         | -          | `"Counter initialized to 10"`       |
| 3    | Copy `c2` to `c3`    | 0          | 10         | 10         | `"Counter copied with value 10"`    |
| 4    | `c1.increment();`    | 1          | 10         | 10         | -                                   |
| 5    | `c2.increment();`    | 1          | 11         | 10         | -                                   |
| 6    | `c3.increment();`    | 1          | 11         | 11         | -                                   |
| 7    | `display()` output   | 1          | 11         | 11         | `"Current count: 1"`                |
|      |                      |            |            |            | `"Current count: 11"`               |
|      |                      |            |            |            | `"Current count: 11"`               |


### **Why Do We Need Constructors?**
- To ensure object initialization at the time of creation.
- To avoid uninitialized data members, which can lead to unpredictable behavior.
- To allow automatic object setup without requiring manual function calls.

---

## **3. Destructors in C++**
A destructor is a special function that is automatically invoked when an object goes out of scope. It is used to release resources allocated by the object.

### **Example:**
```cpp
class Car {
public:
    Car() {
        cout << "Car created" << endl;
    }
    ~Car() {  // Destructor
        cout << "Car destroyed" << endl;
    }
};

int main() {
    Car myCar;
    return 0;
}
```
## **Dynamic Allocation with Constructor and Destructor**
This example demonstrates dynamic memory allocation using a constructor and destructor in C++.

### **C++ Code Implementation**
```cpp
#include <iostream>
using namespace std;

class Car {
public:
    string brand;
    int *mileage;  // Pointer for dynamic allocation

    // Parameterized Constructor
    Car(string b, int m) {
        brand = b;
        mileage = new int(m);  // Dynamically allocate memory for mileage
        cout << "Constructor called for " << brand << " with mileage " << *mileage << endl;
    }

    // Destructor
    ~Car() {
        cout << "Destructor called for " << brand << " with mileage " << *mileage << endl;
        delete mileage;  // Free dynamically allocated memory
    }

    void display() {
        cout << "Car brand: " << brand << ", Mileage: " << *mileage << endl;
    }
};

int main() {
    Car myCar("Toyota", 15000);  // Parameterized constructor
    myCar.display();
    return 0;
}
```
## **Step-by-Step Explanation**

1. **Car myCar("Toyota", 15000);**
   - Calls the parameterized constructor.
   - Initializes `brand` with `"Toyota"`.
   - Dynamically allocates memory for `mileage` and sets it to `15000`.
   - Displays: `"Constructor called for Toyota with mileage 15000"`.

2. **myCar.display();**
   - Prints the values of `brand` and `mileage`.
   - Displays: `"Car brand: Toyota, Mileage: 15000"`.

3. **Destructor is called automatically when `myCar` goes out of scope.**
   - Frees the dynamically allocated memory for `mileage`.
   - Displays: `"Destructor called for Toyota with mileage 15000"`.

---

## **Dry Run of the Program**

| Step | Operation                        | brand (myCar) | mileage (myCar) | Output                                      |
|------|----------------------------------|---------------|------------------|---------------------------------------------|
| 1    | Create `myCar("Toyota", 15000)`  | "Toyota"      | 15000            | `"Constructor called for Toyota with mileage 15000"` |
| 2    | `myCar.display();`               | "Toyota"      | 15000            | `"Car brand: Toyota, Mileage: 15000"`       |
| 3    | Destructor called (end of scope) | "Toyota"      | 15000            | `"Destructor called for Toyota with mileage 15000"` |

---

## **Additional Explanation**

### **Dynamic Memory Allocation**
- The `mileage` variable is a pointer (`int *mileage`).
- Memory is allocated dynamically using `new int(m)` in the constructor.
- This allows the `mileage` value to be stored on the heap instead of the stack.

### **Destructor**
- The destructor is responsible for freeing the dynamically allocated memory using `delete mileage`.
- This prevents memory leaks when the object goes out of scope.

### **Constructor**
- The constructor initializes the object and allocates memory for the `mileage` variable.
- It also prints a message to indicate that the constructor has been called.

### **Scope and Lifetime**
- The object `myCar` is created in the `main()` function and exists until the end of the function.
- When the program exits the `main()` function, the destructor is automatically called to clean up the object.

### **Why Do We Need Destructors?**
- To free dynamically allocated memory and prevent memory leaks.
- To release file handles or network connections.
- To ensure proper cleanup when an object is no longer needed.

---

## **4. Lab Tasks**
1. Create a class `Student` with a default constructor that sets the student name to "Unknown".
2. Implement a parameterized constructor in the `Book` class to initialize `title` and `author`.
3. Define a function `setAge()` inside a `Person` class and implement another function `getAge()` outside the class.
4. Create a class `Laptop` that initializes the brand using a parameterized constructor.
5. Implement a `BankAccount` class with a constructor that initializes `balance` to zero and a destructor that displays a message when an object is destroyed.
6. Create a `Library` class where books can be added using a constructor, and the destructor should indicate when the object is deleted.
7. Implement a copy constructor for a `Car` class and demonstrate deep copying.


---

