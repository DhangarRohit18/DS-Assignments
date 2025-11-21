# Unit IV Assignment 8: Employee Record Search using Tree Data Structure

Implementation of a program to efficiently search employee records using Tree data structure and sort data by employee ID.

## Problem Statement

Write a program to efficiently search a particular employee record by using Tree data structure. Also sort the data on emp­id in ascending order.

## Pseudo Code

### Employee Node Structure
```
Structure EmployeeNode:
    empId: integer
    name: string
    department: string
    salary: float
    left: pointer to EmployeeNode
    right: pointer to EmployeeNode
```

### Insert Employee (based on empId)
```
Algorithm InsertEmployee(root, empId, name, department, salary):
    If root is NULL:
        Create new employee node
        Return new node
    If empId < root.empId:
        root.left = InsertEmployee(root.left, empId, name, department, salary)
    Else If empId > root.empId:
        root.right = InsertEmployee(root.right, empId, name, department, salary)
    Return root
```

### Search Employee
```
Algorithm SearchEmployee(root, empId):
    If root is NULL OR root.empId equals empId:
        Return root
    If empId < root.empId:
        Return SearchEmployee(root.left, empId)
    Else:
        Return SearchEmployee(root.right, empId)
```

### Display Employees (Inorder - sorted by empId)
```
Algorithm DisplayEmployees(root):
    If root is not NULL:
        DisplayEmployees(root.left)
        Print root.empId, root.name, root.department, root.salary
        DisplayEmployees(root.right)
```

## Code Implementation

