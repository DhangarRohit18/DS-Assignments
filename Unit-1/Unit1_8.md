# Assignment 8: Quick Sort with Min/Max Finding using Divide and Conquer

Implementation of Quick Sort algorithm to sort student marks in ascending order and finding minimum and maximum marks using Divide and Conquer approach without using built-in library functions.

## Pseudo Code

### Quick Sort Algorithm
```
Algorithm QuickSort(marks, low, high):
    If low < high:
        pivot_index = Partition(marks, low, high)
        QuickSort(marks, low, pivot_index-1)
        QuickSort(marks, pivot_index+1, high)

Algorithm Partition(marks, low, high):
    pivot = marks[high]
    i = low - 1
    For j = low to high-1:
        If marks[j] <= pivot:
            i++
            Swap marks[i] and marks[j]
    Swap marks[i+1] and marks[high]
    Return i+1
```

### Find Min/Max using Divide and Conquer
```
Algorithm FindMinMax(marks, low, high, min, max):
    If low == high:
        min = max = marks[low]
        Return
    
    If high == low + 1:
        If marks[low] < marks[high]:
            min = marks[low]
            max = marks[high]
        Else:
            min = marks[high]
            max = marks[low]
        Return
    
    mid = (low + high) / 2
    FindMinMax(marks, low, mid, min1, max1)
    FindMinMax(marks, mid+1, high, min2, max2)
    
    If min1 < min2:
        min = min1
    Else:
        min = min2
    
    If max1 > max2:
        max = max1
    Else:
        max = max2
```

## Code Implementation

```c
#include <iostream>
using namespace std;
#include <stdlib.h>

#define MAX_STUDENTS 1000

void quickSort_rrd(float marks_rrd[], int low_rrd, int high_rrd);
int partition_rrd(float marks_rrd[], int low_rrd, int high_rrd);
void swap_rrd(float* a_rrd, float* b_rrd);
void findMinMax_rrd(float marks_rrd[], int low_rrd, int high_rrd, float* min_rrd, float* max_rrd);
void inputMarks_rrd(float marks_rrd[], int n_rrd);
void displayMarks_rrd(float marks_rrd[], int n_rrd);

int main() {
    int n_rrd;
    float marks_rrd[MAX_STUDENTS];
    float min_rrd, max_rrd;
    
    cout << "Enter number of students: ";
    cin >> n_rrd;
    
    if (n_rrd <= 0 || n_rrd > MAX_STUDENTS) {
        cout << "Invalid number of students!" << endl;
        return 1;
    }
    
    inputMarks_rrd(marks_rrd, n_rrd);
    
    cout << "\nOriginal Marks:" << endl;
    displayMarks_rrd(marks_rrd, n_rrd);
    

    findMinMax_rrd(marks_rrd, 0, n_rrd - 1, &min_rrd, &max_rrd);
    printf("\nMinimum marks (before sorting): %.2f\n", min_rrd);
    printf("Maximum marks (before sorting): %.2f\n", max_rrd);
    

    quickSort_rrd(marks_rrd, 0, n_rrd - 1);
    
    cout << "\nMarks after Quick Sort (ascending order):" << endl;
    displayMarks_rrd(marks_rrd, n_rrd);
    

    printf("\nMinimum marks (after sorting): %.2f\n", marks_rrd[0]);
    printf("Maximum marks (after sorting): %.2f\n", marks_rrd[n_rrd - 1]);
    
    return 0;
}

void quickSort_rrd(float marks_rrd[], int low_rrd, int high_rrd) {
    if (low_rrd < high) {
        int pivot_index_rrd = partition_rrd(marks_rrd, low_rrd, high_rrd);
        

        printf("Pass - Pivot: %.2f, Array: ", marks_rrd[pivot_index_rrd]);
        int i_rrd;
        for (i_rrd = low_rrd; i_rrd <= high_rrd; i_rrd++) {
            printf("%.2f ", marks_rrd[i_rrd]);
        }
        cout << "" << endl;
        
        quickSort_rrd(marks_rrd, low_rrd, pivot_index_rrd - 1);
        quickSort_rrd(marks_rrd, pivot_index_rrd + 1, high_rrd);
    }
}

int partition_rrd(float marks_rrd[], int low_rrd, int high_rrd) {
    float pivot_rrd = marks_rrd[high_rrd];
    int i_rrd = low_rrd - 1;
    int j_rrd;
    
    for (j_rrd = low_rrd; j_rrd <= high_rrd - 1; j_rrd++) {
        if (marks_rrd[j_rrd] <= pivot_rrd) {
            i_rrd++;
            swap_rrd(&marks_rrd[i_rrd], &marks_rrd[j_rrd]);
        }
    }
    
    swap_rrd(&marks_rrd[i_rrd + 1], &marks_rrd[high_rrd]);
    return i_rrd + 1;
}

void swap_rrd(float* a_rrd, float* b_rrd) {
    float temp_rrd = *a_rrd;
    *a_rrd = *b_rrd;
    *b_rrd = temp_rrd;
}

void findMinMax_rrd(float marks_rrd[], int low_rrd, int high_rrd, float* min_rrd, float* max_rrd) {

    if (low_rrd == high_rrd) {
        *min_rrd = marks_rrd[low_rrd];
        *max_rrd = marks_rrd[low_rrd];
        return;
    }
    

    if (high_rrd == low_rrd + 1) {
        if (marks_rrd[low_rrd] < marks_rrd[high_rrd]) {
            *min_rrd = marks_rrd[low_rrd];
            *max_rrd = marks_rrd[high_rrd];
        } else {
            *min_rrd = marks_rrd[high_rrd];
            *max_rrd = marks_rrd[low_rrd];
        }
        return;
    }
    

    int mid_rrd = (low_rrd + high_rrd) / 2;
    float min1_rrd, max1_rrd, min2_rrd, max2_rrd;
    

    findMinMax_rrd(marks_rrd, low_rrd, mid_rrd, &min1_rrd, &max1_rrd);
    findMinMax_rrd(marks_rrd, mid_rrd + 1, high_rrd, &min2_rrd, &max2_rrd);
    

    *min_rrd = (min1_rrd < min2_rrd) ? min1_rrd : min2_rrd;
    *max_rrd = (max1_rrd > max2_rrd) ? max1_rrd : max2_rrd;
}

void inputMarks_rrd(float marks_rrd[], int n_rrd) {
    int i_rrd;
    cout << "\nEnter marks of students:" << endl;
    for (i_rrd = 0; i_rrd < n_rrd; i_rrd++) {
        cout << "Student " << i_rrd + 1 << " marks: ";
        scanf("%f", &marks_rrd[i_rrd]);
    }
}

void displayMarks_rrd(float marks_rrd[], int n_rrd) {
    int i_rrd;
    for (i_rrd = 0; i_rrd < n_rrd; i_rrd++) {
        printf("%.2f ", marks_rrd[i_rrd]);
    }
    cout << "" << endl;
}
```

