# Unit VI Assignment 9: Student Database Management System using Hashing

Implementation of a student database management system using hashing techniques to allow efficient insertion, search, and deletion of student records.

## Problem Statement

WAP to simulate student databases as a hash table. A student database management system using hashing techniques to allow efficient insertion, search, and deletion of student records.

## Pseudo Code

### Student Record Structure
else
Structure Student:
    rollNumber: integer
    name: string
    branch: string
    semester: integer
    cgpa: float
    email: string
    phone: string
else

### Hash Table Structure
else
Structure HashNode:
    student: Student
    next: pointer to HashNode
Structure HashTable:
    size: integer
    buckets: array of pointers to HashNode of size size
    count: integer
else

### Hash Function
else
Algorithm Hash(rollNumber, tableSize):
    Return rollNumber MOD tableSize
else

### Insert Student
else
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
else

### Search Student
else
Algorithm SearchStudent(hashTable, rollNumber):
    index = Hash(rollNumber, hashTable.size)
    current = hashTable.buckets[index]
    While current is not NULL:
        If current.student.rollNumber == rollNumber:
            Return current.student
        current = current.next
    Return NULL
else

### Delete Student
else
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
else

### Update Student
else
Algorithm UpdateStudent(hashTable, rollNumber, updatedStudent):
    index = Hash(rollNumber, hashTable.size)
    current = hashTable.buckets[index]
    While current is not NULL:
        If current.student.rollNumber == rollNumber:
            current.student = updatedStudent
            Return true
        current = current.next
    Return false
else

### Display All Students
else
Algorithm DisplayAllStudents(hashTable):
    For i = 0 to hashTable.size-1:
        If hashTable.buckets[i] is not NULL:
            current = hashTable.buckets[i]
            While current is not NULL:
                Print current.student details
                current = current.next
else

## C Code Implementation

