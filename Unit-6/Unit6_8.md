# Unit VI Assignment 8: Employee Database using Hash Table with Mid-Square Method and Linear Probing

Implementation to simulate an employee database as a hash table using mid-square method as hash function for linear probing collision handling technique.

## Problem Statement

WAP to simulate employee databases as a hash table. Search a particular employee by using Mid square method as a hash function for linear probing method of collision handling technique. Assume suitable data for employee record.

## Pseudo Code

### Employee Record Structure
```
Structure Employee:
    id: integer
    name: string
    department: string
    position: string
    salary: float
    joiningDate: string
```

### Hash Table Structure
```
Structure HashTable:
    size: integer
    employees: array of Employee
    occupied: array of booleans
```

### Hash Function (Mid-Square Method)
```
Algorithm HashMidSquare(id, tableSize):
    square = id * id
    numDigits = count digits in tableSize
    middleDigits = extract middle numDigits from square
    Return middleDigits MOD tableSize
```

### Insert Employee (Linear Probing)
```
Algorithm InsertEmployee(hashTable, employee):
    index = HashMidSquare(employee.id, hashTable.size)
    originalIndex = index
    While hashTable.occupied[index] is true:
        If hashTable.employees[index].id == employee.id:
            Print "Employee already exists"
            Return
        index = (index + 1) MOD hashTable.size
        If index == originalIndex:
            Print "Hash table is full"
            Return
    hashTable.employees[index] = employee
    hashTable.occupied[index] = true
```

### Search Employee
```
Algorithm SearchEmployee(hashTable, id):
    index = HashMidSquare(id, hashTable.size)
    originalIndex = index
    While hashTable.occupied[index] is true:
        If hashTable.employees[index].id == id:
            Return hashTable.employees[index]
        index = (index + 1) MOD hashTable.size
        If index == originalIndex:
            Break
    Return NULL
```

### Display All Employees
```
Algorithm DisplayAllEmployees(hashTable):
    For i = 0 to hashTable.size-1:
        If hashTable.occupied[i] is true:
            Print "Index", i, ":"
            Print hashTable.employees[i] details
```

## C++ Code Implementation