```cpp
#include <iostream>
using namespace std;
#define MAX_NAME_LENGTH 50
#define MAX_DEPT_LENGTH 30
struct EmployeeNode_rrd {
    int empId_rrd;
    char name_rrd[MAX_NAME_LENGTH];
    char department_rrd[MAX_DEPT_LENGTH];
    float salary_rrd;
    struct EmployeeNode_rrd* left_rrd;
    struct EmployeeNode_rrd* right_rrd;
};

struct EmployeeNode_rrd* createEmployeeNode_rrd(int empId_rrd, char name_rrd[], char department_rrd[], float salary_rrd);
struct EmployeeNode_rrd* insertEmployee_rrd(struct EmployeeNode_rrd* root_rrd, int empId_rrd, char name_rrd[], char department_rrd[], float salary_rrd);
struct EmployeeNode_rrd* searchEmployee_rrd(struct EmployeeNode_rrd* root_rrd, int empId_rrd);
void displayEmployees_rrd(struct EmployeeNode_rrd* root_rrd);
void displayEmployeesPreorder_rrd(struct EmployeeNode_rrd* root_rrd);
void displayEmployeesPostorder_rrd(struct EmployeeNode_rrd* root_rrd);
void displayStructure_rrd(struct EmployeeNode_rrd* root_rrd, int space_rrd);
void printTreeStructure_rrd(struct EmployeeNode_rrd* root_rrd);
int countEmployees_rrd(struct EmployeeNode_rrd* root_rrd);
int findHeight_rrd(struct EmployeeNode_rrd* root_rrd);
struct EmployeeNode_rrd* findMinEmpId_rrd(struct EmployeeNode_rrd* root_rrd);
struct EmployeeNode_rrd* findMaxEmpId_rrd(struct EmployeeNode_rrd* root_rrd);
double calculateAverageSalary_rrd(struct EmployeeNode_rrd* root_rrd, int* totalCount_rrd);
void findEmployeesBySalaryRange_rrd(struct EmployeeNode_rrd* root_rrd, float minSalary_rrd, float maxSalary_rrd);
void freeTree_rrd(struct EmployeeNode_rrd* root_rrd);
struct EmployeeNode_rrd* createSampleEmployees_rrd();
void displayMenu_rrd();
struct EmployeeNode_rrd* createEmployeeNode_rrd(int empId_rrd, char name_rrd[], char department_rrd[], float salary_rrd) {
    struct EmployeeNode_rrd* newNode_rrd = (struct EmployeeNode_rrd*)malloc(sizeof(struct EmployeeNode_rrd));
    newNode_rrd->empId_rrd = empId_rrd;
    strcpy(newNode_rrd->name_rrd, name_rrd);
    strcpy(newNode_rrd->department_rrd, department_rrd);
    newNode_rrd->salary_rrd = salary_rrd;
    newNode_rrd->left_rrd = NULL;
    newNode_rrd->right_rrd = NULL;
    return newNode_rrd;
}

struct EmployeeNode_rrd* insertEmployee_rrd(struct EmployeeNode_rrd* root_rrd, int empId_rrd, char name_rrd[], char department_rrd[], float salary_rrd) {
    if (root_rrd == NULL)
{
        cout << "Added employee ID " << empId_rrd, name_rrd << ": %s" << endl;
        return createEmployeeNode_rrd(empId_rrd, name_rrd, department_rrd, salary_rrd);
    }

    if (empId_rrd < root_rrd->empId_rrd)
{
        root_rrd->left_rrd = insertEmployee_rrd(root_rrd->left_rrd, empId_rrd, name_rrd, department_rrd, salary_rrd);
    } else if (empId_rrd > root_rrd->empId_rrd)

{
        root_rrd->right_rrd = insertEmployee_rrd(root_rrd->right_rrd, empId_rrd, name_rrd, department_rrd, salary_rrd);
    } else
{

        cout << "Employee with ID " << empId_rrd << " already exists!" << endl;
    }
    return root_rrd;
}

struct EmployeeNode_rrd* searchEmployee_rrd(struct EmployeeNode_rrd* root_rrd, int empId_rrd) {
    if (root_rrd == NULL || root_rrd->empId_rrd == empId_rrd)
{
        return root_rrd;
    }

    if (root_rrd->empId_rrd < empId_rrd)
{
        return searchEmployee_rrd(root_rrd->right_rrd, empId_rrd);
    }
    return searchEmployee_rrd(root_rrd->left_rrd, empId_rrd);
}

void displayEmployees_rrd(struct EmployeeNode_rrd* root_rrd) {
    if (root_rrd != NULL)
{
        displayEmployees_rrd(root_rrd->left_rrd);
        cout << "ID: " << root_rrd->empId_rrd, root_rrd->name_rrd, root_rrd->department_rrd, root_rrd->salary_rrd << "\tName: %-15s\tDept: %-10s\tSalary: %.2f" << endl;
        displayEmployees_rrd(root_rrd->right_rrd);
    }
}

void displayEmployeesPreorder_rrd(struct EmployeeNode_rrd* root_rrd) {
    if (root_rrd != NULL)
{
        cout << "ID: " << root_rrd->empId_rrd, root_rrd->name_rrd, root_rrd->department_rrd, root_rrd->salary_rrd << "\tName: %-15s\tDept: %-10s\tSalary: %.2f" << endl;
        displayEmployeesPreorder_rrd(root_rrd->left_rrd);
        displayEmployeesPreorder_rrd(root_rrd->right_rrd);
    }
}

void displayEmployeesPostorder_rrd(struct EmployeeNode_rrd* root_rrd) {
    if (root_rrd != NULL)
{
        displayEmployeesPostorder_rrd(root_rrd->left_rrd);
        displayEmployeesPostorder_rrd(root_rrd->right_rrd);
        cout << "ID: " << root_rrd->empId_rrd, root_rrd->name_rrd, root_rrd->department_rrd, root_rrd->salary_rrd << "\tName: %-15s\tDept: %-10s\tSalary: %.2f" << endl;
    }
}

void displayStructure_rrd(struct EmployeeNode_rrd* root_rrd, int space_rrd) {
    const int COUNT_rrd = 15;
    if (root_rrd == NULL)
{
        return;
    }

    space_rrd += COUNT_rrd;
    displayStructure_rrd(root_rrd->right_rrd, space_rrd);
    cout << "" << endl;
    for (int i_rrd = COUNT_rrd; i_rrd < space_rrd; i_rrd++)
{
        cout << " ";
    }

    cout << "" << root_rrd->empId_rrd, root_rrd->name_rrd << "(%s)" << endl;
    displayStructure_rrd(root_rrd->left_rrd, space_rrd);
}

void printTreeStructure_rrd(struct EmployeeNode_rrd* root_rrd) {
    cout << "\nEmployee Tree Structure (ID(Name)):" << endl;
    displayStructure_rrd(root_rrd, 0);
    cout << "" << endl;
}

int countEmployees_rrd(struct EmployeeNode_rrd* root_rrd) {
    if (root_rrd == NULL)
{
        return 0;
    }
    return 1 + countEmployees_rrd(root_rrd->left_rrd) + countEmployees_rrd(root_rrd->right_rrd);
}

int findHeight_rrd(struct EmployeeNode_rrd* root_rrd) {
    if (root_rrd == NULL)
{
        return -1;
    }

    int leftHeight_rrd = findHeight_rrd(root_rrd->left_rrd);
    int rightHeight_rrd = findHeight_rrd(root_rrd->right_rrd);
    return 1 + (leftHeight_rrd > rightHeight_rrd ? leftHeight_rrd : rightHeight_rrd);
}

struct EmployeeNode_rrd* findMinEmpId_rrd(struct EmployeeNode_rrd* root_rrd) {
    if (root_rrd == NULL)
{
        return NULL;
    }

    while (root_rrd->left_rrd != NULL)
{
        root_rrd = root_rrd->left_rrd;
    }
    return root_rrd;
}

struct EmployeeNode_rrd* findMaxEmpId_rrd(struct EmployeeNode_rrd* root_rrd) {
    if (root_rrd == NULL)
{
        return NULL;
    }

    while (root_rrd->right_rrd != NULL)
{
        root_rrd = root_rrd->right_rrd;
    }
    return root_rrd;
}

double calculateAverageSalary_rrd(struct EmployeeNode_rrd* root_rrd, int* totalCount_rrd)
{
    if (root_rrd == NULL)
{
        return 0.0;
    }

    (*totalCount_rrd)++;
    return root_rrd->salary_rrd + calculateAverageSalary_rrd(root_rrd->left_rrd, totalCount_rrd) + 
           calculateAverageSalary_rrd(root_rrd->right_rrd, totalCount_rrd);
}

void findEmployeesBySalaryRange_rrd(struct EmployeeNode_rrd* root_rrd, float minSalary_rrd, float maxSalary_rrd) {
    if (root_rrd != NULL)
{
        findEmployeesBySalaryRange_rrd(root_rrd->left_rrd, minSalary_rrd, maxSalary_rrd);
        if (root_rrd->salary_rrd >= minSalary_rrd && root_rrd->salary_rrd <= maxSalary_rrd)
{
            cout << "ID: " << root_rrd->empId_rrd, root_rrd->name_rrd, root_rrd->department_rrd, root_rrd->salary_rrd << "\tName: %-15s\tDept: %-10s\tSalary: %.2f" << endl;
        }

        findEmployeesBySalaryRange_rrd(root_rrd->right_rrd, minSalary_rrd, maxSalary_rrd);
    }
}

void findEmployeesByDepartment_rrd(struct EmployeeNode_rrd* root_rrd, char department_rrd[]) {
    if (root_rrd != NULL)
{
        findEmployeesByDepartment_rrd(root_rrd->left_rrd, department_rrd);
        if (strcmp(root_rrd->department_rrd, department_rrd) == 0)
{
            cout << "ID: " << root_rrd->empId_rrd, root_rrd->name_rrd, root_rrd->department_rrd, root_rrd->salary_rrd << "\tName: %-15s\tDept: %-10s\tSalary: %.2f" << endl;
        }

        findEmployeesByDepartment_rrd(root_rrd->right_rrd, department_rrd);
    }
}

int updateEmployeeSalary_rrd(struct EmployeeNode_rrd* root_rrd, int empId_rrd, float newSalary_rrd) {
    struct EmployeeNode_rrd* employee_rrd = searchEmployee_rrd(root_rrd, empId_rrd);
    if (employee_rrd != NULL)
{
        cout << "Updating salary for employee " << empId_rrd, employee_rrd->name_rrd, employee_rrd->salary_rrd, newSalary_rrd << " (%s): %.2f -> %.2f" << endl;
        employee_rrd->salary_rrd = newSalary_rrd;
        return 1;
    }
    return 0;
}

int deleteEmployee_rrd(struct EmployeeNode_rrd* root_rrd, int empId_rrd) {
    struct EmployeeNode_rrd* employee_rrd = searchEmployee_rrd(root_rrd, empId_rrd);
    if (employee_rrd != NULL)
{
        cout << "Employee ID " << empId_rrd, employee_rrd->name_rrd << " (%s) marked for deletion" << endl;
        return 1;
    }
    return 0;
}

void freeEmployeeTree_rrd(struct EmployeeNode_rrd* root_rrd) {
    if (root_rrd != NULL)
{
        freeEmployeeTree_rrd(root_rrd->left_rrd);
        freeEmployeeTree_rrd(root_rrd->right_rrd);
        free(root_rrd);
    }
}

struct EmployeeNode_rrd* createSampleEmployees_rrd() {
    struct EmployeeNode_rrd* root_rrd = NULL;
    root_rrd = insertEmployee_rrd(root_rrd, 1001, "Alice Johnson", "IT", 75000.0);
    root_rrd = insertEmployee_rrd(root_rrd, 1005, "Bob Smith", "HR", 65000.0);
    root_rrd = insertEmployee_rrd(root_rrd, 1003, "Charlie Brown", "Finance", 70000.0);
    root_rrd = insertEmployee_rrd(root_rrd, 1008, "Diana Wilson", "IT", 80000.0);
    root_rrd = insertEmployee_rrd(root_rrd, 1002, "Edward Davis", "Marketing", 60000.0);
    root_rrd = insertEmployee_rrd(root_rrd, 1007, "Fiona Miller", "Finance", 72000.0);
    root_rrd = insertEmployee_rrd(root_rrd, 1004, "George Taylor", "HR", 62000.0);
    root_rrd = insertEmployee_rrd(root_rrd, 1009, "Helen Anderson", "IT", 85000.0);
    root_rrd = insertEmployee_rrd(root_rrd, 1006, "Ian Thomas", "Marketing", 63000.0);
    return root_rrd;
}

struct EmployeeNode_rrd* addEmployeeInteractive_rrd(struct EmployeeNode_rrd* root_rrd) {
    int empId_rrd;
    char name_rrd[MAX_NAME_LENGTH];
    char department_rrd[MAX_DEPT_LENGTH];
    float salary_rrd;
    cout << "Enter employee ID: ";
    cin >> empId_rrd;
    cout << "Enter employee name: ";
    scanf(" %[^\n]s", name_rrd);
    cout << "Enter department: ";
    scanf(" %[^\n]s", department_rrd);
    cout << "Enter salary: ";
    scanf("%f", &salary_rrd);
    if (salary_rrd < 0)
{
        cout << "Invalid salary! Salary cannot be negative." << endl;
        return root_rrd;
    }

    root_rrd = insertEmployee_rrd(root_rrd, empId_rrd, name_rrd, department_rrd, salary_rrd);
    return root_rrd;
}

void displayMenu_rrd() {
    cout << "\n===== Employee Record Management System =====" << endl;
    cout << "1. Create Sample Employee Data" << endl;
    cout << "2. Add Employee" << endl;
    cout << "3. Search Employee by ID" << endl;
    cout << "4. Display All Employees (Sorted by ID)" << endl;
    cout << "5. Display Tree Structure" << endl;
    cout << "6. Count Employees" << endl;
    cout << "7. Find Employee with Min/Max ID" << endl;
    cout << "8. Calculate Average Salary" << endl;
    cout << "9. Find Employees by Salary Range" << endl;
    cout << "10. Find Employees by Department" << endl;
    cout << "11. Update Employee Salary" << endl;
    cout << "12. Exit" << endl;
    cout << "==========================================" << endl;
    cout << "Enter your choice: ";
}

int main() {
    cout << "Welcome to Employee Record Management System!" << endl;
    cout << "Employees are stored in a BST sorted by Employee ID for efficient search." << endl;
    struct EmployeeNode_rrd* root_rrd = NULL;
    int choice_rrd;
    while (1)
{
        displayMenu_rrd();
        cin >> choice_rrd;
        switch (choice_rrd)
{
{
                freeEmployeeTree_rrd(root_rrd);
                root_rrd = createSampleEmployees_rrd();
                cout << "Sample employee data created successfully!" << endl;
                break;
            }

{
                root_rrd = addEmployeeInteractive_rrd(root_rrd);
                break;
            }

{
                if (root_rrd == NULL)
{
                    cout << "No employees in the system!" << endl;
                    break;
                }

                int empId_rrd;
                cout << "Enter employee ID to search: ";
                cin >> empId_rrd;
                struct EmployeeNode_rrd* employee_rrd = searchEmployee_rrd(root_rrd, empId_rrd);
                if (employee_rrd != NULL)
{
                    cout << "\nEmployee Found:" << endl;
                    cout << "ID: " << employee_rrd->empId_rrd << "" << endl;
                    cout << "Name: " << employee_rrd->name_rrd << "" << endl;
                    cout << "Department: " << employee_rrd->department_rrd << "" << endl;
                    printf("Salary: %.2f\n", employee_rrd->salary_rrd);
                } else
{

                    cout << "Employee with ID " << empId_rrd << " not found!" << endl;
                }
                break;
            }

{
                if (root_rrd == NULL)
{
                    cout << "No employees in the system!" << endl;
                    break;
                }

                cout << "\nAll Employees (Sorted by Employee ID):" << endl;
                cout << "ID\tName\t\t\tDept\t\tSalary" << endl;
                cout << "--\t----\t\t\t----\t\t------" << endl;
                displayEmployees_rrd(root_rrd);
                break;
            }

            {
                if (root_rrd == NULL)
                {
                    cout << "No employees in the system!" << endl;
                    break;
                }

                printTreeStructure_rrd(root_rrd);
                break;
            }

{
                int count_rrd = countEmployees_rrd(root_rrd);
                cout << "Total number of employees: " << count_rrd << "" << endl;
                break;
            }

{
                if (root_rrd == NULL)
{
                    cout << "No employees in the system!" << endl;
                    break;
                }

                struct EmployeeNode_rrd* minEmp_rrd = findMinEmpId_rrd(root_rrd);
                struct EmployeeNode_rrd* maxEmp_rrd = findMaxEmpId_rrd(root_rrd);
                if (minEmp_rrd != NULL)
{
                    cout << "Employee with minimum ID: " << minEmp_rrd->empId_rrd, minEmp_rrd->name_rrd << " (%s)" << endl;
                }

                if (maxEmp_rrd != NULL)
{
                    cout << "Employee with maximum ID: " << maxEmp_rrd->empId_rrd, maxEmp_rrd->name_rrd << " (%s)" << endl;
                }
                break;
            }

{
                if (root_rrd == NULL)
{
                    cout << "No employees in the system!" << endl;
                    break;
                }

                int totalCount_rrd = 0;
                double totalSalary_rrd = calculateAverageSalary_rrd(root_rrd, &totalCount_rrd);
                if (totalCount_rrd > 0)
{
                    double average_rrd = totalSalary_rrd / totalCount_rrd;
                    printf("Average salary of all employees: %.2f\n", average_rrd);
                }
                break;
            }

{
                if (root_rrd == NULL)
{
                    cout << "No employees in the system!" << endl;
                    break;
                }

                float minSalary_rrd, maxSalary_rrd;
                cout << "Enter minimum salary: ";
                scanf("%f", &minSalary_rrd);
                cout << "Enter maximum salary: ";
                scanf("%f", &maxSalary_rrd);
                if (minSalary_rrd > maxSalary_rrd)
{
                    cout << "Invalid range! Minimum salary cannot be greater than maximum salary." << endl;
                    break;
                }

                printf("\nEmployees with salary between %.2f and %.2f:\n", minSalary_rrd, maxSalary_rrd);
                cout << "ID\tName\t\t\tDept\t\tSalary" << endl;
                cout << "--\t----\t\t\t----\t\t------" << endl;
                findEmployeesBySalaryRange_rrd(root_rrd, minSalary_rrd, maxSalary_rrd);
                break;
            }

{
                if (root_rrd == NULL)
{
                    cout << "No employees in the system!" << endl;
                    break;
                }

                char department_rrd[MAX_DEPT_LENGTH];
                cout << "Enter department name: ";
                scanf(" %[^\n]s", department_rrd);
                cout << "\nEmployees in " << department_rrd << " department:" << endl;
                cout << "ID\tName\t\t\tDept\t\tSalary" << endl;
                cout << "--\t----\t\t\t----\t\t------" << endl;
                findEmployeesByDepartment_rrd(root_rrd, department_rrd);
                break;
            }

{
                if (root_rrd == NULL)
{
                    cout << "No employees in the system!" << endl;
                    break;
                }

                int empId_rrd;
                float newSalary_rrd;
                cout << "Enter employee ID: ";
                cin >> empId_rrd;
                cout << "Enter new salary: ";
                scanf("%f", &newSalary_rrd);
                if (newSalary_rrd < 0)
{
                    cout << "Invalid salary! Salary cannot be negative." << endl;
                    break;
                }

                if (updateEmployeeSalary_rrd(root_rrd, empId_rrd, newSalary_rrd))
{
                    cout << "Salary updated successfully!" << endl;
                } else
{

                    cout << "Employee with ID " << empId_rrd << " not found!" << endl;
                }
                break;
            }

{
                cout << "Thank you for using Employee Record Management System!" << endl;
                freeEmployeeTree_rrd(root_rrd);
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
Welcome to Employee Record Management System!
Employees are stored in a BST sorted by Employee ID for efficient search.
===== Employee Record Management System =====
1. Create Sample Employee Data
2. Add Employee
3. Search Employee by ID
4. Display All Employees (Sorted by ID)
5. Display Tree Structure
6. Count Employees
7. Find Employee with Min/Max ID
8. Calculate Average Salary
9. Find Employees by Salary Range
10. Find Employees by Department
11. Update Employee Salary
12. Exit
==========================================
Enter your choice: 1
Added employee ID 1001: Alice Johnson
Added employee ID 1005: Bob Smith
Added employee ID 1003: Charlie Brown
Added employee ID 1008: Diana Wilson
Added employee ID 1002: Edward Davis
Added employee ID 1007: Fiona Miller
Added employee ID 1004: George Taylor
Added employee ID 1009: Helen Anderson
Added employee ID 1006: Ian Thomas
Sample employee data created successfully!
===== Employee Record Management System =====
1. Create Sample Employee Data
2. Add Employee
3. Search Employee by ID
4. Display All Employees (Sorted by ID)
5. Display Tree Structure
6. Count Employees
7. Find Employee with Min/Max ID
8. Calculate Average Salary
9. Find Employees by Salary Range
10. Find Employees by Department
11. Update Employee Salary
12. Exit
==========================================
Enter your choice: 4
All Employees (Sorted by Employee ID):
ID	Name			Dept		Salary
--	----			----		------
1001	Alice Johnson     	IT        	75000.00
1002	Edward Davis      	Marketing 	60000.00
1003	Charlie Brown     	Finance   	70000.00
1004	George Taylor     	HR        	62000.00
1005	Bob Smith         	HR        	65000.00
1006	Ian Thomas        	Marketing 	63000.00
1007	Fiona Miller      	Finance   	72000.00
1008	Diana Wilson      	IT        	80000.00
1009	Helen Anderson    	IT        	85000.00
===== Employee Record Management System =====
1. Create Sample Employee Data
2. Add Employee
3. Search Employee by ID
4. Display All Employees (Sorted by ID)
5. Display Tree Structure
6. Count Employees
7. Find Employee with Min/Max ID
8. Calculate Average Salary
9. Find Employees by Salary Range
10. Find Employees by Department
11. Update Employee Salary
12. Exit
==========================================
Enter your choice: 3
Enter employee ID to search: 1008
Employee Found:
ID: 1008
Name: Diana Wilson
Department: IT
Salary: 80000.00
===== Employee Record Management System =====
1. Create Sample Employee Data
2. Add Employee
3. Search Employee by ID
4. Display All Employees (Sorted by ID)
5. Display Tree Structure
6. Count Employees
7. Find Employee with Min/Max ID
8. Calculate Average Salary
9. Find Employees by Salary Range
10. Find Employees by Department
11. Update Employee Salary
12. Exit
==========================================
Enter your choice: 8
Average salary of all employees: 71333.33
===== Employee Record Management System =====
1. Create Sample Employee Data
2. Add Employee
3. Search Employee by ID
4. Display All Employees (Sorted by ID)
5. Display Tree Structure
6. Count Employees
7. Find Employee with Min/Max ID
8. Calculate Average Salary
9. Find Employees by Salary Range
10. Find Employees by Department
11. Update Employee Salary
12. Exit
==========================================
Enter your choice: 9
Enter minimum salary: 70000
Enter maximum salary: 80000
Employees with salary between 70000.00 and 80000.00:
ID	Name			Dept		Salary
--	----			----		------
1001	Alice Johnson     	IT        	75000.00
1003	Charlie Brown     	Finance   	70000.00
1007	Fiona Miller      	Finance   	72000.00
1008	Diana Wilson      	IT        	80000.00
```

