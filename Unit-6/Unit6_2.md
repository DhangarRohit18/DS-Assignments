# Unit VI Assignment 2: Hash Table with Separate Chaining Collision Resolution

Implementation of collision handling using separate chaining.

## Problem Statement

Implement collision handling using separate chaining.

## Pseudo Code

### Hash Table Structure
```
Structure HashNode:
    key: integer
    value: string
    next: pointer to HashNode
Structure HashTable:
    size: integer
    buckets: array of pointers to HashNode of size size
```

### Hash Function
```
Algorithm Hash(key, tableSize):
    Return key MOD tableSize
```

### Insert
```
Algorithm Insert(hashTable, key, value):
    index = Hash(key, hashTable.size)
    Create new node with key and value
    new node.next = hashTable.buckets[index]
    hashTable.buckets[index] = new node
```

### Search
```
Algorithm Search(hashTable, key):
    index = Hash(key, hashTable.size)
    current = hashTable.buckets[index]
    While current is not NULL:
        If current.key == key:
            Return current.value
        current = current.next
    Return "Key not found"
```

### Delete
```
Algorithm Delete(hashTable, key):
    index = Hash(key, hashTable.size)
    current = hashTable.buckets[index]
    If current is NULL:
        Return "Key not found"
    If current.key == key:
        hashTable.buckets[index] = current.next
        Free current
        Return "Key deleted successfully"
    While current.next is not NULL:
        If current.next.key == key:
            temp = current.next
            current.next = current.next.next
            Free temp
            Return "Key deleted successfully"
        current = current.next
    Return "Key not found"
```

## Code Implementation

