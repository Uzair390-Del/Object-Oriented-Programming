
# Case Study: University Management System (UMS)

##  Objective:
Design a simple University Management System using Object-Oriented Programming in C++. This system will manage:

- Students
- Faculty
- Courses
- Departments

Students should apply OOP principles: **Encapsulation, Inheritance, Polymorphism, and Abstraction**.

---

##  Problem Statement:
You are hired to develop a simple University Management System. Your system must:

- Register students and faculty members with relevant details.
- Assign courses to students and faculty.
- Display details of students, faculty, and the courses they are involved in.
- Use inheritance to avoid repetition.
- Use polymorphism to display info in a dynamic way.

---

##  Requirements:

###  Base Class: Person
- **Data Members:** name, age, CNIC  
- **Member Functions:** getData(), displayData()

###  Derived Class: Faculty (from Person)
- **Data Members:** facultyId, designation, courseAssigned  
- **Functions:** override displayData() to show faculty-specific info

###  Derived Class: Student (from Person)
- **Data Members:** rollNo, degreeProgram, registeredCourses[]  
- **Functions:** override displayData() to show student-specific info

###  Class: Course
- **Data Members:** courseCode, courseName, creditHours

Use arrays to handle multiple students and faculty. Demonstrate the use of:
- Polymorphism using virtual functions
- Encapsulation by using private members and public accessors
- Inheritance between base and derived classes
- Abstract class for defining interfaces

---

##  Final Expected Output:
- Add new student/faculty.
- Register a course to a student/faculty.
- Display list of students or faculty with details.
- Polymorphic behavior for displayData().

---

##  Why OOP Is Needed Here:
- **Encapsulation** secures sensitive data (like CNIC).
- **Inheritance** prevents code duplication for common attributes (like name, age).
- **Polymorphism** allows calling the correct version of displayData() using a base class pointer.
- **Abstraction** hides unnecessary implementation details (like how data is stored).

---

##  C++ Code: University Management System (Beginner-Friendly with Full Explanation)

```cpp
#include <iostream>
using namespace std;

// Abstract Base Class: Person (for Students and Faculty)
class Person {
protected:
    string name;
    int age;
    string cnic;

public:
    // Virtual function to get input (can be overridden)
    virtual void getData() {
        cout << "Enter Name: ";
        cin >> name;
        cout << "Enter Age: ";
        cin >> age;
        cout << "Enter CNIC: ";
        cin >> cnic;
    }

    // Pure virtual function for displaying data (must be overridden)
    virtual void displayData() = 0;
};

// Course class for course information
class Course {
public:
    string courseCode;
    string courseName;
    int creditHours;

    void inputCourse() {
        cout << "Enter Course Code: ";
        cin >> courseCode;
        cout << "Enter Course Name: ";
        cin >> courseName;
        cout << "Enter Credit Hours: ";
        cin >> creditHours;
    }

    void displayCourse() {
        cout << courseCode << " - " << courseName << " (" << creditHours << " Credit Hours)";
    }
};

// Derived Class: Student
class Student : public Person {
private:
    string rollNo;
    string degreeProgram;
    Course registeredCourses[5]; // Max 5 courses
    int courseCount;

public:
    Student() {
        courseCount = 0;
    }

    void getData() override {
        Person::getData(); // Get base class data
        cout << "Enter Roll No: ";
        cin >> rollNo;
        cout << "Enter Degree Program: ";
        cin >> degreeProgram;
        cout << "Enter number of courses to register (Max 5): ";
        cin >> courseCount;

        if (courseCount > 5) {
            cout << "Only 5 courses allowed! Trimming to 5.\n";
            courseCount = 5;
        }

        for (int i = 0; i < courseCount; i++) {
            cout << "--- Enter Course " << i + 1 << " Details ---\n";
            registeredCourses[i].inputCourse();
        }
    }

    void displayData() override {
        cout << "\n----- Student Information -----\n";
        cout << "Name: " << name << "\nAge: " << age << "\nCNIC: " << cnic << endl;
        cout << "Roll No: " << rollNo << "\nDegree Program: " << degreeProgram << endl;
        cout << "Registered Courses:\n";
        for (int i = 0; i < courseCount; i++) {
            cout << "\t";
            registeredCourses[i].displayCourse();
            cout << endl;
        }
    }

    string getRollNo() {
        return rollNo;
    }
};

// Derived Class: Faculty
class Faculty : public Person {
private:
    string facultyId;
    string designation;
    Course assignedCourse;

public:
    void getData() override {
        Person::getData();
        cout << "Enter Faculty ID: ";
        cin >> facultyId;
        cout << "Enter Designation (e.g., Lecturer): ";
        cin >> designation;
        cout << "--- Enter Assigned Course ---\n";
        assignedCourse.inputCourse();
    }

    void displayData() override {
        cout << "\n----- Faculty Information -----\n";
        cout << "Name: " << name << "\nAge: " << age << "\nCNIC: " << cnic << endl;
        cout << "Faculty ID: " << facultyId << "\nDesignation: " << designation << endl;
        cout << "Assigned Course: ";
        assignedCourse.displayCourse();
        cout << endl;
    }
};

// Menu-driven main system
int main() {
    Person* records[20]; // Array to store both Student and Faculty objects
    int count = 0; // Number of persons in the system
    int choice;

    do {
        cout << "\n========= University Management System =========\n";
        cout << "1. Add New Student\n";
        cout << "2. Add New Faculty\n";
        cout << "3. Display All Records\n";
        cout << "4. Search Student by Roll No\n";
        cout << "5. Exit\n";
        cout << "Enter your choice (1-5): ";
        cin >> choice;

        if (choice == 1) {
            Student* s = new Student();
            s->getData();
            records[count++] = s;
        }
        else if (choice == 2) {
            Faculty* f = new Faculty();
            f->getData();
            records[count++] = f;
        }
        else if (choice == 3) {
            cout << "\n==== Displaying All Records ====\n";
            for (int i = 0; i < count; i++) {
                records[i]->displayData(); // Polymorphism in action
            }
        }
        else if (choice == 4) {
            string searchRoll;
            cout << "Enter Roll No to search: ";
            cin >> searchRoll;
            bool found = false;
            for (int i = 0; i < count; i++) {
                Student* s = dynamic_cast<Student*>(records[i]); // Try to convert to Student
                if (s != nullptr && s->getRollNo() == searchRoll) {
                    s->displayData();
                    found = true;
                    break;
                }
            }
            if (!found) {
                cout << "Student with Roll No " << searchRoll << " not found.\n";
            }
        }
        else if (choice == 5) {
            cout << "Exiting program...\n";
        }
        else {
            cout << "Invalid option. Try again.\n";
        }
    } while (choice != 5);

    // Free memory
    for (int i = 0; i < count; i++) {
        delete records[i];
    }

    return 0;
}

```

---

##  Concepts Used in Simple Words

| OOP Concept     | Where Used                                                                 |
|------------------|----------------------------------------------------------------------------|
| Encapsulation   | All data members are private; accessed via class functions.               |
| Inheritance     | Student and Faculty classes inherit from Person.                          |
| Polymorphism    | displayData() is virtual and overridden—called dynamically at runtime.    |
| Abstraction     | Person is abstract—it only gives the idea of a person, not specific.      |

---

##  Suggested Student Tasks
To ensure full learning, ask students to:

- Add another class Admin inheriting from Person.
- Extend the system to save data to a file (bonus).