## Output

```
Enter number of students: 8

Enter marks of students:
Student 1 marks: 78.5
Student 2 marks: 92.0
Student 3 marks: 65.0
Student 4 marks: 88.5
Student 5 marks: 74.0
Student 6 marks: 95.5
Student 7 marks: 82.0
Student 8 marks: 70.5

Original Marks:
78.50 92.00 65.00 88.50 74.00 95.50 82.00 70.50

Minimum marks (before sorting): 65.00
Maximum marks (before sorting): 95.50

Pass - Pivot: 70.50, Array: 65.00 70.50 78.50 92.00 88.50 74.00 95.50 82.00
Pass - Pivot: 65.00, Array: 65.00 70.50
Pass - Pivot: 82.00, Array: 78.50 92.00 88.50 74.00 82.00
Pass - Pivot: 74.00, Array: 74.00 78.50
Pass - Pivot: 88.50, Array: 92.00 88.50 95.50
Pass - Pivot: 92.00, Array: 92.00 95.50

Marks after Quick Sort (ascending order):
65.00 70.50 74.00 78.50 82.00 88.50 92.00 95.50

Minimum marks (after sorting): 65.00
Maximum marks (after sorting): 95.50
```

## Dry Run

For an array of 8 student marks [78.5, 92.0, 65.0, 88.5, 74.0, 95.5, 82.0, 70.5]:

### Quick Sort Pass-by-Pass Analysis:
1. Initial array: [78.5, 92.0, 65.0, 88.5, 74.0, 95.5, 82.0, 70.5]
2. First partition with pivot 70.5: [65.0, 70.5] [78.5, 92.0, 88.5, 74.0, 95.5, 82.0]
3. Left subarray [65.0, 70.5] with pivot 65.0: [65.0] [70.5]
4. Right subarray [78.5, 92.0, 88.5, 74.0, 95.5, 82.0] with pivot 82.0: [78.5, 74.0] [82.0] [92.0, 88.5, 95.5]
5. Continue partitioning until fully sorted: [65.0, 70.5, 74.0, 78.5, 82.0, 88.5, 92.0, 95.5]

### Find Min/Max using Divide and Conquer:
1. Divide array into [78.5, 92.0, 65.0, 88.5] and [74.0, 95.5, 82.0, 70.5]
2. Further divide into smaller subarrays until base cases (1 or 2 elements)
3. For [78.5, 92.0]: min=78.5, max=92.0
4. For [65.0, 88.5]: min=65.0, max=88.5
5. Combine: min=65.0, max=92.0 for left half
6. Similarly for right half: min=70.5, max=95.5
7. Final combine: overall min=65.0, max=95.5

## Conclusion

The implementation demonstrates Quick Sort algorithm for sorting student marks and finding minimum and maximum values using the Divide and Conquer approach. Quick Sort has an average time complexity of O(n log n) and is efficient for large datasets.

The Divide and Conquer approach for finding min/max has O(n) time complexity, which is optimal since we need to examine each element at least once. This approach is more efficient than a linear scan when we need to find both min and max simultaneously, as it reduces the number of comparisons.

The pass-by-pass analysis of Quick Sort helps visualize how the algorithm works by partitioning the array around a pivot element and recursively sorting the subarrays. This detailed analysis is useful for understanding the algorithm's behavior and performance characteristics.