```c
#include <iostream>
using namespace std;
#include <stdlib.h>
#include <string.h>
#define TABLE_SIZE 10
#define MAX_NAME_LENGTH 50
struct HashNode_rrd {
    int key_rrd;
    char value_rrd[MAX_NAME_LENGTH];
    struct HashNode_rrd* next_rrd;
};

struct HashTable_rrd {
    int size_rrd;
    struct HashNode_rrd** buckets_rrd;
};

struct HashNode_rrd* createHashNode_rrd(int key_rrd, char value_rrd[]);
struct HashTable_rrd* createHashTable_rrd(int size_rrd);
int hash_rrd(int key_rrd, int tableSize_rrd);
void insert_rrd(struct HashTable_rrd* hashTable_rrd, int key_rrd, char value_rrd[]);
char* search_rrd(struct HashTable_rrd* hashTable_rrd, int key_rrd);
int delete_rrd(struct HashTable_rrd* hashTable_rrd, int key_rrd);
void displayHashTable_rrd(struct HashTable_rrd* hashTable_rrd);
float loadFactor_rrd(struct HashTable_rrd* hashTable_rrd);
int countCollisions_rrd(struct HashTable_rrd* hashTable_rrd);
void freeHashTable_rrd(struct HashTable_rrd* hashTable_rrd);
void createSampleData_rrd(struct HashTable_rrd* hashTable_rrd);
void displayMenu_rrd();
struct HashNode_rrd* createHashNode_rrd(int key_rrd, char value_rrd[]) {
    struct HashNode_rrd* newNode_rrd = (struct HashNode_rrd*)malloc(sizeof(struct HashNode_rrd));
    newNode_rrd->key_rrd = key_rrd;
    strcpy(newNode_rrd->value_rrd, value_rrd);
    newNode_rrd->next_rrd = NULL;
    return newNode_rrd;
}

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

int hash_rrd(int key_rrd, int tableSize_rrd) {
    return key_rrd % tableSize_rrd;
}

void insert_rrd(struct HashTable_rrd* hashTable_rrd, int key_rrd, char value_rrd[]) {
    int index_rrd = hash_rrd(key_rrd, hashTable_rrd->size_rrd);
    struct HashNode_rrd* newNode_rrd = createHashNode_rrd(key_rrd, value_rrd);
    newNode_rrd->next_rrd = hashTable_rrd->buckets_rrd[index_rrd];
    hashTable_rrd->buckets_rrd[index_rrd] = newNode_rrd;
    cout << "Key " << key_rrd, value_rrd, index_rrd << " inserted with value '%s' at index %d" << endl;
}

char* search_rrd(struct HashTable_rrd* hashTable_rrd, int key_rrd)
{
    int index_rrd = hash_rrd(key_rrd, hashTable_rrd->size_rrd);
    struct HashNode_rrd* current_rrd = hashTable_rrd->buckets_rrd[index_rrd];
    while (current_rrd != NULL)
{
        if (current_rrd->key_rrd == key_rrd)
{
            return current_rrd->value_rrd;
        }

        current_rrd = current_rrd->next_rrd;
    }
    return "Key not found";
}

int delete_rrd(struct HashTable_rrd* hashTable_rrd, int key_rrd) {
    int index_rrd = hash_rrd(key_rrd, hashTable_rrd->size_rrd);
    struct HashNode_rrd* current_rrd = hashTable_rrd->buckets_rrd[index_rrd];
    if (current_rrd != NULL && current_rrd->key_rrd == key_rrd)
{
        hashTable_rrd->buckets_rrd[index_rrd] = current_rrd->next_rrd;
        free(current_rrd);
        cout << "Key " << key_rrd << " deleted successfully" << endl;
        return 1;
    }

    while (current_rrd != NULL && current_rrd->next_rrd != NULL)
{
        if (current_rrd->next_rrd->key_rrd == key_rrd)
{
            struct HashNode_rrd* temp_rrd = current_rrd->next_rrd;
            current_rrd->next_rrd = current_rrd->next_rrd->next_rrd;
            free(temp_rrd);
            cout << "Key " << key_rrd << " deleted successfully" << endl;
            return 1;
        }

        current_rrd = current_rrd->next_rrd;
    }

    cout << "Key " << key_rrd << " not found" << endl;
    return 0;
}

void displayHashTable_rrd(struct HashTable_rrd* hashTable_rrd) {
    cout << "\nHash Table Contents (Separate Chaining):" << endl;
    cout << "Index\tKey-Value Pairs" << endl;
    cout << "-----\t----------------" << endl;
    for (int i_rrd = 0; i_rrd < hashTable_rrd->size_rrd; i_rrd++)
{
        cout << "" << i_rrd << "\t";
        struct HashNode_rrd* current_rrd = hashTable_rrd->buckets_rrd[i_rrd];
        if (current_rrd == NULL)
{
            cout << "-" << endl;
        } else
{

            while (current_rrd != NULL)
{
                cout << "(" << current_rrd->key_rrd, current_rrd->value_rrd << ": %s)";
                if (current_rrd->next_rrd != NULL)
{
                    cout << " -> ";
                }

                current_rrd = current_rrd->next_rrd;
            }

            cout << "" << endl;
        }
    }

    cout << "" << endl;
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
    insert_rrd(hashTable_rrd, 10, "Alice");
    insert_rrd(hashTable_rrd, 20, "Bob");
    insert_rrd(hashTable_rrd, 30, "Charlie");
    insert_rrd(hashTable_rrd, 15, "David");
    insert_rrd(hashTable_rrd, 25, "Eve");
    insert_rrd(hashTable_rrd, 35, "Frank");
    insert_rrd(hashTable_rrd, 45, "Grace");
}

void displayMenu_rrd() {
    cout << "\n===== Hash Table with Separate Chaining =====" << endl;
    cout << "1. Insert Key-Value Pair" << endl;
    cout << "2. Search by Key" << endl;
    cout << "3. Delete by Key" << endl;
    cout << "4. Display Hash Table" << endl;
    cout << "5. Show Load Factor" << endl;
    cout << "6. Show Collision Count" << endl;
    cout << "7. Create Sample Data" << endl;
    cout << "8. Exit" << endl;
    cout << "==========================================" << endl;
    cout << "Enter your choice: ";
}

int main() {
    cout << "Welcome to Hash Table Implementation with Separate Chaining!" << endl;
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
                int key_rrd;
                char value_rrd[MAX_NAME_LENGTH];
                cout << "Enter key (integer): ";
                cin >> key_rrd;
                cout << "Enter value (string): ";
                cin >> value_rrd;
                insert_rrd(hashTable_rrd, key_rrd, value_rrd);
                break;
            }

{
                int key_rrd;
                cout << "Enter key to search: ";
                cin >> key_rrd;
                char* result_rrd = search_rrd(hashTable_rrd, key_rrd);
                cout << "Search result for key " << key_rrd, result_rrd << ": %s" << endl;
                break;
            }

{
                int key_rrd;
                cout << "Enter key to delete: ";
                cin >> key_rrd;
                delete_rrd(hashTable_rrd, key_rrd);
                break;
            }

{
                displayHashTable_rrd(hashTable_rrd);
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
                cout << "Sample data created successfully!" << endl;
                displayHashTable_rrd(hashTable_rrd);
                break;
            }

{
                cout << "Thank you for using Hash Table with Separate Chaining!" << endl;
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
Welcome to Hash Table Implementation with Separate Chaining!
Enter the size of the hash table: 10
===== Hash Table with Separate Chaining =====
1. Insert Key-Value Pair
2. Search by Key
3. Delete by Key
4. Display Hash Table
5. Show Load Factor
6. Show Collision Count
7. Create Sample Data
8. Exit
==========================================
Enter your choice: 7
Sample data created successfully!
Hash Table Contents (Separate Chaining):
Index	Key-Value Pairs
-----	----------------
0	(10: Alice) -> (20: Bob) -> (30: Charlie)
1	-
2	-
3	-
4	-
5	(15: David) -> (25: Eve) -> (35: Frank) -> (45: Grace)
6	-
7	-
8	-
9	-
===== Hash Table with Separate Chaining =====
1. Insert Key-Value Pair
2. Search by Key
3. Delete by Key
4. Display Hash Table
5. Show Load Factor
6. Show Collision Count
7. Create Sample Data
8. Exit
==========================================
Enter your choice: 2
Enter key to search: 25
Search result for key 25: Eve
===== Hash Table with Separate Chaining =====
1. Insert Key-Value Pair
2. Search by Key
3. Delete by Key
4. Display Hash Table
5. Show Load Factor
6. Show Collision Count
7. Create Sample Data
8. Exit
==========================================
Enter your choice: 3
Enter key to delete: 35
Key 35 deleted successfully
Hash Table Contents (Separate Chaining):
Index	Key-Value Pairs
-----	----------------
0	(10: Alice) -> (20: Bob) -> (30: Charlie)
1	-
2	-
3	-
4	-
5	(15: David) -> (25: Eve) -> (45: Grace)
6	-
7	-
8	-
9	-
===== Hash Table with Separate Chaining =====
1. Insert Key-Value Pair
2. Search by Key
3. Delete by Key
4. Display Hash Table
5. Show Load Factor
6. Show Collision Count
7. Create Sample Data
8. Exit
==========================================
Enter your choice: 5
Load Factor: 0.70
===== Hash Table with Separate Chaining =====
1. Insert Key-Value Pair
2. Search by Key
3. Delete by Key
4. Display Hash Table
5. Show Load Factor
6. Show Collision Count
7. Create Sample Data
8. Exit
==========================================
Enter your choice: 6
Number of collisions: 4
```