## Dry Run

For creating a sample employee BST with IDs [1001, 1005, 1003, 1008, 1002, 1007, 1004, 1009, 1006]:

1. **BST Construction**:
   - Insert 1001 - root: 1001
   - Insert 1005 - 1005 > 1001, go right: 1001(null,1005)
   - Insert 1003 - 1003 > 1001, go right, 1003 < 1005, go left: 1001(null,1005(1003,null))
   - Insert 1008 - 1008 > 1001, go right, 1008 > 1005, go right: 1001(null,1005(1003,null,null,1008))
   - Insert 1002 - 1002 > 1001, go right, 1002 < 1005, go left, 1002 < 1003, go left: 1001(null,1005(1003(1002,null),null,null,1008))
   - Insert 1007 - 1007 > 1001, go right, 1007 > 1005, go right, 1007 < 1008, go left: 1001(null,1005(1003(1002,null),null,1008(1007,null)))
   - Insert 1004 - 1004 > 1001, go right, 1004 < 1005, go left, 1004 > 1003, go right: 1001(null,1005(1003(1002,null,1004),null,1008(1007,null)))
   - Insert 1009 - 1009 > 1001, go right, 1009 > 1005, go right, 1009 > 1008, go right: 1001(null,1005(1003(1002,null,1004),null,1008(1007,null,null,1009)))
   - Insert 1006 - 1006 > 1001, go right, 1006 > 1005, go right, 1006 < 1008, go left, 1006 < 1007, go left: 1001(null,1005(1003(1002,null,1004),null,1008(1007(1006,null),null,null,1009)))

