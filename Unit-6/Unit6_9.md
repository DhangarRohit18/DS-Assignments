# Unit VI Assignment 9: Student Database Management System using Hashing

Implementation of a student database management system using hashing techniques to allow efficient insertion, search, and deletion of student records.

## Problem Statement

WAP to simulate student databases as a hash table. A student database management system using hashing techniques to allow efficient insertion, search, and deletion of student records.

## Pseudo Code

### Student Record Structure
```
Structure Student:
    rollNumber: integer
    name: string
    branch: string
    semester: integer
    cgpa: float
    email: string
    phone: string
```

### Hash Table Structure
```
Structure HashNode:
    student: Student
    next: pointer to HashNode
Structure HashTable:
    size: integer
    buckets: array of pointers to HashNode of size size
    count: integer
```

### Hash Function
```
Algorithm Hash(rollNumber, tableSize):
    Return rollNumber MOD tableSize
```

### Insert Student
```
Algorithm InsertStudent(hashTable, student):
    index = Hash(student.rollNumber, hashTable.size)
    current = hashTable.buckets[index]
    While current is not NULL:
        If current.student.rollNumber == student.rollNumber:
            Print "Student already exists"
            Return false
        current = current.next
    Create new node with student
    new node.next = hashTable.buckets[index]
    hashTable.buckets[index] = new node
    hashTable.count++
    Return true
```

### Search Student
```
Algorithm SearchStudent(hashTable, rollNumber):
    index = Hash(rollNumber, hashTable.size)
    current = hashTable.buckets[index]
    While current is not NULL:
        If current.student.rollNumber == rollNumber:
            Return current.student
        current = current.next
    Return NULL
```

### Delete Student
```
Algorithm DeleteStudent(hashTable, rollNumber):
    index = Hash(rollNumber, hashTable.size)
    current = hashTable.buckets[index]
    previous = NULL
    While current is not NULL:
        If current.student.rollNumber == rollNumber:
            If previous is NULL:
                hashTable.buckets[index] = current.next
            Else:
                previous.next = current.next
            Free current
            hashTable.count--
            Return true
        previous = current
        current = current.next
    Return false
```

### Update Student
```
Algorithm UpdateStudent(hashTable, rollNumber, updatedStudent):
    index = Hash(rollNumber, hashTable.size)
    current = hashTable.buckets[index]
    While current is not NULL:
        If current.student.rollNumber == rollNumber:
            current.student = updatedStudent
            Return true
        current = current.next
    Return false
```

### Display All Students
```
Algorithm DisplayAllStudents(hashTable):
    For i = 0 to hashTable.size-1:
        If hashTable.buckets[i] is not NULL:
            current = hashTable.buckets[i]
            While current is not NULL:
                Print current.student details
                current = current.next
```

```
## C++ Code Implementation

```cpp
#include <iostream>
#include <cstring>
using namespace std;

#define TABLE_SIZE 50

struct Student {
    int rollNumber;
    char name[50];
    char branch[30];
    int semester;
    float cgpa;
    char email[50];
    char phone[15];
};

struct HashNode {
    Student student;
    HashNode* next;
};

struct HashTable {
    int size;
    HashNode** buckets;
    int count;
};

HashTable* createHashTable(int size) {
    HashTable* hashTable = new HashTable;
    hashTable->size = size;
    hashTable->count = 0;
    hashTable->buckets = new HashNode*[size];
    
    for (int i = 0; i < size; i++) {
        hashTable->buckets[i] = nullptr;
    }
    
    return hashTable;
}

int hashFunction(int rollNumber, int tableSize) {
    return rollNumber % tableSize;
}

bool insertStudent(HashTable* hashTable, Student student) {
    int index = hashFunction(student.rollNumber, hashTable->size);
    HashNode* current = hashTable->buckets[index];
    
    while (current != nullptr) {
        if (current->student.rollNumber == student.rollNumber) {
            cout << "Error: Student with Roll Number " << student.rollNumber << " already exists!" << endl;
            return false;
        }
        current = current->next;
    }
    
    HashNode* newNode = new HashNode;
    newNode->student = student;
    newNode->next = hashTable->buckets[index];
    hashTable->buckets[index] = newNode;
    hashTable->count++;
    
    cout << "Student " << student.name << " (Roll No: " << student.rollNumber << ") inserted successfully at index " << index << endl;
    return true;
}