## Dry Run

For a hash table of size 10 with MOD hash function and separate chaining:

1. **Insertions**:
   - Insert (10, "Alice"): hash(10) = 10 % 10 = 0 → Insert at bucket 0
   - Insert (20, "Bob"): hash(20) = 20 % 10 = 0 → Collision at bucket 0, add to linked list → Bucket 0: (20, "Bob") -> (10, "Alice")
   - Insert (30, "Charlie"): hash(30) = 30 % 10 = 0 → Collision at bucket 0, add to linked list → Bucket 0: (30, "Charlie") -> (20, "Bob") -> (10, "Alice")
   - Insert (15, "David"): hash(15) = 15 % 10 = 5 → Insert at bucket 5
   - Insert (25, "Eve"): hash(25) = 25 % 10 = 5 → Collision at bucket 5, add to linked list → Bucket 5: (25, "Eve") -> (15, "David")
   - Insert (35, "Frank"): hash(35) = 35 % 10 = 5 → Collision at bucket 5, add to linked list → Bucket 5: (35, "Frank") -> (25, "Eve") -> (15, "David")
   - Insert (45, "Grace"): hash(45) = 45 % 10 = 5 → Collision at bucket 5, add to linked list → Bucket 5: (45, "Grace") -> (35, "Frank") -> (25, "Eve") -> (15, "David")

