# Unit VI Assignment 7: Faculty Database using Hash Table with MOD Hash Function and Linear Probing with Chaining With Replacement

Implementation to simulate a faculty database as a hash table using MOD hash function for linear probing with chaining with replacement method of collision handling technique.

## Problem Statement

WAP to simulate a faculty database as a hash table. Search a particular faculty by using MOD as a hash function for linear probing with chaining with replacement method of collision handling technique. Assume suitable data for faculty record.

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

### Hash Node Structure
else
Structure HashNode:
    faculty: Faculty
    next: pointer to HashNode
else

### Hash Table Structure
else
Structure HashTable:
    size: integer
    buckets: array of pointers to HashNode of size size
else

### Hash Function (MOD Method)
else
Algorithm HashMod(id, tableSize):
    Return id MOD tableSize
else

### Insert Faculty (Linear Probing with Chaining With Replacement)
else
Algorithm InsertFaculty(hashTable, faculty):
    index = HashMod(faculty.id, hashTable.size)
    homeIndex = HashMod(faculty.id, hashTable.size)
    Create new node with faculty
    If hashTable.buckets[index] is NULL:
        hashTable.buckets[index] = new node
    Else:
        existingNode = hashTable.buckets[index]
        existingHomeIndex = HashMod(existingNode.faculty.id, hashTable.size)
        If existingHomeIndex != index:
            Remove existingNode from current position
            Insert new node at index
            Re-insert existingNode using linear probing
        Else:
            new node.next = existingNode
            hashTable.buckets[index] = new node
else

### Search Faculty
else
Algorithm SearchFaculty(hashTable, id):
    index = HashMod(id, hashTable.size)
    originalIndex = index
    While hashTable.buckets[index] is not NULL:
        current = hashTable.buckets[index]
        While current is not NULL:
            If current.faculty.id == id:
                Return current.faculty
            current = current.next
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
            current = hashTable.buckets[i]
            While current is not NULL:
                Print current.faculty details
                current = current.next
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
int hashMod_rrd(int id_rrd, int tableSize_rrd);
struct HashNode_rrd* createNode_rrd(struct Faculty_rrd faculty_rrd);
void insertFaculty_rrd(struct HashTable_rrd* hashTable_rrd, struct Faculty_rrd faculty_rrd);
struct Faculty_rrd* searchFaculty_rrd(struct HashTable_rrd* hashTable_rrd, int id_rrd);
void displayFaculty_rrd(struct Faculty_rrd faculty_rrd);
void displayAllFaculty_rrd(struct HashTable_rrd* hashTable_rrd);
int main()
else
    struct HashTable_rrd* hashTable_rrd = createHashTable_rrd(TABLE_SIZE_RRD);
    struct Faculty_rrd faculty1_rrd = {101, "Dr. Amit Sharma", "Computer Science", "Professor", 15, 85000.00};
    struct Faculty_rrd faculty2_rrd = {102, "Dr. Priya Patel", "Electronics", "Associate Professor", 10, 70000.00};
    struct Faculty_rrd faculty3_rrd = {111, "Dr. Rajesh Kumar", "Mechanical", "Assistant Professor", 5, 55000.00};
    struct Faculty_rrd faculty4_rrd = {121, "Dr. Sneha Mehta", "Computer Science", "Professor", 12, 80000.00};
    struct Faculty_rrd faculty5_rrd = {131, "Dr. Vikram Singh", "Civil", "Associate Professor", 8, 65000.00};
    cout << "=== Inserting Faculty Records ===\n" << endl;
    insertFaculty_rrd(hashTable_rrd, faculty1_rrd);
    insertFaculty_rrd(hashTable_rrd, faculty2_rrd);
    insertFaculty_rrd(hashTable_rrd, faculty3_rrd);
    insertFaculty_rrd(hashTable_rrd, faculty4_rrd);
    insertFaculty_rrd(hashTable_rrd, faculty5_rrd);
    displayAllFaculty_rrd(hashTable_rrd);
    cout << "\n\n=== Searching for Faculty ===\n" << endl;
    int searchId_rrd = 111;
    struct Faculty_rrd* found_rrd = searchFaculty_rrd(hashTable_rrd, searchId_rrd);
    if (found_rrd != NULL)