Student* searchStudent(HashTable* hashTable, int rollNumber) {
    int index = hashFunction(rollNumber, hashTable->size);
    HashNode* current = hashTable->buckets[index];
    
    while (current != nullptr) {
        if (current->student.rollNumber == rollNumber) {
            return &(current->student);
        }
        current = current->next;
    }
    
    return nullptr;
}

bool deleteStudent(HashTable* hashTable, int rollNumber) {
    int index = hashFunction(rollNumber, hashTable->size);
    HashNode* current = hashTable->buckets[index];
    HashNode* previous = nullptr;
    
    while (current != nullptr) {
        if (current->student.rollNumber == rollNumber) {
            if (previous == nullptr) {
                hashTable->buckets[index] = current->next;
            } else {
                previous->next = current->next;
            }
            
            cout << "Student " << current->student.name << " (Roll No: " << rollNumber << ") deleted successfully" << endl;
            delete current;
            hashTable->count--;
            return true;
        }
        
        previous = current;
        current = current->next;
    }
    
    cout << "Error: Student with Roll Number " << rollNumber << " not found!" << endl;
    return false;
}

bool updateStudent(HashTable* hashTable, int rollNumber, Student updatedStudent) {
    int index = hashFunction(rollNumber, hashTable->size);
    HashNode* current = hashTable->buckets[index];
    
    while (current != nullptr) {
        if (current->student.rollNumber == rollNumber) {
            current->student = updatedStudent;
            cout << "Student with Roll Number " << rollNumber << " updated successfully" << endl;
            return true;
        }
        current = current->next;
    }
    
    cout << "Error: Student with Roll Number " << rollNumber << " not found!" << endl;
    return false;
}

void displayStudent(Student student) {
    cout << "\n--- Student Details ---" << endl;
    cout << "Roll Number: " << student.rollNumber << endl;
    cout << "Name: " << student.name << endl;
    cout << "Branch: " << student.branch << endl;
    cout << "Semester: " << student.semester << endl;
    cout << "CGPA: " << student.cgpa << endl;
    cout << "Email: " << student.email << endl;
    cout << "Phone: " << student.phone << endl;
}

void displayAllStudents(HashTable* hashTable) {
    cout << "\n=== Student Database (Total: " << hashTable->count << ") ===" << endl;
    for (int i = 0; i < hashTable->size; i++) {
        HashNode* current = hashTable->buckets[i];
        while (current != nullptr) {
            cout << "\n[Index " << i << "] Roll: " << current->student.rollNumber 
                 << " | Name: " << current->student.name 
                 << " | Branch: " << current->student.branch 
                 << " | Sem: " << current->student.semester 
                 << " | CGPA: " << current->student.cgpa;
            current = current->next;
        }
    }
    
    cout << endl;
}

void displayByBranch(HashTable* hashTable, const char* branch) {
    cout << "\n=== Students in " << branch << " Branch ===" << endl;
    int count = 0;
    
    for (int i = 0; i < hashTable->size; i++) {
        HashNode* current = hashTable->buckets[i];
        while (current != nullptr) {
            if (strcmp(current->student.branch, branch) == 0) {
                displayStudent(current->student);
                count++;
            }
            current = current->next;
        }
    }
    
    if (count == 0) {
        cout << "No students found in " << branch << " branch" << endl;
    } else {
        cout << "\nTotal students in " << branch << ": " << count << endl;
    }
}

void displayToppers(HashTable* hashTable, float minCGPA) {
    cout << "\n=== Students with CGPA >= " << minCGPA << " ===" << endl;
    int count = 0;
    
    for (int i = 0; i < hashTable->size; i++) {
        HashNode* current = hashTable->buckets[i];
        while (current != nullptr) {
            if (current->student.cgpa >= minCGPA) {
                cout << "Roll: " << current->student.rollNumber 
                     << " | Name: " << current->student.name 
                     << " | CGPA: " << current->student.cgpa 
                     << " | Branch: " << current->student.branch << endl;
                count++;
            }
            current = current->next;
        }
    }
    
    cout << "\nTotal toppers: " << count << endl;
}

