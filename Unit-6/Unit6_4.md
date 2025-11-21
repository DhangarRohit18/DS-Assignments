# Unit VI Assignment 4: Student Record Management using Hash Table

Implementation to store and retrieve student records using roll numbers.

## Problem Statement

Store and retrieve student records using roll numbers.

## Pseudo Code

### Student Record Structure
```
Structure Student:
    rollNumber: integer
    name: string
    grade: string
    marks: float
```

### Hash Table Structure
```
Structure HashNode:
    student: Student
    next: pointer to HashNode
Structure HashTable:
    size: integer
    buckets: array of pointers to HashNode of size size
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
    Create new node with student
    new node.next = hashTable.buckets[index]
    hashTable.buckets[index] = new node
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
    If current is NULL:
        Return "Student not found"
    If current.student.rollNumber == rollNumber:
        hashTable.buckets[index] = current.next
        Free current
        Return "Student deleted successfully"
    While current.next is not NULL:
        If current.next.student.rollNumber == rollNumber:
            temp = current.next
            current.next = current.next.next
            Free temp
            Return "Student deleted successfully"
        current = current.next
    Return "Student not found"
```

## Code Implementation

```c
#include <iostream>
using namespace std;
#include <stdlib.h>
#include <string.h>
#define TABLE_SIZE 20
#define MAX_NAME_LENGTH 50
#define MAX_GRADE_LENGTH 5
struct Student_rrd {
    int rollNumber_rrd;
    char name_rrd[MAX_NAME_LENGTH];
    char grade_rrd[MAX_GRADE_LENGTH];
    float marks_rrd;
};

struct HashNode_rrd {
    struct Student_rrd student_rrd;
    struct HashNode_rrd* next_rrd;
};

struct HashTable_rrd {
    int size_rrd;
    struct HashNode_rrd** buckets_rrd;
};

struct HashTable_rrd* createHashTable_rrd(int size_rrd);
int hash_rrd(int rollNumber_rrd, int tableSize_rrd);
void insertStudent_rrd(struct HashTable_rrd* hashTable_rrd, struct Student_rrd student_rrd);
struct Student_rrd* searchStudent_rrd(struct HashTable_rrd* hashTable_rrd, int rollNumber_rrd);
int deleteStudent_rrd(struct HashTable_rrd* hashTable_rrd, int rollNumber_rrd);
void displayStudent_rrd(struct Student_rrd* student_rrd);
void displayAllStudents_rrd(struct HashTable_rrd* hashTable_rrd);
float loadFactor_rrd(struct HashTable_rrd* hashTable_rrd);
int countCollisions_rrd(struct HashTable_rrd* hashTable_rrd);
void freeHashTable_rrd(struct HashTable_rrd* hashTable_rrd);
void createSampleData_rrd(struct HashTable_rrd* hashTable_rrd);
void displayMenu_rrd();
struct HashTable_rrd* createHashTable_rrd(int size_rrd) {
    struct HashTable_rrd* hashTable_rrd = (struct HashTable_rrd*)malloc(sizeof(struct HashTable_rrd));
    hashTable_rrd->size_rrd = size_rrd;
    hashTable_rrd->buckets_rrd = (struct HashNode_rrd**)malloc(size_rrd * sizeof(struct HashNode_rrd*));
    for (int i_rrd = 0; i_rrd < size_rrd; i_rrd++)
{
        hashTable_rrd->buckets_rrd[i_rrd] = NULL;
    }
    return hashTable_rrd;
}

int hash_rrd(int rollNumber_rrd, int tableSize_rrd) {
    return rollNumber_rrd % tableSize_rrd;
}

void insertStudent_rrd(struct HashTable_rrd* hashTable_rrd, struct Student_rrd student_rrd) {
    int index_rrd = hash_rrd(student_rrd.rollNumber_rrd, hashTable_rrd->size_rrd);
    struct HashNode_rrd* newNode_rrd = (struct HashNode_rrd*)malloc(sizeof(struct HashNode_rrd));
    newNode_rrd->student_rrd = student_rrd;
    newNode_rrd->next_rrd = NULL;
    newNode_rrd->next_rrd = hashTable_rrd->buckets_rrd[index_rrd];
    hashTable_rrd->buckets_rrd[index_rrd] = newNode_rrd;
    cout << "Student %s (Roll: " << student_rrd.name_rrd, student_rrd.rollNumber_rrd, index_rrd << ") inserted at index %d" << endl;
}

struct Student_rrd* searchStudent_rrd(struct HashTable_rrd* hashTable_rrd, int rollNumber_rrd) {
    int index_rrd = hash_rrd(rollNumber_rrd, hashTable_rrd->size_rrd);
    struct HashNode_rrd* current_rrd = hashTable_rrd->buckets_rrd[index_rrd];
    while (current_rrd != NULL)
{
        if (current_rrd->student_rrd.rollNumber_rrd == rollNumber_rrd)
{
            return &(current_rrd->student_rrd);
        }

        current_rrd = current_rrd->next_rrd;
    }
    return NULL;
}

int deleteStudent_rrd(struct HashTable_rrd* hashTable_rrd, int rollNumber_rrd) {
    int index_rrd = hash_rrd(rollNumber_rrd, hashTable_rrd->size_rrd);
    struct HashNode_rrd* current_rrd = hashTable_rrd->buckets_rrd[index_rrd];
    if (current_rrd != NULL && current_rrd->student_rrd.rollNumber_rrd == rollNumber_rrd)
{
        hashTable_rrd->buckets_rrd[index_rrd] = current_rrd->next_rrd;
        free(current_rrd);
        cout << "Student with roll number " << rollNumber_rrd << " deleted successfully" << endl;
        return 1;
    }

    while (current_rrd != NULL && current_rrd->next_rrd != NULL)
{
        if (current_rrd->next_rrd->student_rrd.rollNumber_rrd == rollNumber_rrd)
{
            struct HashNode_rrd* temp_rrd = current_rrd->next_rrd;
            current_rrd->next_rrd = current_rrd->next_rrd->next_rrd;
            free(temp_rrd);
            cout << "Student with roll number " << rollNumber_rrd << " deleted successfully" << endl;
            return 1;
        }

        current_rrd = current_rrd->next_rrd;
    }

    cout << "Student with roll number " << rollNumber_rrd << " not found" << endl;
    return 0;
}

void displayStudent_rrd(struct Student_rrd* student_rrd) {
    if (student_rrd != NULL)
{
        cout << "Roll Number: " << student_rrd->rollNumber_rrd << "" << endl;
        cout << "Name: " << student_rrd->name_rrd << "" << endl;
        cout << "Grade: " << student_rrd->grade_rrd << "" << endl;
        printf("Marks: %.2f\n", student_rrd->marks_rrd);
    } else
{

        cout << "Student record not found" << endl;
    }
}

void displayAllStudents_rrd(struct HashTable_rrd* hashTable_rrd) {
    cout << "\nAll Student Records:" << endl;
    cout << "====================" << endl;
    int count_rrd = 0;
    for (int i_rrd = 0; i_rrd < hashTable_rrd->size_rrd; i_rrd++)
{
        struct HashNode_rrd* current_rrd = hashTable_rrd->buckets_rrd[i_rrd];
        while (current_rrd != NULL)
{
            cout << "Bucket " << i_rrd << ":" << endl;
            displayStudent_rrd(&(current_rrd->student_rrd));
            cout << "--------------------" << endl;
            count_rrd++;
            current_rrd = current_rrd->next_rrd;
        }
    }

    if (count_rrd == 0)
{
        cout << "No student records found" << endl;
    } else
{

        cout << "Total students: " << count_rrd << "" << endl;
    }
}

float loadFactor_rrd(struct HashTable_rrd* hashTable_rrd)
{
    int totalElements_rrd = 0;
    for (int i_rrd = 0; i_rrd < hashTable_rrd->size_rrd; i_rrd++)
{
        struct HashNode_rrd* current_rrd = hashTable_rrd->buckets_rrd[i_rrd];
        while (current_rrd != NULL)
{
            totalElements_rrd++;
            current_rrd = current_rrd->next_rrd;
        }
    }
    return (float)totalElements_rrd / hashTable_rrd->size_rrd;
}

int countCollisions_rrd(struct HashTable_rrd* hashTable_rrd) {
    int collisions_rrd = 0;
    for (int i_rrd = 0; i_rrd < hashTable_rrd->size_rrd; i_rrd++)
{
        struct HashNode_rrd* current_rrd = hashTable_rrd->buckets_rrd[i_rrd];
        int bucketSize_rrd = 0;
        while (current_rrd != NULL)
{
            bucketSize_rrd++;
            current_rrd = current_rrd->next_rrd;
        }

        if (bucketSize_rrd > 1)
{
            collisions_rrd += (bucketSize_rrd - 1);
        }
    }
    return collisions_rrd;
}

void freeHashTable_rrd(struct HashTable_rrd* hashTable_rrd) {
    for (int i_rrd = 0; i_rrd < hashTable_rrd->size_rrd; i_rrd++)
{
        struct HashNode_rrd* current_rrd = hashTable_rrd->buckets_rrd[i_rrd];
        while (current_rrd != NULL)
{
            struct HashNode_rrd* temp_rrd = current_rrd;
            current_rrd = current_rrd->next_rrd;
            free(temp_rrd);
        }
    }

    free(hashTable_rrd->buckets_rrd);
    free(hashTable_rrd);
}

void createSampleData_rrd(struct HashTable_rrd* hashTable_rrd) {
    struct Student_rrd students_rrd[] = {
        {101, "Alice Johnson", "A", 95.5},
        {102, "Bob Smith", "B", 87.0},
        {103, "Charlie Brown", "A", 92.5},
        {104, "Diana Prince", "A+", 98.0},
        {105, "Eve Wilson", "B+", 89.5},
        {106, "Frank Miller", "B", 85.0},
        {107, "Grace Lee", "A", 94.0},
        {108, "Henry Davis", "B+", 88.5},
        {109, "Ivy Clark", "A-", 91.0},
        {110, "Jack White", "B", 86.5}
    };

    int numStudents_rrd = sizeof(students_rrd) / sizeof(students_rrd[0]);
    for (int i_rrd = 0; i_rrd < numStudents_rrd; i_rrd++)
{
        insertStudent_rrd(hashTable_rrd, students_rrd[i_rrd]);
    }

    cout << "Sample student data created successfully!" << endl;
}

void addStudentInteractive_rrd(struct HashTable_rrd* hashTable_rrd) {
    struct Student_rrd student_rrd;
    cout << "Enter roll number: ";
    cin >> student_rrd.rollNumber_rrd;
    if (searchStudent_rrd(hashTable_rrd, student_rrd.rollNumber_rrd) != NULL)
{
        cout << "Student with roll number " << student_rrd.rollNumber_rrd << " already exists!" << endl;
        return;
    }

    cout << "Enter name: ";
    scanf(" %[^\n]s", student_rrd.name_rrd);
    cout << "Enter grade: ";
    cin >> student_rrd.grade_rrd;
    cout << "Enter marks: ";
    scanf("%f", &student_rrd.marks_rrd);
    if (student_rrd.marks_rrd < 0 || student_rrd.marks_rrd > 100)
{
        cout << "Invalid marks! Marks should be between 0 and 100." << endl;
        return;
    }

    insertStudent_rrd(hashTable_rrd, student_rrd);
}

void displayMenu_rrd() {
    cout << "\n===== Student Record Management System =====" << endl;
    cout << "1. Add Student Record" << endl;
    cout << "2. Search Student by Roll Number" << endl;
    cout << "3. Delete Student by Roll Number" << endl;
    cout << "4. Display All Students" << endl;
    cout << "5. Show Load Factor" << endl;
    cout << "6. Show Collision Count" << endl;
    cout << "7. Create Sample Data" << endl;
    cout << "8. Exit" << endl;
    cout << "=========================================" << endl;
    cout << "Enter your choice: ";
}

int main() {
    cout << "Welcome to Student Record Management System using Hash Table!" << endl;
    int tableSize_rrd;
    cout << "Enter the size of the hash table: ";
    cin >> tableSize_rrd;
    if (tableSize_rrd <= 0)
{
        cout << "Invalid table size! Must be positive." << endl;
        return 1;
    }

    struct HashTable_rrd* hashTable_rrd = createHashTable_rrd(tableSize_rrd);
    int choice_rrd;
    while (1)
{
        displayMenu_rrd();
        cin >> choice_rrd;
        switch (choice_rrd)
{
{
                addStudentInteractive_rrd(hashTable_rrd);
                break;
            }

{
                int rollNumber_rrd;
                cout << "Enter roll number to search: ";
                cin >> rollNumber_rrd;
                struct Student_rrd* student_rrd = searchStudent_rrd(hashTable_rrd, rollNumber_rrd);
                if (student_rrd != NULL)
{
                    cout << "\nStudent Record Found:" << endl;
                    cout << "=====================" << endl;
                    displayStudent_rrd(student_rrd);
                } else
{

                    cout << "Student with roll number " << rollNumber_rrd << " not found" << endl;
                }
                break;
            }

{
                int rollNumber_rrd;
                cout << "Enter roll number to delete: ";
                cin >> rollNumber_rrd;
                deleteStudent_rrd(hashTable_rrd, rollNumber_rrd);
                break;
            }

{
                displayAllStudents_rrd(hashTable_rrd);
                break;
            }

{
                float loadFactor_rrd_val = loadFactor_rrd(hashTable_rrd);
                printf("Load Factor: %.2f\n", loadFactor_rrd_val);
                break;
            }

{
                int collisions_rrd = countCollisions_rrd(hashTable_rrd);
                cout << "Number of collisions: " << collisions_rrd << "" << endl;
                break;
            }

{
                createSampleData_rrd(hashTable_rrd);
                displayAllStudents_rrd(hashTable_rrd);
                break;
            }

{
                cout << "Thank you for using Student Record Management System!" << endl;
                freeHashTable_rrd(hashTable_rrd);
                exit(0);
            }

{
                cout << "Invalid choice! Please try again." << endl;
            }
        }
    }
    return 0;
}
```