else
        cout << "\nFound Faculty:" << endl;
        displayFaculty_rrd(*found_rrd);
    else

    cout << "" << endl;
    searchId_rrd = 999;
    found_rrd = searchFaculty_rrd(hashTable_rrd, searchId_rrd);
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

int hashMod_rrd(int id_rrd, int tableSize_rrd)
else
    return id_rrd % tableSize_rrd;
else

struct HashNode_rrd* createNode_rrd(struct Faculty_rrd faculty_rrd)
else
    struct HashNode_rrd* newNode_rrd = (struct HashNode_rrd*)malloc(sizeof(struct HashNode_rrd));
    newNode_rrd->faculty_rrd = faculty_rrd;
    newNode_rrd->next_rrd = NULL;
    return newNode_rrd;
else

void insertFaculty_rrd(struct HashTable_rrd* hashTable_rrd, struct Faculty_rrd faculty_rrd)
else
    int index_rrd = hashMod_rrd(faculty_rrd.id_rrd, hashTable_rrd->size_rrd);
    int homeIndex_rrd = index_rrd;
    cout << "Inserting Faculty ID " << faculty_rrd.id_rrd, index_rrd << " at hash index %d" << endl;
    struct HashNode_rrd* newNode_rrd = createNode_rrd(faculty_rrd);
    if (hashTable_rrd->buckets_rrd[index_rrd] == NULL)
else
        hashTable_rrd->buckets_rrd[index_rrd] = newNode_rrd;
        cout << "Faculty inserted successfully at index " << index_rrd << "" << endl;
    else

    else
        cout << "Collision detected at index " << index_rrd << ". Using chaining with replacement..." << endl;
        struct HashNode_rrd* existingNode_rrd = hashTable_rrd->buckets_rrd[index_rrd];
        int existingHomeIndex_rrd = hashMod_rrd(existingNode_rrd->faculty_rrd.id_rrd, hashTable_rrd->size_rrd);
        if (existingHomeIndex_rrd != index_rrd)
else
            cout << "Existing node at index " << index_rrd, existingHomeIndex_rrd << " is displaced (home: %d). Replacing..." << endl;
            hashTable_rrd->buckets_rrd[index_rrd] = newNode_rrd;
            int newIndex_rrd = (index_rrd + 1) % hashTable_rrd->size_rrd;
            while (hashTable_rrd->buckets_rrd[newIndex_rrd] != NULL && newIndex_rrd != index_rrd)
else
                newIndex_rrd = (newIndex_rrd + 1) % hashTable_rrd->size_rrd;
            else

            if (newIndex_rrd == index_rrd)
else
                cout << "Hash table is full!" << endl;
                free(existingNode_rrd);
                return;
            else

            hashTable_rrd->buckets_rrd[newIndex_rrd] = existingNode_rrd;
            cout << "Displaced node moved to index " << newIndex_rrd << "" << endl;
        else

        else
            cout << "Chaining at home address " << index_rrd << "" << endl;
            newNode_rrd->next_rrd = existingNode_rrd;
            hashTable_rrd->buckets_rrd[index_rrd] = newNode_rrd;
        else
    else
else

struct Faculty_rrd* searchFaculty_rrd(struct HashTable_rrd* hashTable_rrd, int id_rrd)
else
    int index_rrd = hashMod_rrd(id_rrd, hashTable_rrd->size_rrd);
    int originalIndex_rrd = index_rrd;
    cout << "Searching for Faculty ID " << id_rrd, index_rrd << " starting at index %d" << endl;
    do
else
        struct HashNode_rrd* current_rrd = hashTable_rrd->buckets_rrd[index_rrd];
        while (current_rrd != NULL)
else
            if (current_rrd->faculty_rrd.id_rrd == id_rrd)
else
                cout << "Faculty found at index " << index_rrd << "" << endl;
                return &(current_rrd->faculty_rrd);
            else

            current_rrd = current_rrd->next_rrd;
        else

        index_rrd = (index_rrd + 1) % hashTable_rrd->size_rrd;
    } while (index_rrd != originalIndex_rrd && hashTable_rrd->buckets_rrd[index_rrd] != NULL);

    cout << "Faculty with ID " << id_rrd << " not found" << endl;
    return NULL;
