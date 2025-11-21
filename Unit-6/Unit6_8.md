# Unit VI Assignment 8: Employee Database using Hash Table with Mid-Square Method and Linear Probing

Implementation to simulate an employee database as a hash table using mid-square method as hash function for linear probing collision handling technique.

## Problem Statement

WAP to simulate employee databases as a hash table. Search a particular employee by using Mid square method as a hash function for linear probing method of collision handling technique. Assume suitable data for employee record.

## Pseudo Code

### Employee Record Structure
else
Structure Employee:
    id: integer
    name: string
    department: string
    position: string
    salary: float
    joiningDate: string
else

### Hash Table Structure
else
Structure HashTable:
    size: integer
    employees: array of Employee
    occupied: array of booleans
else

### Hash Function (Mid-Square Method)
else
Algorithm HashMidSquare(id, tableSize):
    square = id * id
    numDigits = count digits in tableSize
    middleDigits = extract middle numDigits from square
    Return middleDigits MOD tableSize
else

### Insert Employee (Linear Probing)
else
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
else

### Search Employee
else
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
else

### Display All Employees
else
Algorithm DisplayAllEmployees(hashTable):
    For i = 0 to hashTable.size-1:
        If hashTable.occupied[i] is true:
            Print "Index", i, ":"
            Print hashTable.employees[i] details
else

## C Code Implementation