void freeHashTable(HashTable* hashTable) {
    for (int i = 0; i < hashTable->size; i++) {
        HashNode* current = hashTable->buckets[i];
        while (current != nullptr) {
            HashNode* temp = current;
            current = current->next;
            delete temp;
        }
    }
    
    delete[] hashTable->buckets;
    delete hashTable;
}

int main() {
    HashTable* hashTable = createHashTable(TABLE_SIZE);
    
    Student s1 = {1001, "Rahul Sharma", "Computer Science", 6, 8.9, "rahul@vit.edu", "9876543210"};
    Student s2 = {1002, "Priya Patel", "Electronics", 4, 9.2, "priya@vit.edu", "9876543211"};
    Student s3 = {1003, "Amit Kumar", "Mechanical", 6, 7.8, "amit@vit.edu", "9876543212"};
    Student s4 = {1004, "Sneha Gupta", "Computer Science", 4, 9.5, "sneha@vit.edu", "9876543213"};
    Student s5 = {1005, "Vikram Singh", "Civil", 6, 8.1, "vikram@vit.edu", "9876543214"};
    Student s6 = {1006, "Ananya Reddy", "Computer Science", 4, 8.7, "ananya@vit.edu", "9876543215"};
    
    cout << "=== Inserting Student Records ===\n" << endl;
    insertStudent(hashTable, s1);
    insertStudent(hashTable, s2);
    insertStudent(hashTable, s3);
    insertStudent(hashTable, s4);
    insertStudent(hashTable, s5);
    insertStudent(hashTable, s6);
    
    displayAllStudents(hashTable);
    
    cout << "\n\n=== Searching for Student ===" << endl;
    int searchRoll = 1004;
    Student* found = searchStudent(hashTable, searchRoll);
    if (found != nullptr) {
        cout << "Student found!";
        displayStudent(*found);
    } else {
        cout << "Student with Roll Number " << searchRoll << " not found!" << endl;
    }
    
    cout << "\n\n=== Updating Student ===" << endl;
    Student updatedS3 = {1003, "Amit Kumar", "Mechanical", 7, 8.2, "amit@vit.edu", "9876543212"};
    updateStudent(hashTable, 1003, updatedS3);
    
    cout << "\n\n=== Display by Branch ===";
    displayByBranch(hashTable, "Computer Science");
    
    cout << "\n\n=== Display Toppers ===";
    displayToppers(hashTable, 8.5);
    
    cout << "\n\n=== Deleting Student ===" << endl;
    deleteStudent(hashTable, 1002);
    
    displayAllStudents(hashTable);
    
    freeHashTable(hashTable);
    return 0;
}
```

## Sample Output
```
=== Inserting Student Records ===

Student Rahul Sharma (Roll No: 1001) inserted successfully at index 1
Student Priya Patel (Roll No: 1002) inserted successfully at index 2
Student Amit Kumar (Roll No: 1003) inserted successfully at index 3
Student Sneha Gupta (Roll No: 1004) inserted successfully at index 4
Student Vikram Singh (Roll No: 1005) inserted successfully at index 5
Student Ananya Reddy (Roll No: 1006) inserted successfully at index 6

=== Student Database (Total: 6) ===

[Index 1] Roll: 1001 | Name: Rahul Sharma | Branch: Computer Science | Sem: 6 | CGPA: 8.90
[Index 2] Roll: 1002 | Name: Priya Patel | Branch: Electronics | Sem: 4 | CGPA: 9.20
[Index 3] Roll: 1003 | Name: Amit Kumar | Branch: Mechanical | Sem: 6 | CGPA: 7.80
[Index 4] Roll: 1004 | Name: Sneha Gupta | Branch: Computer Science | Sem: 4 | CGPA: 9.50
[Index 5] Roll: 1005 | Name: Vikram Singh | Branch: Civil | Sem: 6 | CGPA: 8.10
[Index 6] Roll: 1006 | Name: Ananya Reddy | Branch: Computer Science | Sem: 4 | CGPA: 8.70