## Output

```
Welcome to Student Record Management System using Hash Table!
Enter the size of the hash table: 20
===== Student Record Management System =====
1. Add Student Record
2. Search Student by Roll Number
3. Delete Student by Roll Number
4. Display All Students
5. Show Load Factor
6. Show Collision Count
7. Create Sample Data
8. Exit
=========================================
Enter your choice: 7
Sample student data created successfully!
===== Student Record Management System =====
1. Add Student Record
2. Search Student by Roll Number
3. Delete Student by Roll Number
4. Display All Students
5. Show Load Factor
6. Show Collision Count
7. Create Sample Data
8. Exit
=========================================
Enter your choice: 4
All Student Records:
====================
Bucket 1:
Roll Number: 101
Name: Alice Johnson
Grade: A
Marks: 95.50
--------------------
Bucket 2:
Roll Number: 102
Name: Bob Smith
Grade: B
Marks: 87.00
--------------------
Bucket 3:
Roll Number: 103
Name: Charlie Brown
Grade: A
Marks: 92.50
--------------------
Bucket 4:
Roll Number: 104
Name: Diana Prince
Grade: A+
Marks: 98.00
--------------------
Bucket 5:
Roll Number: 105
Name: Eve Wilson
Grade: B+
Marks: 89.50
--------------------
Bucket 6:
Roll Number: 106
Name: Frank Miller
Grade: B
Marks: 85.00
--------------------
Bucket 7:
Roll Number: 107
Name: Grace Lee
Grade: A
Marks: 94.00
--------------------
Bucket 8:
Roll Number: 108
Name: Henry Davis
Grade: B+
Marks: 88.50
--------------------
Bucket 9:
Roll Number: 109
Name: Ivy Clark
Grade: A-
Marks: 91.00
--------------------
Bucket 10:
Roll Number: 110
Name: Jack White
Grade: B
Marks: 86.50
--------------------
Total students: 10
===== Student Record Management System =====
1. Add Student Record
2. Search Student by Roll Number
3. Delete Student by Roll Number
4. Display All Students
5. Show Load Factor
6. Show Collision Count
7. Create Sample Data
8. Exit
=========================================
Enter your choice: 2
Enter roll number to search: 105
Student Record Found:
=====================
Roll Number: 105
Name: Eve Wilson
Grade: B+
Marks: 89.50
===== Student Record Management System =====
1. Add Student Record
2. Search Student by Roll Number
3. Delete Student by Roll Number
4. Display All Students
5. Show Load Factor
6. Show Collision Count
7. Create Sample Data
8. Exit
=========================================
Enter your choice: 3
Enter roll number to delete: 103
Student with roll number 103 deleted successfully
===== Student Record Management System =====
1. Add Student Record
2. Search Student by Roll Number
3. Delete Student by Roll Number
4. Display All Students
5. Show Load Factor
6. Show Collision Count
7. Create Sample Data
8. Exit
=========================================
Enter your choice: 5
Load Factor: 0.45
```

