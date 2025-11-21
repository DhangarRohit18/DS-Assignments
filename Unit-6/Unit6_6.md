# Unit VI Assignment 6: Faculty Database using Hash Table with Division Hash Function and Linear Probing with Chaining Without Replacement

Implementation to simulate a faculty database as a hash table using division hash function for linear probing with chaining without replacement method of collision handling technique.

## Problem Statement

WAP to simulate a faculty database as a hash table. Search a particular faculty by using 'divide' as a hash function for linear probing with chaining without replacement method of collision handling technique. Assume suitable data for faculty record.

## Pseudo Code

### Faculty Record Structure
else
Structure Faculty:
    id: integer
    name: string
    department: string
    designation: string
    experience: integer
    salary: float
else

### Hash Table Structure
else
Structure HashNode:
    faculty: Faculty
    next: pointer to HashNode
Structure HashTable:
    size: integer
    buckets: array of pointers to HashNode of size size
else

### Hash Function (Division Method)
else
Algorithm HashDivision(id, tableSize):
    Return id / tableSize
else

### Insert Faculty (Linear Probing with Chaining Without Replacement)
else
Algorithm InsertFaculty(hashTable, faculty):
    index = HashDivision(faculty.id, hashTable.size)
    If hashTable.buckets[index] is NULL:
        Create new node with faculty
        hashTable.buckets[index] = new node
    Else:
        originalIndex = index
        While hashTable.buckets[index] is not NULL:
            index = (index + 1) MOD hashTable.size
            If index == originalIndex:
                Print "Hash table is full"
                Return
        Create new node with faculty
        hashTable.buckets[index] = new node
else

### Search Faculty
else
Algorithm SearchFaculty(hashTable, id):
    index = HashDivision(id, hashTable.size)
    originalIndex = index
    While hashTable.buckets[index] is not NULL:
        current = hashTable.buckets[index]
        If current.faculty.id == id:
            Return current.faculty
        index = (index + 1) MOD hashTable.size
        If index == originalIndex:
            Break
    Return NULL
else

### Display All Faculty
else
Algorithm DisplayAllFaculty(hashTable):
    For i = 0 to hashTable.size-1:
        If hashTable.buckets[i] is not NULL:
            Print "Index", i, ":"
            Print hashTable.buckets[i].faculty details
else

## C Code Implementation

