# Unit VI Assignment 7: Faculty Database using Hash Table with MOD Hash Function and Linear Probing with Chaining With Replacement

Implementation to simulate a faculty database as a hash table using MOD hash function for linear probing with chaining with replacement method of collision handling technique.

## Problem Statement

WAP to simulate a faculty database as a hash table. Search a particular faculty by using MOD as a hash function for linear probing with chaining with replacement method of collision handling technique. Assume suitable data for faculty record.

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

### Hash Node Structure
```
Structure HashNode:
    faculty: Faculty
    next: pointer to HashNode
```

### Hash Table Structure
```
Structure HashTable:
    size: integer
    buckets: array of pointers to HashNode of size size
```

### Hash Function (MOD Method)
```
Algorithm HashMod(id, tableSize):
    Return id MOD tableSize
```

### Insert Faculty (Linear Probing with Chaining With Replacement)
```
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
```

### Search Faculty
```
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
```

### Display All Faculty
```
Algorithm DisplayAllFaculty(hashTable):
    For i = 0 to hashTable.size-1:
        If hashTable.buckets[i] is not NULL:
            Print "Index", i, ":"
            current = hashTable.buckets[i]
            While current is not NULL:
                Print current.faculty details
                current = current.next
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

int hashMod(int id, int tableSize) {
    return id % tableSize;
}

HashNode* createNode(Faculty faculty) {
    HashNode* newNode = new HashNode;
    newNode->faculty = faculty;
    newNode->next = nullptr;
    return newNode;
}

void insertFaculty(HashTable* hashTable, Faculty faculty) {
    int index = hashMod(faculty.id, hashTable->size);
    int homeIndex = index;
    
    cout << "Inserting Faculty ID " << faculty.id << " at hash index " << index << endl;
    
    HashNode* newNode = createNode(faculty);
    
    if (hashTable->buckets[index] == nullptr) {
        hashTable->buckets[index] = newNode;
        cout << "Faculty inserted successfully at index " << index << endl;
    } else {
        cout << "Collision detected at index " << index << ". Using chaining with replacement..." << endl;
        HashNode* existingNode = hashTable->buckets[index];
        int existingHomeIndex = hashMod(existingNode->faculty.id, hashTable->size);
        
        if (existingHomeIndex != index) {
            cout << "Existing node at index " << index << " is displaced (home: " << existingHomeIndex << "). Replacing..." << endl;
            hashTable->buckets[index] = newNode;
            
            int newIndex = (index + 1) % hashTable->size;
            while (hashTable->buckets[newIndex] != nullptr && newIndex != index) {
                newIndex = (newIndex + 1) % hashTable->size;
            }
            
            if (newIndex == index) {
                cout << "Hash table is full!" << endl;
                delete existingNode;
                return;
            }
            
            hashTable->buckets[newIndex] = existingNode;
            cout << "Displaced node moved to index " << newIndex << endl;
        } else {
            cout << "Chaining at home address " << index << endl;
            newNode->next = existingNode;
            hashTable->buckets[index] = newNode;
        }
    }
}

Faculty* searchFaculty(HashTable* hashTable, int id) {
    int index = hashMod(id, hashTable->size);
    int originalIndex = index;
    
    cout << "Searching for Faculty ID " << id << " starting at index " << index << endl;
    
    do {
        HashNode* current = hashTable->buckets[index];
        while (current != nullptr) {
            if (current->faculty.id == id) {
                cout << "Faculty found at index " << index << endl;
                return &(current->faculty);
            }
            current = current->next;
        }
        
        index = (index + 1) % hashTable->size;
    } while (index != originalIndex && hashTable->buckets[index] != nullptr);
    
    cout << "Faculty with ID " << id << " not found" << endl;
    return nullptr;
}

void displayFaculty(Faculty faculty) {
    cout << "  ID: " << faculty.id << ", Name: " << faculty.name << ", Dept: " << faculty.department 
         << ", Designation: " << faculty.designation << ", Exp: " << faculty.experience 
         << " years, Salary: " << faculty.salary << endl;
}

void displayAllFaculty(HashTable* hashTable) {
    cout << "\n=== Faculty Database ===" << endl;
    for (int i = 0; i < hashTable->size; i++) {
        if (hashTable->buckets[i] != nullptr) {
            cout << "\nIndex " << i << ":" << endl;
            HashNode* current = hashTable->buckets[i];
            while (current != nullptr) {
                displayFaculty(current->faculty);
                current = current->next;
            }
        }
    }
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
    
    Faculty faculty1 = {101, "Dr. Amit Sharma", "Computer Science", "Professor", 15, 85000.00};
    Faculty faculty2 = {102, "Dr. Priya Patel", "Electronics", "Associate Professor", 10, 70000.00};
    Faculty faculty3 = {111, "Dr. Rajesh Kumar", "Mechanical", "Assistant Professor", 5, 55000.00};
    Faculty faculty4 = {121, "Dr. Sneha Mehta", "Computer Science", "Professor", 12, 80000.00};
    Faculty faculty5 = {131, "Dr. Vikram Singh", "Civil", "Associate Professor", 8, 65000.00};
    
    cout << "=== Inserting Faculty Records ===\n" << endl;
    insertFaculty(hashTable, faculty1);
    insertFaculty(hashTable, faculty2);
    insertFaculty(hashTable, faculty3);
    insertFaculty(hashTable, faculty4);
    insertFaculty(hashTable, faculty5);
    
    displayAllFaculty(hashTable);
    
    cout << "\n\n=== Searching for Faculty ===\n" << endl;
    int searchId = 111;
    Faculty* found = searchFaculty(hashTable, searchId);
    if (found != nullptr) {
        cout << "\nFound Faculty:" << endl;
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
```


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