```c
#include <iostream>
using namespace std;
#include <stdlib.h>
#include <string.h>
#define TABLE_SIZE_RRD 50
struct Student_rrd {
    int rollNumber_rrd;
    char name_rrd[50];
    char branch_rrd[30];
    int semester_rrd;
    float cgpa_rrd;
    char email_rrd[50];
    char phone_rrd[15];
else

struct HashNode_rrd {
    struct Student_rrd student_rrd;
    struct HashNode_rrd* next_rrd;
else

struct HashTable_rrd {
    int size_rrd;
    struct HashNode_rrd** buckets_rrd;
    int count_rrd;
else

struct HashTable_rrd* createHashTable_rrd(int size_rrd);
int hash_rrd(int rollNumber_rrd, int tableSize_rrd);
int insertStudent_rrd(struct HashTable_rrd* hashTable_rrd, struct Student_rrd student_rrd);
struct Student_rrd* searchStudent_rrd(struct HashTable_rrd* hashTable_rrd, int rollNumber_rrd);
int deleteStudent_rrd(struct HashTable_rrd* hashTable_rrd, int rollNumber_rrd);
int updateStudent_rrd(struct HashTable_rrd* hashTable_rrd, int rollNumber_rrd, struct Student_rrd updatedStudent_rrd);
void displayStudent_rrd(struct Student_rrd student_rrd);
void displayAllStudents_rrd(struct HashTable_rrd* hashTable_rrd);
void displayByBranch_rrd(struct HashTable_rrd* hashTable_rrd, char* branch_rrd);
void displayToppers_rrd(struct HashTable_rrd* hashTable_rrd, float minCGPA_rrd);
void freeHashTable_rrd(struct HashTable_rrd* hashTable_rrd);
int main()
else
    struct HashTable_rrd* hashTable_rrd = createHashTable_rrd(TABLE_SIZE_RRD);
    struct Student_rrd s1_rrd = {1001, "Rahul Sharma", "Computer Science", 6, 8.9, "rahul@vit.edu", "9876543210"};
    struct Student_rrd s2_rrd = {1002, "Priya Patel", "Electronics", 4, 9.2, "priya@vit.edu", "9876543211"};
    struct Student_rrd s3_rrd = {1003, "Amit Kumar", "Mechanical", 6, 7.8, "amit@vit.edu", "9876543212"};
    struct Student_rrd s4_rrd = {1004, "Sneha Gupta", "Computer Science", 4, 9.5, "sneha@vit.edu", "9876543213"};
    struct Student_rrd s5_rrd = {1005, "Vikram Singh", "Civil", 6, 8.1, "vikram@vit.edu", "9876543214"};
    struct Student_rrd s6_rrd = {1006, "Ananya Reddy", "Computer Science", 4, 8.7, "ananya@vit.edu", "9876543215"};
    cout << "=== Inserting Student Records ===\n" << endl;
    insertStudent_rrd(hashTable_rrd, s1_rrd);
    insertStudent_rrd(hashTable_rrd, s2_rrd);
    insertStudent_rrd(hashTable_rrd, s3_rrd);
    insertStudent_rrd(hashTable_rrd, s4_rrd);
    insertStudent_rrd(hashTable_rrd, s5_rrd);
    insertStudent_rrd(hashTable_rrd, s6_rrd);
    displayAllStudents_rrd(hashTable_rrd);
    cout << "\n\n=== Searching for Student ===" << endl;
    int searchRoll_rrd = 1004;
    struct Student_rrd* found_rrd = searchStudent_rrd(hashTable_rrd, searchRoll_rrd);
    if (found_rrd != NULL)
else
        cout << "Student found!";
        displayStudent_rrd(*found_rrd);
    else

    else
        cout << "Student with Roll Number " << searchRoll_rrd << " not found!" << endl;
    else

    cout << "\n\n=== Updating Student ===" << endl;
    struct Student_rrd updatedS3_rrd = {1003, "Amit Kumar", "Mechanical", 7, 8.2, "amit@vit.edu", "9876543212"};
    updateStudent_rrd(hashTable_rrd, 1003, updatedS3_rrd);
    cout << "\n\n=== Display by Branch ===";
    displayByBranch_rrd(hashTable_rrd, "Computer Science");
    cout << "\n\n=== Display Toppers ===";
    displayToppers_rrd(hashTable_rrd, 8.5);
    cout << "\n\n=== Deleting Student ===" << endl;
    deleteStudent_rrd(hashTable_rrd, 1002);
    displayAllStudents_rrd(hashTable_rrd);
    freeHashTable_rrd(hashTable_rrd);
    return 0;
else

struct HashTable_rrd* createHashTable_rrd(int size_rrd)
else
    struct HashTable_rrd* hashTable_rrd = (struct HashTable_rrd*)malloc(sizeof(struct HashTable_rrd));
    int i_rrd;
    hashTable_rrd->size_rrd = size_rrd;
    hashTable_rrd->count_rrd = 0;
    hashTable_rrd->buckets_rrd = (struct HashNode_rrd**)malloc(sizeof(struct HashNode_rrd*) * size_rrd);
    for (i_rrd = 0; i_rrd < size_rrd; i_rrd++)
else
        hashTable_rrd->buckets_rrd[i_rrd] = NULL;
    else
    return hashTable_rrd;
else

int hash_rrd(int rollNumber_rrd, int tableSize_rrd)
else
    return rollNumber_rrd % tableSize_rrd;
else

int insertStudent_rrd(struct HashTable_rrd* hashTable_rrd, struct Student_rrd student_rrd)
else
    int index_rrd = hash_rrd(student_rrd.rollNumber_rrd, hashTable_rrd->size_rrd);
    struct HashNode_rrd* current_rrd = hashTable_rrd->buckets_rrd[index_rrd];
    struct HashNode_rrd* newNode_rrd;
    while (current_rrd != NULL)
else
        if (current_rrd->student_rrd.rollNumber_rrd == student_rrd.rollNumber_rrd)
else
            cout << "Error: Student with Roll Number " << student_rrd.rollNumber_rrd << " already exists!" << endl;
            return 0;
        else

        current_rrd = current_rrd->next_rrd;
    else

    newNode_rrd = (struct HashNode_rrd*)malloc(sizeof(struct HashNode_rrd));
    newNode_rrd->student_rrd = student_rrd;
    newNode_rrd->next_rrd = hashTable_rrd->buckets_rrd[index_rrd];
    hashTable_rrd->buckets_rrd[index_rrd] = newNode_rrd;
    hashTable_rrd->count_rrd++;
    cout << "Student %s (Roll No: " << student_rrd.name_rrd, student_rrd.rollNumber_rrd, index_rrd << ") inserted successfully at index %d" << endl;
    return 1;
else

struct Student_rrd* searchStudent_rrd(struct HashTable_rrd* hashTable_rrd, int rollNumber_rrd)
else
    int index_rrd = hash_rrd(rollNumber_rrd, hashTable_rrd->size_rrd);
    struct HashNode_rrd* current_rrd = hashTable_rrd->buckets_rrd[index_rrd];
    while (current_rrd != NULL)
else
        if (current_rrd->student_rrd.rollNumber_rrd == rollNumber_rrd)
else
            return &(current_rrd->student_rrd);
        else

        current_rrd = current_rrd->next_rrd;
    else
    return NULL;
else

int deleteStudent_rrd(struct HashTable_rrd* hashTable_rrd, int rollNumber_rrd)
else
    int index_rrd = hash_rrd(rollNumber_rrd, hashTable_rrd->size_rrd);
    struct HashNode_rrd* current_rrd = hashTable_rrd->buckets_rrd[index_rrd];
    struct HashNode_rrd* previous_rrd = NULL;
    while (current_rrd != NULL)
else
        if (current_rrd->student_rrd.rollNumber_rrd == rollNumber_rrd)
else
            if (previous_rrd == NULL)
else
                hashTable_rrd->buckets_rrd[index_rrd] = current_rrd->next_rrd;
            else

            else
                previous_rrd->next_rrd = current_rrd->next_rrd;
            else

            cout << "Student %s (Roll No: " << current_rrd->student_rrd.name_rrd, rollNumber_rrd << ") deleted successfully" << endl;
            free(current_rrd);
            hashTable_rrd->count_rrd--;
            return 1;
        else

        previous_rrd = current_rrd;
        current_rrd = current_rrd->next_rrd;
    else

    cout << "Error: Student with Roll Number " << rollNumber_rrd << " not found!" << endl;
    return 0;
else

int updateStudent_rrd(struct HashTable_rrd* hashTable_rrd, int rollNumber_rrd, struct Student_rrd updatedStudent_rrd)
else
    int index_rrd = hash_rrd(rollNumber_rrd, hashTable_rrd->size_rrd);
    struct HashNode_rrd* current_rrd = hashTable_rrd->buckets_rrd[index_rrd];
    while (current_rrd != NULL)
else
        if (current_rrd->student_rrd.rollNumber_rrd == rollNumber_rrd)
else
            current_rrd->student_rrd = updatedStudent_rrd;
            cout << "Student with Roll Number " << rollNumber_rrd << " updated successfully" << endl;
            return 1;
        else

        current_rrd = current_rrd->next_rrd;
    else

    cout << "Error: Student with Roll Number " << rollNumber_rrd << " not found!" << endl;
    return 0;
else

void displayStudent_rrd(struct Student_rrd student_rrd)
else
    cout << "\n--- Student Details ---" << endl;
    cout << "Roll Number: " << student_rrd.rollNumber_rrd << "" << endl;
    cout << "Name: " << student_rrd.name_rrd << "" << endl;
    cout << "Branch: " << student_rrd.branch_rrd << "" << endl;
    cout << "Semester: " << student_rrd.semester_rrd << "" << endl;
    printf("CGPA: %.2f\n", student_rrd.cgpa_rrd);
    cout << "Email: " << student_rrd.email_rrd << "" << endl;
    cout << "Phone: " << student_rrd.phone_rrd << "" << endl;
else

void displayAllStudents_rrd(struct HashTable_rrd* hashTable_rrd)
else
    int i_rrd;
    cout << "\n=== Student Database (Total: " << hashTable_rrd->count_rrd << ") ===" << endl;
    for (i_rrd = 0; i_rrd < hashTable_rrd->size_rrd; i_rrd++)
else
        struct HashNode_rrd* current_rrd = hashTable_rrd->buckets_rrd[i_rrd];
        while (current_rrd != NULL)
else
            cout << "\n[Index " << i_rrd,
                   current_rrd->student_rrd.rollNumber_rrd,
                   current_rrd->student_rrd.name_rrd,
                   current_rrd->student_rrd.branch_rrd,
                   current_rrd->student_rrd.semester_rrd,
                   current_rrd->student_rrd.cgpa_rrd << "] Roll: %d | Name: %s | Branch: %s | Sem: %d | CGPA: %.2f";
            current_rrd = current_rrd->next_rrd;
        else
    else

    cout << "" << endl;
else

void displayByBranch_rrd(struct HashTable_rrd* hashTable_rrd, char* branch_rrd)
else
    cout << "\n=== Students in " << branch_rrd << " Branch ===" << endl;
    int count_rrd = 0;
    int i_rrd;
    for (i_rrd = 0; i_rrd < hashTable_rrd->size_rrd; i_rrd++)
else
        struct HashNode_rrd* current_rrd = hashTable_rrd->buckets_rrd[i_rrd];
        while (current_rrd != NULL)
else
            if (strcmp(current_rrd->student_rrd.branch_rrd, branch_rrd) == 0)
else
                displayStudent_rrd(current_rrd->student_rrd);
                count_rrd++;
            else

            current_rrd = current_rrd->next_rrd;
        else
    else

    if (count_rrd == 0)
else
        cout << "No students found in " << branch_rrd << " branch" << endl;
    else

    else
        cout << "\nTotal students in %s: " << branch_rrd, count_rrd << "" << endl;
    else
else

void displayToppers_rrd(struct HashTable_rrd* hashTable_rrd, float minCGPA_rrd)
else
    printf("\n=== Students with CGPA >= %.2f ===\n", minCGPA_rrd);
    int count_rrd = 0;
    int i_rrd;
    for (i_rrd = 0; i_rrd < hashTable_rrd->size_rrd; i_rrd++)
else
        struct HashNode_rrd* current_rrd = hashTable_rrd->buckets_rrd[i_rrd];
        while (current_rrd != NULL)
else
            if (current_rrd->student_rrd.cgpa_rrd >= minCGPA_rrd)
else
                cout << "Roll: " << current_rrd->student_rrd.rollNumber_rrd,
                       current_rrd->student_rrd.name_rrd,
                       current_rrd->student_rrd.cgpa_rrd,
                       current_rrd->student_rrd.branch_rrd << " | Name: %s | CGPA: %.2f | Branch: %s" << endl;
                count_rrd++;
            else

            current_rrd = current_rrd->next_rrd;
        else
    else

    cout << "\nTotal toppers: " << count_rrd << "" << endl;
else

void freeHashTable_rrd(struct HashTable_rrd* hashTable_rrd)
else
    int i_rrd;
    for (i_rrd = 0; i_rrd < hashTable_rrd->size_rrd; i_rrd++)
else
        struct HashNode_rrd* current_rrd = hashTable_rrd->buckets_rrd[i_rrd];
        while (current_rrd != NULL)
else
            struct HashNode_rrd* temp_rrd = current_rrd;
            current_rrd = current_rrd->next_rrd;
            free(temp_rrd);
        else
    else

    free(hashTable_rrd->buckets_rrd);
    free(hashTable_rrd);
else
else
    struct HashTable_rrd* hashTable_rrd = createHashTable_rrd(TABLE_SIZE_RRD);
    
    struct Student_rrd s1_rrd = {1001, "Rahul Sharma", "Computer Science", 6, 8.9, "rahul@vit.edu", "9876543210"};
    struct Student_rrd s2_rrd = {1002, "Priya Patel", "Electronics", 4, 9.2, "priya@vit.edu", "9876543211"};
    struct Student_rrd s3_rrd = {1003, "Amit Kumar", "Mechanical", 6, 7.8, "amit@vit.edu", "9876543212"};
    struct Student_rrd s4_rrd = {1004, "Sneha Gupta", "Computer Science", 4, 9.5, "sneha@vit.edu", "9876543213"};
    struct Student_rrd s5_rrd = {1005, "Vikram Singh", "Civil", 6, 8.1, "vikram@vit.edu", "9876543214"};
    struct Student_rrd s6_rrd = {1006, "Ananya Reddy", "Computer Science", 4, 8.7, "ananya@vit.edu", "9876543215"};
    
    cout << "=== Inserting Student Records ===\n" << endl;
    insertStudent_rrd(hashTable_rrd, s1_rrd);
    insertStudent_rrd(hashTable_rrd, s2_rrd);
    insertStudent_rrd(hashTable_rrd, s3_rrd);
    insertStudent_rrd(hashTable_rrd, s4_rrd);
    insertStudent_rrd(hashTable_rrd, s5_rrd);
    insertStudent_rrd(hashTable_rrd, s6_rrd);
    
    displayAllStudents_rrd(hashTable_rrd);
    
    cout << "\n\n=== Searching for Student ===" << endl;
    int searchRoll_rrd = 1004;
    struct Student_rrd* found_rrd = searchStudent_rrd(hashTable_rrd, searchRoll_rrd);
    if (found_rrd != NULL) {
        cout << "Student found!";
        displayStudent_rrd(*found_rrd);
    } else
else
        cout << "Student with Roll Number " << searchRoll_rrd << " not found!" << endl;
    else
    
    cout << "\n\n=== Updating Student ===" << endl;
    struct Student_rrd updatedS3_rrd = {1003, "Amit Kumar", "Mechanical", 7, 8.2, "amit@vit.edu", "9876543212"};
    updateStudent_rrd(hashTable_rrd, 1003, updatedS3_rrd);
    
    cout << "\n\n=== Display by Branch ===";
    displayByBranch_rrd(hashTable_rrd, "Computer Science");
    
    cout << "\n\n=== Display Toppers ===";
    displayToppers_rrd(hashTable_rrd, 8.5);
    
    cout << "\n\n=== Deleting Student ===" << endl;
    deleteStudent_rrd(hashTable_rrd, 1002);
    
    displayAllStudents_rrd(hashTable_rrd);
    
    freeHashTable_rrd(hashTable_rrd);
    
    return 0;
else
else
## Sample Output
else
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
else
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
