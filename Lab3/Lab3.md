# **Lab: Object-Oriented Programming in C++**

## **Objective**  
By the end of this lab, students will:  
✅ Understand **Object-Oriented Programming (OOP) concepts**.  
✅ Learn the difference between **structures and classes**.  
✅ Implement **objects, classes, data members, and member functions**.  
✅ Understand **data hiding and encapsulation**.  
✅ Work with **structure variables and class objects** in C++.  

---  

# **1. Introduction to Object-Oriented Programming**  

### **What is Object-Oriented Programming (OOP)?**  
Object-Oriented Programming (OOP) is a **programming paradigm** that focuses on using **objects** to design and structure programs. Objects **bundle** data and related functions together, making code more modular, reusable, and maintainable.  

### **Why Do We Need OOP?**  
In traditional procedural programming, code becomes difficult to maintain as the complexity increases. OOP provides:  
- **Better Code Organization:** Grouping related data and functions together.  
- **Reusability:** Code can be reused using **inheritance**.  
- **Security:** Encapsulation restricts unauthorized data access.  
- **Scalability:** Programs can be expanded with minimal effort.  

**Key Features of OOP:**  
- **Encapsulation:** Bundling data and methods into objects.  
- **Abstraction:** Hiding implementation details from users.  
- **Inheritance:** Enabling code reusability.  
- **Polymorphism:** Allowing different objects to be treated uniformly.  

---  

# **2. Objects, Classes, Data Members, and Member Functions**  

### **What is a Class?**  
A **class** is a blueprint for creating objects. It defines the properties (**data members**) and behaviors (**member functions**) of an object.

### **What is an Object?**  
An **object** is an instance of a class. It represents real-world entities with attributes and actions.

### **Declaring a Class in C++**  
```cpp
#include <iostream>
using namespace std;

class Car {
public:
    string brand;
    int modelYear;

    void display() {
        cout << "Brand: " << brand << ", Model Year: " << modelYear << endl;
    }
};

int main() {
    Car car1;
    car1.brand = "Toyota";
    car1.modelYear = 2022;
    car1.display();
    return 0;
}
```
**Explanation:**  
- `Car` is a **class** with two **data members** (`brand` and `modelYear`).  
- `display()` is a **member function** that prints the car details.  
- `car1` is an **object** of the `Car` class.  

---  

# **3. Data Hiding and Encapsulation**  

### **What is Encapsulation?**  
Encapsulation is the concept of **restricting direct access** to certain details of an object and only exposing the necessary functionalities. It helps in **protecting data** and **reducing dependencies** between parts of the program.

### **Using Private Data Members in C++**  
```cpp
#include <iostream>
using namespace std;

class BankAccount {
private:
    double balance;

public:
    void setBalance(double amount) {
        if (amount >= 0)
            balance = amount;
        else
            cout << "Invalid balance!" << endl;
    }
    double getBalance() {
        return balance;
    }
};

int main() {
    BankAccount myAccount;
    myAccount.setBalance(1000);
    cout << "Balance: " << myAccount.getBalance() << endl;
    return 0;
}
```
**Explanation:**  
- `balance` is a **private data member** (cannot be accessed directly).  
- `setBalance()` ensures only valid values are assigned.  
- `getBalance()` provides controlled access to the balance.  

---  

# **4. Declaring Structures, Defining Structure Variables & Accessing Structure Members**  

### **Structures in C++**  
Structures (`struct`) are used to **group related variables** under a single name.

```cpp
#include <iostream>
using namespace std;

struct Student {
    string name;
    int age;
};

int main() {
    Student s1 = {"Alice", 20};
    cout << "Name: " << s1.name << ", Age: " << s1.age << endl;
    return 0;
}
```
**Key Differences Between Structures and Classes:**  
| Feature        | Structure (`struct`) | Class (`class`) |
|--------------|------------------|--------------|
| Default Access | Public          | Private      |
| Supports OOP? | Limited         | Full Support |
| Used for? | Small data groups | Complex Objects |

---  

# **5. Comparing Structures and Classes**  

### **Why Use Classes Instead of Structures?**  
- **Encapsulation:** Classes provide **data hiding** using private members.  
- **Functionality:** Classes allow **methods** (member functions) to operate on data.  
- **Security:** By default, members of a **class** are **private**, preventing unauthorized access.  
- **Code Reusability:** Classes support **inheritance**, which is absent in structures.  

### **Structures vs. Classes: Which One to Use?**  
- Use **structures** for **simple data grouping** (e.g., a `Point` with `x, y` coordinates).  
- Use **classes** when data should be **private** with **methods** controlling access.  

### **Example: Converting Structure to Class**  
#### **Structure Version:**  
```cpp
struct Rectangle {
    int width, height;
};
```
#### **Class Version:**  
```cpp
class Rectangle {
private:
    int width, height;
public:
    void setValues(int w, int h) { width = w; height = h; }
    int area() { return width * height; }
};
```

---  

# **Lab Tasks**  
### ✅ **Task 1: Implement a Class and Objects**  
- Create a `Book` class with `title`, `author`, and `price`.  
- Create an object and display book details.  

### ✅ **Task 2: Implement Data Hiding and Encapsulation**  
- Modify Task 1 by making `price` **private** and using getter/setter functions.  

### ✅ **Task 3: Structure vs. Class**  
- Create a `Student` structure with `name` and `grade`.  
- Convert it into a class with encapsulation.  

---  

# **Conclusion**  
🎯 **Key Takeaways:**  
✔ **OOP provides modularity** and code reusability.  
✔ **Encapsulation** protects data from unintended access.  
✔ **Structures are simple**, while **classes provide full OOP features**.  
✔ **Classes should be used** when data protection and behavior control are needed.  

---  

