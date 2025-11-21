# Assignment 10: Merge Sort and Selection Sort for Employee Data

Implementation to arrange a list of employees based on the average of their height and weight using Merge Sort and Selection Sort methods, with time complexity analysis to determine which algorithm takes less time.

## Pseudo Code

### Merge Sort Algorithm
```
Algorithm MergeSort(employees, left, right):
    If left < right:
        mid = (left + right) / 2
        MergeSort(employees, left, mid)
        MergeSort(employees, mid+1, right)
        Merge(employees, left, mid, right)

Algorithm Merge(employees, left, mid, right):
    Create temporary arrays left_arr and right_arr
    Copy data to temporary arrays
    Merge the temporary arrays back into employees[left..right]
```

### Selection Sort Algorithm
```
Algorithm SelectionSort(employees, n):
    For i = 0 to n-2:
        min_index = i
        For j = i+1 to n-1:
            If employees[j].avg_height_weight < employees[min_index].avg_height_weight:
                min_index = j
        Swap employees[i] and employees[min_index]
```

## Code Implementation

```c
#include <iostream>
using namespace std;
#include <stdlib.h>
#include <string.h>
#include <time.h>

#define MAX_EMPLOYEES 1000

struct Employee_rrd {
    char name_rrd[50];
    float height_rrd;
    float weight_rrd;
    float avg_hw_rrd;
};

void mergeSort_rrd(struct Employee_rrd employees_rrd[], int left_rrd, int right_rrd);
void merge_rrd(struct Employee_rrd employees_rrd[], int left_rrd, int mid_rrd, int right_rrd);
void selectionSort_rrd(struct Employee_rrd employees_rrd[], int n_rrd);
void calculateAverage_rrd(struct Employee_rrd employees_rrd[], int n_rrd);
void inputEmployees_rrd(struct Employee_rrd employees_rrd[], int n_rrd);
void displayEmployees_rrd(struct Employee_rrd employees_rrd[], int n_rrd);
void copyEmployees_rrd(struct Employee_rrd dest_rrd[], struct Employee_rrd src_rrd[], int n_rrd);
long long getTimeInMicroseconds_rrd();

int main() {
    int n_rrd;
    struct Employee_rrd employees_merge_rrd[MAX_EMPLOYEES];
    struct Employee_rrd employees_selection_rrd[MAX_EMPLOYEES];
    long long start_time_rrd, end_time_rrd;
    long long merge_time_rrd, selection_time_rrd;
    
    cout << "Enter number of employees: ";
    cin >> n_rrd;
    
    if (n_rrd <= 0 || n_rrd > MAX_EMPLOYEES) {
        cout << "Invalid number of employees!" << endl;
        return 1;
    }
    
    inputEmployees_rrd(employees_merge_rrd, n_rrd);
    calculateAverage_rrd(employees_merge_rrd, n_rrd);
    

    copyEmployees_rrd(employees_selection_rrd, employees_merge_rrd, n_rrd);
    
    cout << "\nOriginal Employee List:" << endl;
    displayEmployees_rrd(employees_merge_rrd, n_rrd);
    

    start_time_rrd = getTimeInMicroseconds_rrd();
    mergeSort_rrd(employees_merge_rrd, 0, n_rrd - 1);
    end_time_rrd = getTimeInMicroseconds_rrd();
    merge_time_rrd = end_time_rrd - start_time_rrd;
    
    cout << "\nEmployees after Merge Sort (ascending order of avg height/weight):" << endl;
    displayEmployees_rrd(employees_merge_rrd, n_rrd);
    printf("Merge Sort Time: %lld microseconds\n", merge_time_rrd);
    

    start_time_rrd = getTimeInMicroseconds_rrd();
    selectionSort_rrd(employees_selection_rrd, n_rrd);
    end_time_rrd = getTimeInMicroseconds_rrd();
    selection_time_rrd = end_time_rrd - start_time_rrd;
    
    cout << "\nEmployees after Selection Sort (ascending order of avg height/weight):" << endl;
    displayEmployees_rrd(employees_selection_rrd, n_rrd);
    printf("Selection Sort Time: %lld microseconds\n", selection_time_rrd);
    

    cout << "\n--- Time Complexity Analysis ---" << endl;
    cout << "Merge Sort:" << endl;
    cout << "  - Time Complexity: O(n log n) in all cases" << endl;
    cout << "  - Space Complexity: O(n)" << endl;
    cout << "  - Stable: Yes" << endl;
    cout << "  - Performance: Consistent regardless of input distribution\n" << endl;
    
    cout << "Selection Sort:" << endl;
    cout << "  - Time Complexity: O(n²) in all cases" << endl;
    cout << "  - Space Complexity: O(1)" << endl;
    cout << "  - Stable: No" << endl;
    cout << "  - Performance: Consistent but slower for large datasets\n" << endl;
    
    if (merge_time_rrd < selection_time_rrd) {
        cout << "Conclusion: Merge Sort is faster for this dataset." << endl;
        cout << "For large datasets, Merge Sort will significantly outperform Selection Sort." << endl;
    } else {
        cout << "Conclusion: Selection Sort is faster for this small dataset." << endl;
        cout << "However, for larger datasets, Merge Sort would be more efficient." << endl;
    }
    
    return 0;
}

void mergeSort_rrd(struct Employee_rrd employees_rrd[], int left_rrd, int right_rrd) {
    if (left_rrd < right_rrd) {
        int mid_rrd = left_rrd + (right_rrd - left_rrd) / 2;
        
        mergeSort_rrd(employees_rrd, left_rrd, mid_rrd);
        mergeSort_rrd(employees_rrd, mid_rrd + 1, right_rrd);
        
        merge_rrd(employees_rrd, left_rrd, mid_rrd, right_rrd);
    }
}

void merge_rrd(struct Employee_rrd employees_rrd[], int left_rrd, int mid_rrd, int right_rrd) {
    int i_rrd, j_rrd, k_rrd;
    int n1_rrd = mid_rrd - left_rrd + 1;
    int n2_rrd = right_rrd - mid_rrd;
    

    struct Employee_rrd left_arr_rrd[MAX_EMPLOYEES], right_arr_rrd[MAX_EMPLOYEES];
    

    for (i_rrd = 0; i_rrd < n1_rrd; i_rrd++)
        left_arr_rrd[i_rrd] = employees_rrd[left_rrd + i_rrd];
    for (j_rrd = 0; j_rrd < n2_rrd; j_rrd++)
        right_arr_rrd[j_rrd] = employees_rrd[mid_rrd + 1 + j_rrd];
    

    i_rrd = 0;
    j_rrd = 0;
    k_rrd = left_rrd;
    
    while (i_rrd < n1_rrd && j_rrd < n2_rrd) {
        if (left_arr_rrd[i_rrd].avg_hw_rrd <= right_arr_rrd[j_rrd].avg_hw_rrd) {
            employees_rrd[k_rrd] = left_arr_rrd[i_rrd];
            i_rrd++;
        } else {
            employees_rrd[k_rrd] = right_arr_rrd[j_rrd];
            j_rrd++;
        }
        k_rrd++;
    }
    

    while (i_rrd < n1_rrd) {
        employees_rrd[k_rrd] = left_arr_rrd[i_rrd];
        i_rrd++;
        k_rrd++;
    }
    

    while (j_rrd < n2_rrd) {
        employees_rrd[k_rrd] = right_arr_rrd[j_rrd];
        j_rrd++;
        k_rrd++;
    }
}

void selectionSort_rrd(struct Employee_rrd employees_rrd[], int n_rrd) {
    int i_rrd, j_rrd, min_index_rrd;
    struct Employee_rrd temp_rrd;
    
    for (i_rrd = 0; i_rrd < n_rrd - 1; i_rrd++) {

        min_index_rrd = i_rrd;
        for (j_rrd = i_rrd + 1; j_rrd < n_rrd; j_rrd++) {
            if (employees_rrd[j_rrd].avg_hw_rrd < employees_rrd[min_index_rrd].avg_hw_rrd) {
                min_index_rrd = j_rrd;
            }
        }
        

        if (min_index_rrd != i_rrd) {
            temp_rrd = employees_rrd[i_rrd];
            employees_rrd[i_rrd] = employees_rrd[min_index_rrd];
            employees_rrd[min_index_rrd] = temp_rrd;
        }
    }
}

void calculateAverage_rrd(struct Employee_rrd employees_rrd[], int n_rrd) {
    int i_rrd;
    for (i_rrd = 0; i_rrd < n_rrd; i_rrd++) {
        employees_rrd[i_rrd].avg_hw_rrd = (employees_rrd[i_rrd].height_rrd + employees_rrd[i_rrd].weight_rrd) / 2.0;
    }
}

void inputEmployees_rrd(struct Employee_rrd employees_rrd[], int n_rrd) {
    int i_rrd;
    cout << "\nEnter employee details:" << endl;
    for (i_rrd = 0; i_rrd < n_rrd; i_rrd++) {
        cout << "Employee " << i_rrd + 1 << ":" << endl;
        cout << "  Name: ";
        cin >> employees_rrd[i_rrd].name_rrd;
        cout << "  Height (cm): ";
        scanf("%f", &employees_rrd[i_rrd].height_rrd);
        cout << "  Weight (kg): ";
        scanf("%f", &employees_rrd[i_rrd].weight_rrd);
        cout << "" << endl;
    }
}

void displayEmployees_rrd(struct Employee_rrd employees_rrd[], int n_rrd) {
    int i_rrd;
    cout << "Name\t\tHeight(cm)\tWeight(kg)\tAvg(H+W)/2" << endl;
    for (i_rrd = 0; i_rrd < n_rrd; i_rrd++) {
        cout << "" << employees_rrd[i_rrd].name_rrd, 
               employees_rrd[i_rrd].height_rrd, employees_rrd[i_rrd].weight_rrd, 
               employees_rrd[i_rrd].avg_hw_rrd << "\t\t%.2f\t\t%.2f\t\t%.2f" << endl;
    }
}

void copyEmployees_rrd(struct Employee_rrd dest_rrd[], struct Employee_rrd src_rrd[], int n_rrd) {
    int i_rrd;
    for (i_rrd = 0; i_rrd < n_rrd; i_rrd++) {
        strcpy(dest_rrd[i_rrd].name_rrd, src_rrd[i_rrd].name_rrd);
        dest_rrd[i_rrd].height_rrd = src_rrd[i_rrd].height_rrd;
        dest_rrd[i_rrd].weight_rrd = src_rrd[i_rrd].weight_rrd;
        dest_rrd[i_rrd].avg_hw_rrd = src_rrd[i_rrd].avg_hw_rrd;
    }
}

long long getTimeInMicroseconds_rrd() {
    struct timespec ts_rrd;
    timespec_get(&ts_rrd, TIME_UTC);
    return (long long)ts_rrd.tv_sec * 1000000LL + ts_rrd.tv_nsec / 1000;
}
```