```cpp
#include <iostream>
#include <cstring>
#include <cmath>
using namespace std;

#define TABLE_SIZE 100

struct Employee {
    int id;
    char name[50];
    char department[50];
    char position[50];
    float salary;
    char joiningDate[15];
};

struct HashTable {
    int size;
    Employee* employees;
    bool* occupied;
};

HashTable* createHashTable(int size) {
    HashTable* hashTable = new HashTable;
    hashTable->size = size;
    hashTable->employees = new Employee[size];
    hashTable->occupied = new bool[size];
    
    for (int i = 0; i < size; i++) {
        hashTable->occupied[i] = false;
    }
    
    return hashTable;
}

int countDigits(int num) {
    if (num == 0) return 1;
    int count = 0;
    while (num > 0) {
        count++;
        num /= 10;
    }
    return count;
}

int extractMiddleDigits(long long square, int numDigits) {
    int totalDigits = countDigits(square);
    
    if (totalDigits <= numDigits) {
        return (int)square;
    }
    
    int startPos = (totalDigits - numDigits) / 2;
    for (int i = 0; i < startPos; i++) {
        square /= 10;
    }
    
    int divisor = 1;
    for (int i = 0; i < numDigits; i++) {
        divisor *= 10;
    }
    return (int)(square % divisor);
}

int hashMidSquare(int id, int tableSize) {
    long long square = (long long)id * id;
    int numDigits = countDigits(tableSize);
    int middleDigits = extractMiddleDigits(square, numDigits);
    int hashValue = middleDigits % tableSize;
    cout << "  ID: " << id << " -> Square: " << square << " -> Middle: " << middleDigits << " -> Hash: " << hashValue << endl;
    return hashValue;
}

void insertEmployee(HashTable* hashTable, Employee employee) {
    cout << "\nInserting Employee ID " << employee.id << " (" << employee.name << ")" << endl;
    int index = hashMidSquare(employee.id, hashTable->size);
    int originalIndex = index;
    int probeCount = 0;
    
    while (hashTable->occupied[index]) {
        if (hashTable->employees[index].id == employee.id) {
            cout << "Employee with ID " << employee.id << " already exists!" << endl;
            return;
        }
        
        probeCount++;
        index = (index + 1) % hashTable->size;
        if (index == originalIndex) {
            cout << "Hash table is full. Cannot insert employee." << endl;
            return;
        }
    }
    
    hashTable->employees[index] = employee;
    hashTable->occupied[index] = true;
    
    if (probeCount > 0) {
        cout << "Inserted at index " << index << " after " << probeCount << " probes" << endl;
    } else {
        cout << "Inserted successfully at index " << index << endl;
    }
}

Employee* searchEmployee(HashTable* hashTable, int id) {
    cout << "\nSearching for Employee ID " << id << endl;
    int index = hashMidSquare(id, hashTable->size);
    int originalIndex = index;
    int probeCount = 0;
    
    while (hashTable->occupied[index]) {
        if (hashTable->employees[index].id == id) {
            cout << "Employee found at index " << index << " after " << probeCount << " probes" << endl;
            return &hashTable->employees[index];
        }
        
        probeCount++;
        index = (index + 1) % hashTable->size;
        if (index == originalIndex) {
            break;
        }
    }
    
    cout << "Employee with ID " << id << " not found" << endl;
    return nullptr;
}

void displayEmployee(Employee employee) {
    cout << "\n--- Employee Details ---" << endl;
    cout << "ID: " << employee.id << endl;
    cout << "Name: " << employee.name << endl;
    cout << "Department: " << employee.department << endl;
    cout << "Position: " << employee.position << endl;
    cout << "Salary: " << employee.salary << endl;
    cout << "Joining Date: " << employee.joiningDate << endl;
}

void displayAllEmployees(HashTable* hashTable) {
    cout << "\n=== Employee Database ===" << endl;
    int count = 0;
    for (int i = 0; i < hashTable->size; i++) {
        if (hashTable->occupied[i]) {
            cout << "\nIndex " << i << ":" << endl;
            cout << "  ID: " << hashTable->employees[i].id 
                 << ", Name: " << hashTable->employees[i].name
                 << ", Dept: " << hashTable->employees[i].department
                 << ", Position: " << hashTable->employees[i].position
                 << ", Salary: " << hashTable->employees[i].salary
                 << ", Joining: " << hashTable->employees[i].joiningDate << endl;
            count++;
        }
    }
    
    cout << "\nTotal Employees: " << count << endl;
}

void deleteEmployee(HashTable* hashTable, int id) {
    cout << "\nDeleting Employee ID " << id << endl;
    int index = hashMidSquare(id, hashTable->size);
    int originalIndex = index;
    
    while (hashTable->occupied[index]) {
        if (hashTable->employees[index].id == id) {
            hashTable->occupied[index] = false;
            cout << "Employee deleted successfully from index " << index << endl;
            return;
        }
        
        index = (index + 1) % hashTable->size;
        if (index == originalIndex) {
            break;
        }
    }
    
    cout << "Employee with ID " << id << " not found" << endl;
}

void freeHashTable(HashTable* hashTable) {
    delete[] hashTable->employees;
    delete[] hashTable->occupied;
    delete hashTable;
}

int main() {
    HashTable* hashTable = createHashTable(TABLE_SIZE);
    
    Employee emp1 = {1234, "Rajesh Kumar", "IT", "Software Engineer", 75000.00, "2020-01-15"};
    Employee emp2 = {5678, "Priya Sharma", "HR", "Manager", 95000.00, "2019-03-20"};
    Employee emp3 = {9012, "Amit Patel", "Finance", "Analyst", 65000.00, "2021-06-10"};
    Employee emp4 = {3456, "Sneha Gupta", "IT", "Team Lead", 85000.00, "2018-11-05"};
    Employee emp5 = {7890, "Vikram Singh", "Marketing", "Executive", 55000.00, "2022-02-28"};
    
    cout << "=== Inserting Employee Records ===" << endl;
    insertEmployee(hashTable, emp1);
    insertEmployee(hashTable, emp2);
    insertEmployee(hashTable, emp3);
    insertEmployee(hashTable, emp4);
    insertEmployee(hashTable, emp5);
    
    displayAllEmployees(hashTable);
    
    cout << "\n\n=== Searching for Employees ===" << endl;
    int searchId = 3456;
    Employee* found = searchEmployee(hashTable, searchId);
    if (found != nullptr) {
        displayEmployee(*found);
    }
    
    searchId = 9999;
    searchEmployee(hashTable, searchId);
    
    cout << "\n\n=== Deleting Employee ===" << endl;
    deleteEmployee(hashTable, 5678);
    
    displayAllEmployees(hashTable);
    
    freeHashTable(hashTable);
    return 0;
}
```

## Sample Output

