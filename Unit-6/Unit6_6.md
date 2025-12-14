# Unit VI Assignment 6: Faculty Database using Hash Table with Division Hash Function and Linear Probing with Chaining Without Replacement

Implementation to simulate a faculty database as a hash table using division hash function for linear probing with chaining without replacement method of collision handling technique.

## Problem Statement

WAP to simulate a faculty database as a hash table. Search a particular faculty by using 'divide' as a hash function for linear probing with chaining without replacement method of collision handling technique. Assume suitable data for faculty record.

## Pseudo Code

### Faculty Record Structure
```
Structure Faculty:
    id: integer
    name: string
    department: string
    designation: string
    experience: integer
    salary: float
```

### Hash Table Structure
```
Structure HashNode:
    faculty: Faculty
    next: pointer to HashNode
    
Structure HashTable:
    size: integer
    buckets: array of pointers to HashNode of size size
```

### Hash Function (Division Method)
```
Algorithm HashDivision(id, tableSize):
    Return id MOD tableSize
```

### Insert Faculty (Linear Probing with Chaining Without Replacement)
```
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
```

### Search Faculty
```
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
```

### Display All Faculty
```
Algorithm DisplayAllFaculty(hashTable):
    For i = 0 to hashTable.size-1:
        If hashTable.buckets[i] is not NULL:
            Print "Index", i, ":"
            Print hashTable.buckets[i].faculty details
```

## C++ Code Implementation

```cpp
#include <iostream>
#include <cstring>
using namespace std;

#define TABLE_SIZE 10

struct Faculty {
    int id;
    char name[50];
    char department[50];
    char designation[50];
    int experience;
    float salary;
};

struct HashNode {
    Faculty faculty;
    HashNode* next;
};

struct HashTable {
    int size;
    HashNode** buckets;
};

HashTable* createHashTable(int size) {
    HashTable* hashTable = new HashTable;
    hashTable->size = size;
    hashTable->buckets = new HashNode*[size];
    
    for (int i = 0; i < size; i++) {
        hashTable->buckets[i] = nullptr;
    }
    
    return hashTable;
}

int hashDivision(int id, int tableSize) {
    return id % tableSize;
}

void insertFaculty(HashTable* hashTable, Faculty faculty) {
    int index = hashDivision(faculty.id, hashTable->size);
    int originalIndex = index;
    
    cout << "Inserting Faculty ID " << faculty.id << " at hash index " << index << endl;
    
    if (hashTable->buckets[index] == nullptr) {
        HashNode* newNode = new HashNode;
        newNode->faculty = faculty;
        newNode->next = nullptr;
        hashTable->buckets[index] = newNode;
        cout << "Faculty inserted successfully at index " << index << endl;
    } else {
        cout << "Collision detected at index " << index << ". Using linear probing..." << endl;
        while (hashTable->buckets[index] != nullptr) {
            index = (index + 1) % hashTable->size;
            if (index == originalIndex) {
                cout << "Hash table is full. Cannot insert faculty." << endl;
                return;
            }
        }
        
        HashNode* newNode = new HashNode;
        newNode->faculty = faculty;
        newNode->next = nullptr;
        hashTable->buckets[index] = newNode;
        cout << "Faculty inserted at index " << index << " after probing" << endl;
    }
}

Faculty* searchFaculty(HashTable* hashTable, int id) {
    int index = hashDivision(id, hashTable->size);
    int originalIndex = index;
    
    cout << "Searching for Faculty ID " << id << " starting at index " << index << endl;
    
    while (hashTable->buckets[index] != nullptr) {
        if (hashTable->buckets[index]->faculty.id == id) {
            cout << "Faculty found at index " << index << endl;
            return &(hashTable->buckets[index]->faculty);
        }
        
        index = (index + 1) % hashTable->size;
        if (index == originalIndex) {
            break;
        }
    }
    
    cout << "Faculty with ID " << id << " not found" << endl;
    return nullptr;
}

void displayFaculty(Faculty faculty) {
    cout << "\n--- Faculty Details ---" << endl;
    cout << "ID: " << faculty.id << endl;
    cout << "Name: " << faculty.name << endl;
    cout << "Department: " << faculty.department << endl;
    cout << "Designation: " << faculty.designation << endl;
    cout << "Experience: " << faculty.experience << " years" << endl;
    cout << "Salary: " << faculty.salary << endl;
}

void displayAllFaculty(HashTable* hashTable) {
    cout << "\n=== Faculty Database ===" << endl;
    for (int i = 0; i < hashTable->size; i++) {
        if (hashTable->buckets[i] != nullptr) {
            cout << "\nIndex " << i << ":" << endl;
            displayFaculty(hashTable->buckets[i]->faculty);
        }
    }
}

void freeHashTable(HashTable* hashTable) {
    for (int i = 0; i < hashTable->size; i++) {
        if (hashTable->buckets[i] != nullptr) {
            delete hashTable->buckets[i];
        }
    }
    
    delete[] hashTable->buckets;
    delete hashTable;
}

int main() {
    HashTable* hashTable = createHashTable(TABLE_SIZE);
    
    Faculty faculty1 = {101, "Dr. Amit Sharma", "Computer Science", "Professor", 15, 85000.00};
    Faculty faculty2 = {205, "Dr. Priya Patel", "Electronics", "Associate Professor", 10, 70000.00};
    Faculty faculty3 = {312, "Dr. Rajesh Kumar", "Mechanical", "Assistant Professor", 5, 55000.00};
    Faculty faculty4 = {418, "Dr. Sneha Mehta", "Computer Science", "Professor", 12, 80000.00};
    Faculty faculty5 = {523, "Dr. Vikram Singh", "Civil", "Associate Professor", 8, 65000.00};
    
    cout << "=== Inserting Faculty Records ===\n" << endl;
    insertFaculty(hashTable, faculty1);
    insertFaculty(hashTable, faculty2);
    insertFaculty(hashTable, faculty3);
    insertFaculty(hashTable, faculty4);
    insertFaculty(hashTable, faculty5);
    
    displayAllFaculty(hashTable);
    
    cout << "\n\n=== Searching for Faculty ===\n" << endl;
    int searchId = 312;
    Faculty* found = searchFaculty(hashTable, searchId);
    if (found != nullptr) {
        displayFaculty(*found);
    }
    
    cout << endl;
    searchId = 999;
    found = searchFaculty(hashTable, searchId);
    
    freeHashTable(hashTable);
    return 0;
}
```