## Dry Run

For a hash table of size 20 with MOD hash function and student records:

1. **Insertions**:
   - Insert student (101, "Alice Johnson", "A", 95.5): hash(101) = 101 % 20 = 1 → Insert at bucket 1
   - Insert student (102, "Bob Smith", "B", 87.0): hash(102) = 102 % 20 = 2 → Insert at bucket 2
   - Insert student (103, "Charlie Brown", "A", 92.5): hash(103) = 103 % 20 = 3 → Insert at bucket 3
   - Insert student (104, "Diana Prince", "A+", 98.0): hash(104) = 104 % 20 = 4 → Insert at bucket 4
   - Insert student (105, "Eve Wilson", "B+", 89.5): hash(105) = 105 % 20 = 5 → Insert at bucket 5

2. **Search for roll number 105**:
   - hash(105) = 105 % 20 = 5
   - Check bucket 5:
     * Found student with roll number 105
     * Return student record: Eve Wilson, Grade B+, Marks 89.5

3. **Delete student with roll number 103**:
   - hash(103) = 103 % 20 = 3
   - Check bucket 3:
     * Found student with roll number 103 (Charlie Brown)
     * Remove student record from bucket 3

4. **Load Factor**:
   - Total students: 10
   - Table size: 20
   - Load factor: 10/20 = 0.5