```
=== Inserting Employee Records ===
Inserting Employee ID 1234 (Rajesh Kumar)
  ID: 1234 -> Square: 1522756 -> Middle: 227 -> Hash: 27
Inserted successfully at index 27
Inserting Employee ID 5678 (Priya Sharma)
  ID: 5678 -> Square: 32239684 -> Middle: 396 -> Hash: 96
Inserted successfully at index 96
Inserting Employee ID 9012 (Amit Patel)
  ID: 9012 -> Square: 81216144 -> Middle: 161 -> Hash: 61
Inserted successfully at index 61
Inserting Employee ID 3456 (Sneha Gupta)
  ID: 3456 -> Square: 11943936 -> Middle: 439 -> Hash: 39
Inserted successfully at index 39
Inserting Employee ID 7890 (Vikram Singh)
  ID: 7890 -> Square: 62252100 -> Middle: 521 -> Hash: 21
Inserted successfully at index 21
=== Employee Database ===
Index 21:
  ID: 7890, Name: Vikram Singh, Dept: Marketing, Position: Executive, Salary: 55000.00, Joining: 2022-02-28
Index 27:
  ID: 1234, Name: Rajesh Kumar, Dept: IT, Position: Software Engineer, Salary: 75000.00, Joining: 2020-01-15
Index 39:
  ID: 3456, Name: Sneha Gupta, Dept: IT, Position: Team Lead, Salary: 85000.00, Joining: 2018-11-05
Index 61:
  ID: 9012, Name: Amit Patel, Dept: Finance, Position: Analyst, Salary: 65000.00, Joining: 2021-06-10
Index 96:
  ID: 5678, Name: Priya Sharma, Dept: HR, Position: Manager, Salary: 95000.00, Joining: 2019-03-20
Total Employees: 5
=== Searching for Employees ===
Searching for Employee ID 3456
  ID: 3456 -> Square: 11943936 -> Middle: 439 -> Hash: 39
Employee found at index 39 after 0 probes
--- Employee Details ---
ID: 3456
Name: Sneha Gupta
Department: IT
Position: Team Lead
Salary: 85000.00
Joining Date: 2018-11-05
Searching for Employee ID 9999
  ID: 9999 -> Square: 99980001 -> Middle: 800 -> Hash: 0
Employee with ID 9999 not found
=== Deleting Employee ===
Deleting Employee ID 5678
  ID: 5678 -> Square: 32239684 -> Middle: 396 -> Hash: 96
Employee deleted successfully from index 96
=== Employee Database ===
Index 21:
  ID: 7890, Name: Vikram Singh, Dept: Marketing, Position: Executive, Salary: 55000.00, Joining: 2022-02-28
Index 27:
  ID: 1234, Name: Rajesh Kumar, Dept: IT, Position: Software Engineer, Salary: 75000.00, Joining: 2020-01-15
Index 39:
  ID: 3456, Name: Sneha Gupta, Dept: IT, Position: Team Lead, Salary: 85000.00, Joining: 2018-11-05
Index 61:
  ID: 9012, Name: Amit Patel, Dept: Finance, Position: Analyst, Salary: 65000.00, Joining: 2021-06-10
Total Employees: 4
```

## Dry Run

### Mid-Square Hash Function Process:

1. **Employee ID 1234:**
   - Square: 1234² = 1,522,756
   - Extract middle 3 digits: 227
   - Hash: 227 % 100 = 27
   
2. **Employee ID 5678:**
   - Square: 5678² = 32,239,684
   - Extract middle 3 digits: 396
   - Hash: 396 % 100 = 96

3. **Employee ID 3456:**
   - Square: 3456² = 11,943,936
   - Extract middle 3 digits: 439
   - Hash: 439 % 100 = 39

### Search Process:

1. **Search Employee ID 3456:**
   - Calculate hash: 39
   - Check index 39
   - Employee found at index 39

## Performance Analysis

### Time Complexity:
- **Hash Function:** O(1)
- **Insert (Average):** O(1)
- **Insert (Worst):** O(n) - when many collisions occur
- **Search (Average):** O(1)
- **Search (Worst):** O(n) - when linear probing requires checking multiple slots
- **Delete (Average):** O(1)
- **Delete (Worst):** O(n)
- **Display All:** O(n)

### Space Complexity:
- O(n) where n is the table size

### Mid-Square Method Advantages:
- Better distribution than division or modulo methods
- Uses middle digits which tend to be more random
- Good for numeric keys with patterns
- Reduces clustering

## Conclusion

The mid-square method with linear probing provides:
- Improved hash distribution using middle digits of squared key
- Simple collision resolution with linear probing
- Good performance for employee databases with numeric IDs
- Better randomization than simple division methods
- Efficient for datasets with moderate load factors
- Suitable for employee management systems with unique employee IDs
- Trade-off between computation time and distribution quality