## Sample Output

```
=== Inserting Faculty Records ===

Inserting Faculty ID 101 at hash index 1
Faculty inserted successfully at index 1
Inserting Faculty ID 205 at hash index 5
Faculty inserted successfully at index 5
Inserting Faculty ID 312 at hash index 2
Faculty inserted successfully at index 2
Inserting Faculty ID 418 at hash index 8
Faculty inserted successfully at index 8
Inserting Faculty ID 523 at hash index 3
Faculty inserted successfully at index 3

=== Faculty Database ===

Index 1:
--- Faculty Details ---
ID: 101
Name: Dr. Amit Sharma
Department: Computer Science
Designation: Professor
Experience: 15 years
Salary: 85000

Index 2:
--- Faculty Details ---
ID: 312
Name: Dr. Rajesh Kumar
Department: Mechanical
Designation: Assistant Professor
Experience: 5 years
Salary: 55000

Index 3:
--- Faculty Details ---
ID: 523
Name: Dr. Vikram Singh
Department: Civil
Designation: Associate Professor
Experience: 8 years
Salary: 65000

Index 5:
--- Faculty Details ---
ID: 205
Name: Dr. Priya Patel
Department: Electronics
Designation: Associate Professor
Experience: 10 years
Salary: 70000

Index 8:
--- Faculty Details ---
ID: 418
Name: Dr. Sneha Mehta
Department: Computer Science
Designation: Professor
Experience: 12 years
Salary: 80000

=== Searching for Faculty ===

Searching for Faculty ID 312 starting at index 2
Faculty found at index 2

--- Faculty Details ---
ID: 312
Name: Dr. Rajesh Kumar
Department: Mechanical
Designation: Assistant Professor
Experience: 5 years
Salary: 55000

Searching for Faculty ID 999 starting at index 9
Faculty with ID 999 not found
```

## Dry Run

### Insertion Process:

1. **Insert Faculty ID 101:**
   - Hash index = 101 % 10 = 1
   - Bucket[1] is empty, insert directly
   
2. **Insert Faculty ID 205:**
   - Hash index = 205 % 10 = 5
   - Bucket[5] is empty, insert directly
   
3. **Insert Faculty ID 312:**
   - Hash index = 312 % 10 = 2
   - Bucket[2] is empty, insert directly

### Search Process:

1. **Search Faculty ID 312:**
   - Hash index = 312 % 10 = 2
   - Check index 2
   - Faculty found at index 2

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