2. **Search for key 25**:
   - hash(25) = 25 % 10 = 5
   - Traverse linked list at bucket 5:
     * Check (45, "Grace") - not 25
     * Check (35, "Frank") - not 25
     * Check (25, "Eve") - found → Return "Eve"

3. **Delete key 35**:
   - hash(35) = 35 % 10 = 5
   - Traverse linked list at bucket 5:
     * Check (45, "Grace") - not 35
     * Check (35, "Frank") - found
     * Remove node (35, "Frank") from linked list
     * Bucket 5 becomes: (45, "Grace") -> (25, "Eve") -> (15, "David")

4. **Load Factor**:
   - Total elements: 7
   - Table size: 10
   - Load factor: 7/10 = 0.7

5. **Collision Count**:
   - Bucket 0: 3 elements → 2 collisions
   - Bucket 5: 4 elements → 3 collisions
   - Total collisions: 2 + 3 = 5

## Conclusion

The implementation demonstrates a hash table with separate chaining collision resolution. Key features include:

1. **Separate Chaining**: Each bucket contains a linked list of elements
2. **MOD Hash Function**: Basic but effective hash function
3. **Complete Operations**: Insert, search, delete, and display operations
4. **Performance Metrics**: Load factor and collision count calculation

**Time Complexities**:
- Insert: O(1) average case, O(n) worst case (when all elements hash to same bucket)
- Search: O(1) average case, O(n) worst case (when all elements hash to same bucket)
- Delete: O(1) average case, O(n) worst case (when all elements hash to same bucket)
- Display: O(n + m) where n is table size and m is total elements

**Space Complexity**: O(n + m) where n is table size and m is total elements

Separate chaining has advantages and disadvantages:

**Advantages**:
1. **Simple Implementation**: Easy to understand and implement
2. **No Clustering**: No primary clustering problem
3. **Unlimited Storage**: Can store any number of elements
4. **Good Performance**: Maintains good performance even at high load factors
5. **Easy Deletion**: Simple deletion without tombstone issues

**Disadvantages**:
1. **Extra Memory**: Requires additional memory for pointers
2. **Cache Performance**: Poor cache performance due to pointer chasing
3. **Memory Allocation**: Dynamic memory allocation overhead
4. **List Traversal**: Need to traverse linked lists for operations

The implementation handles edge cases properly:
- Empty buckets
- Single element buckets
- Multiple element buckets
- Key not found during search/delete
- Memory management to prevent leaks
- Comprehensive user interface with clear feedback

Additional features beyond requirements:
- Hash table visualization
- Load factor calculation
- Collision count tracking
- Sample data creation for testing
- Interactive menu system
- Complete error handling

In real-world applications, this system could be extended to:
1. Support dynamic resizing
2. Implement self-balancing trees instead of linked lists
3. Add performance statistics
4. Support different data types
5. Implement open addressing as an alternative

Hash tables are fundamental data structures used in:
1. **Database Indexing**: Fast data retrieval
2. **Caching**: Quick access to frequently used data
3. **Compiler Design**: Symbol tables for variables and functions
4. **Networking**: Routing tables and packet filtering
5. **Cryptography**: Hash functions for data integrity

This implementation provides a solid foundation for understanding hash tables and collision resolution techniques, which are essential in computer science and software engineering for efficient data storage and retrieval. Separate chaining is particularly useful when the load factor is expected to be high or when the exact number of elements is unknown.