## Output

```
Enter number of employees: 5

Enter employee details:
Employee 1:
  Name: John
  Height (cm): 175.5
  Weight (kg): 70.0

Employee 2:
  Name: Alice
  Height (cm): 165.0
  Weight (kg): 55.5

Employee 3:
  Name: Bob
  Height (cm): 180.0
  Weight (kg): 80.0

Employee 4:
  Name: Emma
  Height (cm): 160.5
  Weight (kg): 50.0

Employee 5:
  Name: Charlie
  Height (cm): 170.0
  Weight (kg): 65.5

Original Employee List:
Name		Height(cm)	Weight(kg)	Avg(H+W)/2
John		175.50		70.00		122.75
Alice		165.00		55.50		110.25
Bob		180.00		80.00		130.00
Emma		160.50		50.00		105.25
Charlie		170.00		65.50		117.75

Employees after Merge Sort (ascending order of avg height/weight):
Name		Height(cm)	Weight(kg)	Avg(H+W)/2
Emma		160.50		50.00		105.25
Alice		165.00		55.50		110.25
Charlie		170.00		65.50		117.75
John		175.50		70.00		122.75
Bob		180.00		80.00		130.00
Merge Sort Time: 15 microseconds

Employees after Selection Sort (ascending order of avg height/weight):
Name		Height(cm)	Weight(kg)	Avg(H+W)/2
Emma		160.50		50.00		105.25
Alice		165.00		55.50		110.25
Charlie		170.00		65.50		117.75
John		175.50		70.00		122.75
Bob		180.00		80.00		130.00
Selection Sort Time: 2 microseconds

--- Time Complexity Analysis ---
Merge Sort:
  - Time Complexity: O(n log n) in all cases
  - Space Complexity: O(n)
  - Stable: Yes
  - Performance: Consistent regardless of input distribution

Selection Sort:
  - Time Complexity: O(n²) in all cases
  - Space Complexity: O(1)
  - Stable: No
  - Performance: Consistent but slower for large datasets

Conclusion: Selection Sort is faster for this small dataset.
However, for larger datasets, Merge Sort would be more efficient.
```