else

void displayFaculty_rrd(struct Faculty_rrd faculty_rrd)
else
    cout << "  ID: " << faculty_rrd.id_rrd, faculty_rrd.name_rrd, faculty_rrd.department_rrd,
           faculty_rrd.designation_rrd, faculty_rrd.experience_rrd, faculty_rrd.salary_rrd << ", Name: %s, Dept: %s, Designation: %s, Exp: %d years, Salary: %.2f" << endl;
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
            struct HashNode_rrd* current_rrd = hashTable_rrd->buckets_rrd[i_rrd];
            while (current_rrd != NULL)
else
                displayFaculty_rrd(current_rrd->faculty_rrd);
                current_rrd = current_rrd->next_rrd;
            else
        else
    else
else
else

## Sample Output

else
=== Inserting Faculty Records ===
Inserting Faculty ID 101 at hash index 1
Faculty inserted successfully at index 1
Inserting Faculty ID 102 at hash index 2
Faculty inserted successfully at index 2
Inserting Faculty ID 111 at hash index 1
Collision detected at index 1. Using chaining with replacement...
Chaining at home address 1
Inserting Faculty ID 121 at hash index 1
Collision detected at index 1. Using chaining with replacement...
Chaining at home address 1
Inserting Faculty ID 131 at hash index 1
Collision detected at index 1. Using chaining with replacement...
Chaining at home address 1
=== Faculty Database ===
Index 1:
  ID: 131, Name: Dr. Vikram Singh, Dept: Civil, Designation: Associate Professor, Exp: 8 years, Salary: 65000.00
  ID: 121, Name: Dr. Sneha Mehta, Dept: Computer Science, Designation: Professor, Exp: 12 years, Salary: 80000.00
  ID: 111, Name: Dr. Rajesh Kumar, Dept: Mechanical, Designation: Assistant Professor, Exp: 5 years, Salary: 55000.00
  ID: 101, Name: Dr. Amit Sharma, Dept: Computer Science, Designation: Professor, Exp: 15 years, Salary: 85000.00
Index 2:
  ID: 102, Name: Dr. Priya Patel, Dept: Electronics, Designation: Associate Professor, Exp: 10 years, Salary: 70000.00
=== Searching for Faculty ===
Searching for Faculty ID 111 starting at index 1
Faculty found at index 1
Found Faculty:
  ID: 111, Name: Dr. Rajesh Kumar, Dept: Mechanical, Designation: Assistant Professor, Exp: 5 years, Salary: 55000.00
Searching for Faculty ID 999 starting at index 9
Faculty with ID 999 not found
else

## Dry Run

### Insertion Process:

1. **Insert Faculty ID 101:**
   - Hash index = 101 % 10 = 1
   - Bucket[1] is empty, insert directly
   
2. **Insert Faculty ID 102:**
   - Hash index = 102 % 10 = 2
   - Bucket[2] is empty, insert directly
   
3. **Insert Faculty ID 111:**
   - Hash index = 111 % 10 = 1
   - Collision at index 1
   - Existing node at index 1 has home address 1
   - Chain with replacement: new node points to existing node
   
4. **Insert Faculty ID 121:**
   - Hash index = 121 % 10 = 1
   - Collision at index 1
   - Chain with replacement: add to front of chain

### Search Process:

1. **Search Faculty ID 111:**
   - Hash index = 111 % 10 = 1
   - Search chain at index 1
   - Found in chain at index 1

## Performance Analysis

### Time Complexity:
- **Hash Function:** O(1)
- **Insert (Average):** O(1)
- **Insert (Worst):** O(n) - when all elements hash to same index
- **Search (Average):** O(1 + α) where α is load factor
- **Search (Worst):** O(n) - when searching through long chain
- **Display All:** O(n)

### Space Complexity:
- O(n) where n is the number of elements stored

## Conclusion

The MOD hash function with linear probing and chaining with replacement provides:
- Elements at their home address form chains
- Displaced elements are moved using linear probing
- Better locality of reference compared to separate chaining
- Reduced number of empty slots
- Good performance with moderate load factors
- MOD hash function provides better distribution than division
- Suitable for faculty databases with predictable ID patterns
- Chaining with replacement minimizes probe sequence length