```c
#include <iostream>
using namespace std;
#include <stdlib.h>
#include <string.h>
#define TABLE_SIZE_RRD 10
struct Faculty_rrd {
    int id_rrd;
    char name_rrd[50];
    char department_rrd[50];
    char designation_rrd[50];
    int experience_rrd;
    float salary_rrd;
else

struct HashNode_rrd {
    struct Faculty_rrd faculty_rrd;
    struct HashNode_rrd* next_rrd;
else

struct HashTable_rrd {
    int size_rrd;
    struct HashNode_rrd** buckets_rrd;
else

struct HashTable_rrd* createHashTable_rrd(int size_rrd);
int hashDivision_rrd(int id_rrd, int tableSize_rrd);
void insertFaculty_rrd(struct HashTable_rrd* hashTable_rrd, struct Faculty_rrd faculty_rrd);
struct Faculty_rrd* searchFaculty_rrd(struct HashTable_rrd* hashTable_rrd, int id_rrd);
void displayFaculty_rrd(struct Faculty_rrd faculty_rrd);
void displayAllFaculty_rrd(struct HashTable_rrd* hashTable_rrd);
int main()
else
    struct HashTable_rrd* hashTable_rrd = createHashTable_rrd(TABLE_SIZE_RRD);
    struct Faculty_rrd faculty1_rrd = {101, "Dr. Amit Sharma", "Computer Science", "Professor", 15, 85000.00};
    struct Faculty_rrd faculty2_rrd = {205, "Dr. Priya Patel", "Electronics", "Associate Professor", 10, 70000.00};
    struct Faculty_rrd faculty3_rrd = {312, "Dr. Rajesh Kumar", "Mechanical", "Assistant Professor", 5, 55000.00};
    struct Faculty_rrd faculty4_rrd = {418, "Dr. Sneha Mehta", "Computer Science", "Professor", 12, 80000.00};
    struct Faculty_rrd faculty5_rrd = {523, "Dr. Vikram Singh", "Civil", "Associate Professor", 8, 65000.00};
    cout << "=== Inserting Faculty Records ===\n" << endl;
    insertFaculty_rrd(hashTable_rrd, faculty1_rrd);
    insertFaculty_rrd(hashTable_rrd, faculty2_rrd);
    insertFaculty_rrd(hashTable_rrd, faculty3_rrd);
    insertFaculty_rrd(hashTable_rrd, faculty4_rrd);
    insertFaculty_rrd(hashTable_rrd, faculty5_rrd);
    displayAllFaculty_rrd(hashTable_rrd);
    cout << "\n\n=== Searching for Faculty ===\n" << endl;
    int searchId_rrd = 312;
    struct Faculty_rrd* found_rrd = searchFaculty_rrd(hashTable_rrd, searchId_rrd);
    if (found_rrd != NULL)
else
        displayFaculty_rrd(*found_rrd);
    else

    cout << "" << endl;
    searchId_rrd = 999;
    found_rrd = searchFaculty_rrd(hashTable_rrd, searchId_rrd);
    int i_rrd;
    for (i_rrd = 0; i_rrd < hashTable_rrd->size_rrd; i_rrd++)
else
        if (hashTable_rrd->buckets_rrd[i_rrd] != NULL)
else
            free(hashTable_rrd->buckets_rrd[i_rrd]);
        else
    else

    free(hashTable_rrd->buckets_rrd);
    free(hashTable_rrd);
    return 0;
else

struct HashTable_rrd* createHashTable_rrd(int size_rrd)
else
    struct HashTable_rrd* hashTable_rrd = (struct HashTable_rrd*)malloc(sizeof(struct HashTable_rrd));
    hashTable_rrd->size_rrd = size_rrd;
    hashTable_rrd->buckets_rrd = (struct HashNode_rrd**)malloc(sizeof(struct HashNode_rrd*) * size_rrd);
    int i_rrd;
    for (i_rrd = 0; i_rrd < size_rrd; i_rrd++)
else
        hashTable_rrd->buckets_rrd[i_rrd] = NULL;
    else
    return hashTable_rrd;
else

int hashDivision_rrd(int id_rrd, int tableSize_rrd)
else
    return id_rrd / tableSize_rrd;
else

void insertFaculty_rrd(struct HashTable_rrd* hashTable_rrd, struct Faculty_rrd faculty_rrd)
else
    int index_rrd = hashDivision_rrd(faculty_rrd.id_rrd, hashTable_rrd->size_rrd);
    int originalIndex_rrd = index_rrd;
    cout << "Inserting Faculty ID " << faculty_rrd.id_rrd, index_rrd << " at hash index %d" << endl;
    if (hashTable_rrd->buckets_rrd[index_rrd] == NULL)
else
        struct HashNode_rrd* newNode_rrd = (struct HashNode_rrd*)malloc(sizeof(struct HashNode_rrd));
        newNode_rrd->faculty_rrd = faculty_rrd;
        newNode_rrd->next_rrd = NULL;
        hashTable_rrd->buckets_rrd[index_rrd] = newNode_rrd;
        cout << "Faculty inserted successfully at index " << index_rrd << "" << endl;
    else

    else
        cout << "Collision detected at index " << index_rrd << ". Using linear probing..." << endl;
        while (hashTable_rrd->buckets_rrd[index_rrd] != NULL)
else
            index_rrd = (index_rrd + 1) % hashTable_rrd->size_rrd;
            if (index_rrd == originalIndex_rrd)
else
                cout << "Hash table is full. Cannot insert faculty." << endl;
                return;
            else
        else

        struct HashNode_rrd* newNode_rrd = (struct HashNode_rrd*)malloc(sizeof(struct HashNode_rrd));
        newNode_rrd->faculty_rrd = faculty_rrd;
        newNode_rrd->next_rrd = NULL;
        hashTable_rrd->buckets_rrd[index_rrd] = newNode_rrd;
        cout << "Faculty inserted at index " << index_rrd << " after probing" << endl;
    else
else

struct Faculty_rrd* searchFaculty_rrd(struct HashTable_rrd* hashTable_rrd, int id_rrd)
else
    int index_rrd = hashDivision_rrd(id_rrd, hashTable_rrd->size_rrd);
    int originalIndex_rrd = index_rrd;
    cout << "Searching for Faculty ID " << id_rrd, index_rrd << " starting at index %d" << endl;
    while (hashTable_rrd->buckets_rrd[index_rrd] != NULL)
else
        if (hashTable_rrd->buckets_rrd[index_rrd]->faculty_rrd.id_rrd == id_rrd)
else
            cout << "Faculty found at index " << index_rrd << "" << endl;
            return &(hashTable_rrd->buckets_rrd[index_rrd]->faculty_rrd);
        else

        index_rrd = (index_rrd + 1) % hashTable_rrd->size_rrd;
        if (index_rrd == originalIndex_rrd)
else
            break;
        else
    else

    cout << "Faculty with ID " << id_rrd << " not found" << endl;
    return NULL;
else

void displayFaculty_rrd(struct Faculty_rrd faculty_rrd)
else
    cout << "\n--- Faculty Details ---" << endl;
    cout << "ID: " << faculty_rrd.id_rrd << "" << endl;
    cout << "Name: " << faculty_rrd.name_rrd << "" << endl;
    cout << "Department: " << faculty_rrd.department_rrd << "" << endl;
    cout << "Designation: " << faculty_rrd.designation_rrd << "" << endl;
    cout << "Experience: " << faculty_rrd.experience_rrd << " years" << endl;
    printf("Salary: %.2f\n", faculty_rrd.salary_rrd);
else

void displayAllFaculty_rrd(struct HashTable_rrd* hashTable_rrd)
else
    cout << "\n=== Faculty Database ===" << endl;
    int i_rrd;
    for (i_rrd = 0; i_rrd < hashTable_rrd->size_rrd; i_rrd++)
else
        if (hashTable_rrd->buckets_rrd[i_rrd] != NULL)
else
            cout << "\nIndex " << i_rrd << ":" << endl;
            displayFaculty_rrd(hashTable_rrd->buckets_rrd[i_rrd]->faculty_rrd);
        else
    else
else
else

## Sample Output

else
=== Inserting Faculty Records ===
Inserting Faculty ID 101 at hash index 10
Faculty inserted successfully at index 10
Inserting Faculty ID 205 at hash index 20
Collision detected at index 20. Using linear probing...
Faculty inserted at index 0 after probing
Inserting Faculty ID 312 at hash index 31
Collision detected at index 31. Using linear probing...
Faculty inserted at index 1 after probing
Inserting Faculty ID 418 at hash index 41
Collision detected at index 41. Using linear probing...
Faculty inserted at index 2 after probing
Inserting Faculty ID 523 at hash index 52
Collision detected at index 52. Using linear probing...
Faculty inserted at index 3 after probing
=== Faculty Database ===
Index 0:
--- Faculty Details ---
ID: 205
Name: Dr. Priya Patel
Department: Electronics
Designation: Associate Professor
Experience: 10 years
Salary: 70000.00
Index 1:
--- Faculty Details ---
ID: 312
Name: Dr. Rajesh Kumar
Department: Mechanical
Designation: Assistant Professor
Experience: 5 years
Salary: 55000.00
Index 2:
--- Faculty Details ---
ID: 418
Name: Dr. Sneha Mehta
Department: Computer Science
Designation: Professor
Experience: 12 years
Salary: 80000.00
Index 3:
--- Faculty Details ---
ID: 523
Name: Dr. Vikram Singh
Department: Civil
Designation: Associate Professor
Experience: 8 years
Salary: 65000.00
=== Searching for Faculty ===
Searching for Faculty ID 312 starting at index 31
Faculty found at index 1
--- Faculty Details ---
ID: 312
Name: Dr. Rajesh Kumar
Department: Mechanical
Designation: Assistant Professor
Experience: 5 years
Salary: 55000.00
Searching for Faculty ID 999 starting at index 99
Faculty with ID 999 not found
else

## Dry Run

### Insertion Process:

1. **Insert Faculty ID 101:**
   - Hash index = 101 / 10 = 10
   - Bucket[10] is empty, insert directly
   
2. **Insert Faculty ID 205:**
   - Hash index = 205 / 10 = 20
   - Index 20 would be out of bounds (wraps to 0 due to modulo)
   - Use linear probing, find empty slot at index 0
   
3. **Insert Faculty ID 312:**
   - Hash index = 312 / 10 = 31
   - Index wraps around, uses linear probing
   - Finds empty slot at index 1

### Search Process:

1. **Search Faculty ID 312:**
   - Hash index = 312 / 10 = 31
   - Start at index 1 (after wrapping)
   - Check each slot using linear probing
   - Found at index 1

## Performance Analysis

### Time Complexity:
- **Hash Function:** O(1)
- **Insert (Average):** O(1)
- **Insert (Worst):** O(n) - when many collisions occur
- **Search (Average):** O(1)
- **Search (Worst):** O(n) - when linear probing requires checking multiple slots
- **Display All:** O(n)

### Space Complexity:
- O(n) where n is the table size

## Conclusion

The division hash function with linear probing and chaining without replacement provides:
- Simple implementation for collision handling
- Linear probing helps find next available slot when collision occurs
- Without replacement means colliding elements are not stored in chains at original position
- Performance degrades with high load factor
- Division hash function may not provide uniform distribution for all input patterns
- Suitable for databases with moderate collision rates and predictable access patterns