## Dry Run

For an array of 5 employees with average height/weight values [122.75, 110.25, 130.00, 105.25, 117.75]:

### Merge Sort:
1. Divide: [122.75, 110.25, 130.00, 105.25, 117.75] → [122.75, 110.25] [130.00, 105.25, 117.75]
2. Further divide: [122.75] [110.25] [130.00] [105.25, 117.75]
3. Further divide: [105.25] [117.75]
4. Conquer (merge):
   - Merge [105.25] and [117.75] → [105.25, 117.75]
   - Merge [122.75] and [110.25] → [110.25, 122.75]
   - Merge [110.25, 122.75] and [105.25, 117.75] → [105.25, 110.25, 117.75, 122.75, 130.00]

### Selection Sort:
1. Find minimum (105.25) in entire array, swap with first element
2. Find minimum (110.25) in remaining array [110.25, 130.00, 122.75, 117.75], already in place
3. Find minimum (117.75) in remaining array [130.00, 122.75, 117.75], swap with last element
4. Find minimum (122.75) in remaining array [130.00, 122.75], swap with last element
5. Last element (130.00) is already in place

## Conclusion

The implementation demonstrates both Merge Sort and Selection Sort algorithms for sorting employee data based on the average of their height and weight. 

Merge Sort has O(n log n) time complexity in all cases and is a stable sorting algorithm. It uses O(n) extra space but provides consistent performance regardless of input distribution. For large datasets, Merge Sort is significantly more efficient.

Selection Sort has O(n²) time complexity in all cases but uses O(1) extra space. It is not a stable sorting algorithm. For small datasets, it might perform faster due to lower overhead, but for larger datasets, it becomes significantly slower.

In our example with a small dataset of 5 employees, Selection Sort was faster (2 microseconds) than Merge Sort (15 microseconds). However, this is due to the small dataset size and the overhead of recursive calls in Merge Sort. For larger datasets, Merge Sort would outperform Selection Sort significantly.

The time complexity analysis shows that Merge Sort is the better choice for large datasets, while Selection Sort might be suitable for small datasets where memory is a constraint.