Final BST structure:
```
                1001
                   \
                   1005
                   /  \
                1003   1008
                / \    /  \
              1002 1004 1007 1009
                        /
                      1006
```

2. **Search Employee (ID 1008)**:
   - searchEmployee_rrd(1001, 1008):
     * 1008 > 1001, go to right subtree
     * searchEmployee_rrd(1005, 1008):
       - 1008 > 1005, go to right subtree
       - searchEmployee_rrd(1008, 1008):
         * 1008 == 1008, return node with ID 1008
   - Result: Employee Diana Wilson found

3. **Display Employees (Inorder - Sorted by ID)**:
   - displayEmployees_rrd(1001):
     * displayEmployees_rrd(null): (nothing)
     * Print 1001: Alice Johnson
     * displayEmployees_rrd(1005):
       - displayEmployees_rrd(1003):
         * displayEmployees_rrd(1002):
           + displayEmployees_rrd(null): (nothing)
           + Print 1002: Edward Davis
           + displayEmployees_rrd(null): (nothing)
         * Print 1003: Charlie Brown
         * displayEmployees_rrd(1004):
           + displayEmployees_rrd(null): (nothing)
           + Print 1004: George Taylor
           + displayEmployees_rrd(null): (nothing)
       - Print 1005: Bob Smith
       - displayEmployees_rrd(1008):
         * displayEmployees_rrd(1007):
           - displayEmployees_rrd(1006):
             + displayEmployees_rrd(null): (nothing)
             + Print 1006: Ian Thomas
             + displayEmployees_rrd(null): (nothing)
           - Print 1007: Fiona Miller
           - displayEmployees_rrd(null): (nothing)
         * Print 1008: Diana Wilson
         * displayEmployees_rrd(1009):
           + displayEmployees_rrd(null): (nothing)
           + Print 1009: Helen Anderson
           + displayEmployees_rrd(null): (nothing)
   - Result: Employees displayed in ascending order of IDs: 1001, 1002, 1003, 1004, 1005, 1006, 1007, 1008, 1009