=== Searching for Student ===
Student found!
--- Student Details ---
Roll Number: 1004
Name: Sneha Gupta
Branch: Computer Science
Semester: 4
CGPA: 9.50
Email: sneha@vit.edu
Phone: 9876543213


=== Updating Student ===
Student with Roll Number 1003 updated successfully


=== Display by Branch ===

=== Students in Computer Science Branch ===

--- Student Details ---
Roll Number: 1001
Name: Rahul Sharma
Branch: Computer Science
Semester: 6
CGPA: 8.90
Email: rahul@vit.edu
Phone: 9876543210

--- Student Details ---
Roll Number: 1004
Name: Sneha Gupta
Branch: Computer Science
Semester: 4
CGPA: 9.50
Email: sneha@vit.edu
Phone: 9876543213

--- Student Details ---
Roll Number: 1006
Name: Ananya Reddy
Branch: Computer Science
Semester: 4
CGPA: 8.70
Email: ananya@vit.edu
Phone: 9876543215

Total students in Computer Science: 3


=== Display Toppers ===

=== Students with CGPA >= 8.50 ===
Roll: 1001 | Name: Rahul Sharma | CGPA: 8.90 | Branch: Computer Science
Roll: 1002 | Name: Priya Patel | CGPA: 9.20 | Branch: Electronics
Roll: 1004 | Name: Sneha Gupta | CGPA: 9.50 | Branch: Computer Science
Roll: 1006 | Name: Ananya Reddy | CGPA: 8.70 | Branch: Computer Science

Total toppers: 4


=== Deleting Student ===
Student Priya Patel (Roll No: 1002) deleted successfully

=== Student Database (Total: 5) ===

[Index 1] Roll: 1001 | Name: Rahul Sharma | Branch: Computer Science | Sem: 6 | CGPA: 8.90
[Index 3] Roll: 1003 | Name: Amit Kumar | Branch: Mechanical | Sem: 7 | CGPA: 8.20
[Index 4] Roll: 1004 | Name: Sneha Gupta | Branch: Computer Science | Sem: 4 | CGPA: 9.50
[Index 5] Roll: 1005 | Name: Vikram Singh | Branch: Civil | Sem: 6 | CGPA: 8.10
[Index 6] Roll: 1006 | Name: Ananya Reddy | Branch: Computer Science | Sem: 4 | CGPA: 8.70
```
```
```
## Dry Run
### Insertion Process:
1. **Insert Student 1001:**
   - Hash: 1001 % 50 = 1
   - Insert at index 1
2. **Insert Student 1002:**
   - Hash: 1002 % 50 = 2
   - Insert at index 2
3. **Insert Student 1003:**
   - Hash: 1003 % 50 = 3
   - Insert at index 3
### Search Process:
1. **Search Student 1004:**
   - Hash: 1004 % 50 = 4
   - Check chain at index 4
   - Found student 1004
### Update Process:
1. **Update Student 1003:**
   - Hash: 1003 % 50 = 3
   - Find student at index 3
   - Update CGPA from 7.8 to 8.2
   - Update semester from 6 to 7
### Delete Process:
1. **Delete Student 1002:**
   - Hash: 1002 % 50 = 2
   - Find student at index 2
   - Remove from chain
   - Decrease count
## Performance Analysis
### Time Complexity:
- **Hash Function:** O(1)
- **Insert (Average):** O(1)
- **Insert (Worst):** O(n) - when all students hash to same index
- **Search (Average):** O(1)
- **Search (Worst):** O(n) - long chain
- **Delete (Average):** O(1)
- **Delete (Worst):** O(n)
- **Update (Average):** O(1)
- **Update (Worst):** O(n)
- **Display All:** O(n)
- **Display by Branch:** O(n)
- **Display Toppers:** O(n)
### Space Complexity:
- O(n) where n is the number of students
## Conclusion
The student database management system using hashing provides:
- Efficient O(1) average-case operations for insert, search, delete, and update
- Separate chaining for collision resolution handles duplicates well
- Additional features like branch-wise display and topper filtering
- Scalable design suitable for large student databases
- Good distribution with MOD hash function
- Easy to extend with more search criteria
- Memory efficient with dynamic allocation
- Suitable for real-world college management systems
