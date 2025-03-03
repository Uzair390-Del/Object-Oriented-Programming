# **Lab: Structures and Pointers in C++**

## **Objective**  
By the end of this lab, students will:  
✅ Understand **structures** and how they work.  
✅ Learn how to **declare, initialize, and access** structure members.  
✅ Understand **pointers with structures** and how they improve efficiency.  
✅ Implement **dynamic memory allocation** for structures.  
✅ Learn how to **pass structures to functions** using pointers.  
✅ Work with **arrays of structures dynamically**.  

---  

# **1. Introduction to Structures**  

### **What is a Structure?**  
A **structure** (`struct`) is a user-defined data type in C++ that **groups multiple variables** (of different types) into a single unit.  

**Why Use Structures?**  
- Helps in **organizing related data** efficiently.  
- Enables **better readability** and maintainability.  
- Useful for handling **complex data** (e.g., student records, employee details).  

### **Declaring a Structure**  
A structure is defined using the `struct` keyword, followed by its **name** and **members**.

```cpp
struct Student {
    string name;
    int age;
    float gpa;
};
```

**Explanation:**  
- `Student` is the **structure name**.  
- `name`, `age`, and `gpa` are **data members**.  

---  

### **Creating and Accessing Structure Variables**  

Once a structure is defined, we can create **structure variables (objects)** and access its members using the **dot (`.`) operator**.

#### **Example 1: Basic Structure Usage**  

```cpp
#include <iostream>
using namespace std;

struct Student {
    string name;
    int age;
    float gpa;
};

int main() {
    Student s1;  // Creating a structure variable

    // Assigning values
    s1.name = "Alice";
    s1.age = 20;
    s1.gpa = 3.9;

    // Displaying values
    cout << "Student Name: " << s1.name << endl;
    cout << "Age: " << s1.age << endl;
    cout << "GPA: " << s1.gpa << endl;

    return 0;
}
```

### **🔎 Step-by-Step Dry Run**  

| **Step** | **Statement Executed** | **Memory State** |
|---------|------------------|--------------|
| 1 | `Student s1;` | `s1` is created |
| 2 | `s1.name = "Alice";` | `s1.name = "Alice"` |
| 3 | `s1.age = 20;` | `s1.age = 20` |
| 4 | `s1.gpa = 3.9;` | `s1.gpa = 3.9` |
| 5 | `cout` statements | Output displayed |

---

# **2. Pointers and Structures**  
### **What are Pointers to Structures?**  
A **pointer** is a variable that stores the memory address of another variable. When working with structures, **pointers help in accessing and modifying structure members efficiently** without needing to copy entire structures. This is particularly useful for large structures, as passing them by pointer avoids unnecessary memory usage.  

**Advantages of Using Pointers with Structures:**  
- Efficient memory usage, as only the address is passed instead of the entire structure.  
- Faster data access and modification.  
- Used in dynamic memory allocation, allowing structures to be created at runtime. 

### **Example 2: Pointer to Structure**  

```cpp
#include <iostream>
using namespace std;

struct Student {
    string name;
    int age;
    float gpa;
};

int main() {
    Student s1 = {"Bob", 21, 3.8};
    Student* ptr = &s1;  // Pointer to structure

    // Accessing structure members using pointer
    cout << "Using Pointer:" << endl;
    cout << "Name: " << ptr->name << endl;
    cout << "Age: " << ptr->age << endl;
    cout << "GPA: " << ptr->gpa << endl;

    return 0;
}
```

### **🔎 Step-by-Step Dry Run**  

| **Step** | **Statement Executed** | **Memory State** |
|---------|------------------|--------------|
| 1 | `Student s1 = {"Bob", 21, 3.8};` | `s1` is created |
| 2 | `Student* ptr = &s1;` | `ptr` stores `s1`'s address |
| 3 | `cout << ptr->name;` | "Bob" is printed |
| 4 | `cout << ptr->age;` | `21` is printed |
| 5 | `cout << ptr->gpa;` | `3.8` is printed |

---


# **Lab Tasks**  
### ✅ **Task 1: Structure Basics**  
- Create an `Employee` structure with `name`, `id`, and `salary`.  
- Assign values and display them.  
### ✅ **Task 2: Structure Basics**  
- Create a `Book` structure with `title`, `author`, and `price`.  
- Assign values and display them.  

### ✅ **Task 2: Pointer to Structure**  
- Modify Task 1 and Task 2 to use **pointers**.  

---

# **Conclusion**  
🎯 **Key Takeaways:**  
✔ Structures **organize complex data** efficiently.  
✔ Pointers **optimize memory usage**.   