## Conclusion

The implementation demonstrates an efficient employee record management system using Binary Search Tree. Key features include:

1. **BST-based Storage**: Employees stored in BST for O(log n) average search time
2. **Sorted Display**: Inorder traversal provides ascending order by empId
3. **Comprehensive Operations**: Search, insert, and various query operations
4. **Memory Management**: Proper allocation and deallocation

**Time Complexities**:
- Insert Employee: O(h) where h is height of tree (O(log n) average, O(n) worst case)
- Search Employee: O(h) where h is height of tree
- Display Employees: O(n) where n is number of employees
- All operations depend on tree height

**Space Complexity**: O(n) for storing n employees, O(h) for recursion stack

The BST approach is ideal for this application because:
1. **Efficient Search**: O(log n) average time for employee lookup
2. **Automatic Sorting**: Employees sorted by ID during insertion
3. **Dynamic Operations**: Can add employees at any time
4. **Range Queries**: Can efficiently find employees in salary ranges

The implementation handles edge cases properly:
- Empty employee list
- Duplicate employee IDs
- Invalid input validation
- Memory management to prevent leaks

Additional features beyond requirements:
- Employee count and statistics
- Salary range queries
- Department-based filtering
- Salary updates
- Tree structure visualization
- Interactive employee addition
- Min/max employee ID finding
- Average salary calculation
- Comprehensive menu system

In real-world applications, this system could be extended to:
1. **Database Integration**: Store data in persistent storage
2. **Multi-field Indexing**: Create BSTs for different fields (name, department, etc.)
3. **Batch Operations**: Import/export employee data from files
4. **Security Features**: Add authentication and access control
5. **Reporting**: Generate detailed reports and analytics
6. **Web Interface**: Create a web-based version
7. **Backup/Restore**: Add data backup and recovery features

The system correctly maintains employee records:
1. **Unique IDs**: Each employee has a unique identifier
2. **Sorted Access**: Employees can be viewed in ID order
3. **Efficient Search**: Quick lookup by employee ID
4. **Data Integrity**: Proper validation of input data

This implementation provides a solid foundation for understanding how BSTs can be applied to real-world problems like employee management systems, demonstrating both the data structure concepts and practical application.