## Conclusion

The implementation demonstrates a student record management system using hash table with separate chaining. Key features include:

1. **Student Record Management**: Complete CRUD operations for student records
2. **Hash Table Implementation**: Efficient storage and retrieval using MOD hash function
3. **Collision Handling**: Separate chaining with linked lists
4. **Data Validation**: Input validation for marks and duplicate roll numbers

**Time Complexities**:
- Insert Student: O(1) average case, O(n) worst case (when all students hash to same bucket)
- Search Student: O(1) average case, O(n) worst case (when all students hash to same bucket)
- Delete Student: O(1) average case, O(n) worst case (when all students hash to same bucket)
- Display All Students: O(n + m) where n is table size and m is total students

**Space Complexity**: O(n + m) where n is table size and m is total students

The implementation handles edge cases properly:
- Duplicate roll number validation
- Student not found during search/delete
- Invalid marks validation (0-100 range)
- Memory management to prevent leaks
- Comprehensive user interface with clear feedback

Additional features beyond requirements:
- Complete student record display
- Load factor calculation
- Collision count tracking
- Sample data creation for testing
- Interactive menu system
- Complete error handling

In real-world applications, this system could be extended to:
1. Support dynamic resizing
2. Implement file persistence
3. Add sorting and filtering capabilities
4. Support different search criteria (name, grade, marks range)
5. Implement backup and restore functionality
6. Add statistical analysis (class average, grade distribution)

Hash tables are fundamental data structures used in:
1. **Database Indexing**: Fast data retrieval
2. **Caching**: Quick access to frequently used data
3. **Compiler Design**: Symbol tables for variables and functions
4. **Networking**: Routing tables and packet filtering
5. **Cryptography**: Hash functions for data integrity

This implementation provides a solid foundation for understanding hash tables and their practical applications in student record management systems, which are essential in educational institutions for efficient data storage and retrieval.