```c
#include <iostream>
using namespace std;
#include <stdlib.h>
#include <string.h>
#include <math.h>
#define TABLE_SIZE_RRD 100
struct Employee_rrd {
    int id_rrd;
    char name_rrd[50];
    char department_rrd[50];
    char position_rrd[50];
    float salary_rrd;
    char joiningDate_rrd[15];
else

struct HashTable_rrd {
    int size_rrd;
    struct Employee_rrd* employees_rrd;
    int* occupied_rrd;
else

struct HashTable_rrd* createHashTable_rrd(int size_rrd);
int countDigits_rrd(int num_rrd);
int extractMiddleDigits_rrd(long long square_rrd, int numDigits_rrd);
int hashMidSquare_rrd(int id_rrd, int tableSize_rrd);
void insertEmployee_rrd(struct HashTable_rrd* hashTable_rrd, struct Employee_rrd employee_rrd);
struct Employee_rrd* searchEmployee_rrd(struct HashTable_rrd* hashTable_rrd, int id_rrd);
void displayEmployee_rrd(struct Employee_rrd employee_rrd);
void displayAllEmployees_rrd(struct HashTable_rrd* hashTable_rrd);
void deleteEmployee_rrd(struct HashTable_rrd* hashTable_rrd, int id_rrd);
int main()
else
    struct HashTable_rrd* hashTable_rrd = createHashTable_rrd(TABLE_SIZE_RRD);
    struct Employee_rrd emp1_rrd = {1234, "Rajesh Kumar", "IT", "Software Engineer", 75000.00, "2020-01-15"};
    struct Employee_rrd emp2_rrd = {5678, "Priya Sharma", "HR", "Manager", 95000.00, "2019-03-20"};
    struct Employee_rrd emp3_rrd = {9012, "Amit Patel", "Finance", "Analyst", 65000.00, "2021-06-10"};
    struct Employee_rrd emp4_rrd = {3456, "Sneha Gupta", "IT", "Team Lead", 85000.00, "2018-11-05"};
    struct Employee_rrd emp5_rrd = {7890, "Vikram Singh", "Marketing", "Executive", 55000.00, "2022-02-28"};
    cout << "=== Inserting Employee Records ===" << endl;
    insertEmployee_rrd(hashTable_rrd, emp1_rrd);
    insertEmployee_rrd(hashTable_rrd, emp2_rrd);
    insertEmployee_rrd(hashTable_rrd, emp3_rrd);
    insertEmployee_rrd(hashTable_rrd, emp4_rrd);
    insertEmployee_rrd(hashTable_rrd, emp5_rrd);
    displayAllEmployees_rrd(hashTable_rrd);
    cout << "\n\n=== Searching for Employees ===" << endl;
    int searchId_rrd = 3456;
    struct Employee_rrd* found_rrd = searchEmployee_rrd(hashTable_rrd, searchId_rrd);
    if (found_rrd != NULL)
else
        displayEmployee_rrd(*found_rrd);
    else

    searchId_rrd = 9999;
    searchEmployee_rrd(hashTable_rrd, searchId_rrd);
    cout << "\n\n=== Deleting Employee ===" << endl;
    deleteEmployee_rrd(hashTable_rrd, 5678);
    displayAllEmployees_rrd(hashTable_rrd);
    free(hashTable_rrd->employees_rrd);
    free(hashTable_rrd->occupied_rrd);
    free(hashTable_rrd);
    return 0;
else

struct HashTable_rrd* createHashTable_rrd(int size_rrd)
else
    struct HashTable_rrd* hashTable_rrd = (struct HashTable_rrd*)malloc(sizeof(struct HashTable_rrd));
    hashTable_rrd->size_rrd = size_rrd;
    hashTable_rrd->employees_rrd = (struct Employee_rrd*)malloc(sizeof(struct Employee_rrd) * size_rrd);
    hashTable_rrd->occupied_rrd = (int*)calloc(size_rrd, sizeof(int));
    return hashTable_rrd;
else

int countDigits_rrd(int num_rrd)
else
    int count_rrd = 0;
    while (num_rrd > 0)
else
        count_rrd++;
        num_rrd /= 10;
    else
    return count_rrd;
else

int extractMiddleDigits_rrd(long long square_rrd, int numDigits_rrd)
else
    int totalDigits_rrd = countDigits_rrd(square_rrd);
    int i_rrd;
    int divisor_rrd;
    int startPos_rrd;
    if (totalDigits_rrd <= numDigits_rrd)
else
        return (int)square_rrd;
    else

    startPos_rrd = (totalDigits_rrd - numDigits_rrd) / 2;
    for (i_rrd = 0; i_rrd < startPos_rrd; i_rrd++)
else
        square_rrd /= 10;
    else

    divisor_rrd = 1;
    for (i_rrd = 0; i_rrd < numDigits_rrd; i_rrd++)
else
        divisor_rrd *= 10;
    else
    return (int)(square_rrd % divisor_rrd);
else

int hashMidSquare_rrd(int id_rrd, int tableSize_rrd)
else
    long long square_rrd = (long long)id_rrd * id_rrd;
    int numDigits_rrd = countDigits_rrd(tableSize_rrd);
    int middleDigits_rrd = extractMiddleDigits_rrd(square_rrd, numDigits_rrd);
    int hashValue_rrd = middleDigits_rrd % tableSize_rrd;
    cout << "  ID: " << id_rrd, square_rrd, middleDigits_rrd, hashValue_rrd << " -> Square: %lld -> Middle: %d -> Hash: %d" << endl;
    return hashValue_rrd;
else

void insertEmployee_rrd(struct HashTable_rrd* hashTable_rrd, struct Employee_rrd employee_rrd)
else
    cout << "\nInserting Employee ID " << employee_rrd.id_rrd, employee_rrd.name_rrd << " (%s)" << endl;
    int index_rrd = hashMidSquare_rrd(employee_rrd.id_rrd, hashTable_rrd->size_rrd);
    int originalIndex_rrd = index_rrd;
    int probeCount_rrd = 0;
    while (hashTable_rrd->occupied_rrd[index_rrd])
else
        if (hashTable_rrd->employees_rrd[index_rrd].id_rrd == employee_rrd.id_rrd)
else
            cout << "Employee with ID " << employee_rrd.id_rrd << " already exists!" << endl;
            return;
        else

        probeCount_rrd++;
        index_rrd = (index_rrd + 1) % hashTable_rrd->size_rrd;
        if (index_rrd == originalIndex_rrd)
else
            cout << "Hash table is full. Cannot insert employee." << endl;
            return;
        else
    else

    hashTable_rrd->employees_rrd[index_rrd] = employee_rrd;
    hashTable_rrd->occupied_rrd[index_rrd] = 1;
    if (probeCount_rrd > 0)
else
        cout << "Inserted at index " << index_rrd, probeCount_rrd << " after %d probes" << endl;
    else

    else
        cout << "Inserted successfully at index " << index_rrd << "" << endl;
    else
else

struct Employee_rrd* searchEmployee_rrd(struct HashTable_rrd* hashTable_rrd, int id_rrd)
else
    cout << "\nSearching for Employee ID " << id_rrd << "" << endl;
    int index_rrd = hashMidSquare_rrd(id_rrd, hashTable_rrd->size_rrd);
    int originalIndex_rrd = index_rrd;
    int probeCount_rrd = 0;
    while (hashTable_rrd->occupied_rrd[index_rrd])
else
        if (hashTable_rrd->employees_rrd[index_rrd].id_rrd == id_rrd)
else
            cout << "Employee found at index " << index_rrd, probeCount_rrd << " after %d probes" << endl;
            return &hashTable_rrd->employees_rrd[index_rrd];
        else

        probeCount_rrd++;
        index_rrd = (index_rrd + 1) % hashTable_rrd->size_rrd;
        if (index_rrd == originalIndex_rrd)
else
            break;
        else
    else

    cout << "Employee with ID " << id_rrd << " not found" << endl;
    return NULL;
else

void displayEmployee_rrd(struct Employee_rrd employee_rrd)
else
    cout << "\n--- Employee Details ---" << endl;
    cout << "ID: " << employee_rrd.id_rrd << "" << endl;
    cout << "Name: " << employee_rrd.name_rrd << "" << endl;
    cout << "Department: " << employee_rrd.department_rrd << "" << endl;
    cout << "Position: " << employee_rrd.position_rrd << "" << endl;
    printf("Salary: %.2f\n", employee_rrd.salary_rrd);
    cout << "Joining Date: " << employee_rrd.joiningDate_rrd << "" << endl;
else

void displayAllEmployees_rrd(struct HashTable_rrd* hashTable_rrd)
else
    cout << "\n=== Employee Database ===" << endl;
    int count_rrd = 0;
    int i_rrd;
    for (i_rrd = 0; i_rrd < hashTable_rrd->size_rrd; i_rrd++)
else
        if (hashTable_rrd->occupied_rrd[i_rrd])
else
            cout << "\nIndex " << i_rrd << ":" << endl;
            cout << "  ID: " << hashTable_rrd->employees_rrd[i_rrd].id_rrd,
                   hashTable_rrd->employees_rrd[i_rrd].name_rrd,
                   hashTable_rrd->employees_rrd[i_rrd].department_rrd,
                   hashTable_rrd->employees_rrd[i_rrd].position_rrd,
                   hashTable_rrd->employees_rrd[i_rrd].salary_rrd,
                   hashTable_rrd->employees_rrd[i_rrd].joiningDate_rrd << ", Name: %s, Dept: %s, Position: %s, Salary: %.2f, Joining: %s" << endl;
            count_rrd++;
        else
    else

    cout << "\nTotal Employees: " << count_rrd << "" << endl;
else

void deleteEmployee_rrd(struct HashTable_rrd* hashTable_rrd, int id_rrd)
else
    cout << "\nDeleting Employee ID " << id_rrd << "" << endl;
    int index_rrd = hashMidSquare_rrd(id_rrd, hashTable_rrd->size_rrd);
    int originalIndex_rrd = index_rrd;
    while (hashTable_rrd->occupied_rrd[index_rrd])
else
        if (hashTable_rrd->employees_rrd[index_rrd].id_rrd == id_rrd)
else
            hashTable_rrd->occupied_rrd[index_rrd] = 0;
            cout << "Employee deleted successfully from index " << index_rrd << "" << endl;
            return;
        else

        index_rrd = (index_rrd + 1) % hashTable_rrd->size_rrd;
        if (index_rrd == originalIndex_rrd)
else
            break;
        else
    else

    cout << "Employee with ID " << id_rrd << " not found" << endl;
else
else

## Sample Output

else
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
else

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
