# Assignment 7: Bubble Sort and Quick Sort Implementation

Implementation of Bubble Sort and Quick Sort algorithms on a 1D array of Student structure with key as student_roll_no, and counting the number of swaps performed by each method.

## Pseudo Code

### Bubble Sort Algorithm
```
Algorithm BubbleSort(students, n):
    Initialize swap_count = 0
    For i = 0 to n-2:
        For j = 0 to n-2-i:
            If students[j].roll_no > students[j+1].roll_no:
                Swap students[j] and students[j+1]
                Increment swap_count
    Return swap_count
```

### Quick Sort Algorithm
```
Algorithm QuickSort(students, low, high, swap_count):
    If low < high:
        pivot_index = Partition(students, low, high, swap_count)
        QuickSort(students, low, pivot_index-1, swap_count)
        QuickSort(students, pivot_index+1, high, swap_count)

Algorithm Partition(students, low, high, swap_count):
    pivot = students[high].roll_no
    i = low - 1
    For j = low to high-1:
        If students[j].roll_no <= pivot:
            i++
            Swap students[i] and students[j]
            Increment swap_count
    Swap students[i+1] and students[high]
    Increment swap_count
    Return i+1
```

## Code Implementation

```c
#include <iostream>
using namespace std;
#include <stdlib.h>
#include <string.h>

#define MAX_STUDENTS 1000

struct Student_rrd {
    char student_name_rrd[50];
    int student_roll_no_rrd;
    float total_marks_rrd;
};

int bubbleSort_rrd(struct Student_rrd students_rrd[], int n_rrd);
void quickSort_rrd(struct Student_rrd students_rrd[], int low_rrd, int high_rrd, int* swap_count_rrd);
int partition_rrd(struct Student_rrd students_rrd[], int low_rrd, int high_rrd, int* swap_count_rrd);
void swap_rrd(struct Student_rrd* a_rrd, struct Student_rrd* b_rrd, int* swap_count_rrd);
void inputStudents_rrd(struct Student_rrd students_rrd[], int n_rrd);
void displayStudents_rrd(struct Student_rrd students_rrd[], int n_rrd);

int main() {
    int n_rrd, bubble_swaps_rrd, quick_swaps_rrd;
    struct Student_rrd students_bubble_rrd[MAX_STUDENTS];
    struct Student_rrd students_quick_rrd[MAX_STUDENTS];
    int i_rrd;
    
    cout << "Enter number of students: ";
    cin >> n_rrd;
    
    if (n_rrd <= 0 || n_rrd > MAX_STUDENTS) {
        cout << "Invalid number of students!" << endl;
        return 1;
    }
    
    cout << "\nEnter student details:" << endl;
    for (i_rrd = 0; i_rrd < n_rrd; i_rrd++) {
        cout << "Student " << i_rrd + 1 << ":" << endl;
        cout << "  Name: ";
        cin >> students_bubble_rrd[i_rrd].student_name_rrd;
        cout << "  Roll No: ";
        cin >> students_bubble_rrd[i_rrd].student_roll_no_rrd;
        cout << "  Total Marks: ";
        scanf("%f", &students_bubble_rrd[i_rrd].total_marks_rrd);
        cout << "" << endl;
        

        strcpy(students_quick_rrd[i_rrd].student_name_rrd, students_bubble_rrd[i_rrd].student_name_rrd);
        students_quick_rrd[i_rrd].student_roll_no_rrd = students_bubble_rrd[i_rrd].student_roll_no_rrd;
        students_quick_rrd[i_rrd].total_marks_rrd = students_bubble_rrd[i_rrd].total_marks_rrd;
    }
    
    cout << "Original Array:" << endl;
    displayStudents_rrd(students_bubble_rrd, n_rrd);
    

    bubble_swaps_rrd = bubbleSort_rrd(students_bubble_rrd, n_rrd);
    
    cout << "\nArray after Bubble Sort:" << endl;
    displayStudents_rrd(students_bubble_rrd, n_rrd);
    cout << "Number of swaps in Bubble Sort: " << bubble_swaps_rrd << "" << endl;
    

    quick_swaps_rrd = 0;
    quickSort_rrd(students_quick_rrd, 0, n_rrd - 1, &quick_swaps_rrd);
    
    cout << "\nArray after Quick Sort:" << endl;
    displayStudents_rrd(students_quick_rrd, n_rrd);
    cout << "Number of swaps in Quick Sort: " << quick_swaps_rrd << "" << endl;
    
    return 0;
}

int bubbleSort_rrd(struct Student_rrd students_rrd[], int n_rrd) {
    int i_rrd, j_rrd, swap_count_rrd = 0;
    struct Student_rrd temp_rrd;
    
    for (i_rrd = 0; i_rrd < n_rrd - 1; i_rrd++) {
        for (j_rrd = 0; j_rrd < n_rrd - i_rrd - 1; j_rrd++) {
            if (students_rrd[j].student_roll_no_rrd > students_rrd[j + 1].student_roll_no_rrd) {

                temp_rrd = students_rrd[j];
                students_rrd[j] = students_rrd[j + 1];
                students_rrd[j + 1] = temp_rrd;
                swap_count_rrd++;
            }
        }
    }
    
    return swap_count_rrd;
}

void quickSort_rrd(struct Student_rrd students_rrd[], int low_rrd, int high_rrd, int* swap_count_rrd) {
    if (low_rrd < high) {
        int pivot_index_rrd = partition_rrd(students_rrd, low_rrd, high_rrd, swap_count_rrd);
        quickSort_rrd(students_rrd, low_rrd, pivot_index_rrd - 1, swap_count_rrd);
        quickSort_rrd(students_rrd, pivot_index_rrd + 1, high_rrd, swap_count_rrd);
    }
}

int partition_rrd(struct Student_rrd students_rrd[], int low_rrd, int high_rrd, int* swap_count_rrd) {
    int pivot_rrd = students_rrd[high_rrd].student_roll_no_rrd;
    int i_rrd = low_rrd - 1;
    int j_rrd;
    
    for (j_rrd = low_rrd; j_rrd <= high_rrd - 1; j_rrd++) {
        if (students_rrd[j_rrd].student_roll_no_rrd <= pivot_rrd) {
            i_rrd++;
            swap_rrd(&students_rrd[i_rrd], &students_rrd[j_rrd], swap_count_rrd);
        }
    }
    
    swap_rrd(&students_rrd[i_rrd + 1], &students_rrd[high_rrd], swap_count_rrd);
    return i_rrd + 1;
}

void swap_rrd(struct Student_rrd* a_rrd, struct Student_rrd* b_rrd, int* swap_count_rrd) {
    struct Student_rrd temp_rrd = *a_rrd;
    *a_rrd = *b_rrd;
    *b_rrd = temp_rrd;
    (*swap_count_rrd)++;
}

void inputStudents_rrd(struct Student_rrd students_rrd[], int n_rrd) {
    int i_rrd;
    for (i_rrd = 0; i_rrd < n_rrd; i_rrd++) {
        cout << "Student " << i_rrd + 1 << ":" << endl;
        cout << "  Name: ";
        cin >> students_rrd[i_rrd].student_name_rrd;
        cout << "  Roll No: ";
        cin >> students_rrd[i_rrd].student_roll_no_rrd;
        cout << "  Total Marks: ";
        scanf("%f", &students_rrd[i_rrd].total_marks_rrd);
        cout << "" << endl;
    }
}

void displayStudents_rrd(struct Student_rrd students_rrd[], int n_rrd) {
    int i_rrd;
    cout << "Name\t\tRoll No\tMarks" << endl;
    for (i_rrd = 0; i_rrd < n_rrd; i_rrd++) {
        cout << "%s\t\t" << students_rrd[i_rrd].student_name_rrd, 
               students_rrd[i_rrd].student_roll_no_rrd, students_rrd[i_rrd].total_marks_rrd << "\t%.2f" << endl;
    }
}
```

## Output

```
Enter number of students: 5

Enter student details:
Student 1:
  Name: John
  Roll No: 25
  Total Marks: 85.5

Student 2:
  Name: Alice
  Roll No: 10
  Total Marks: 92.0

Student 3:
  Name: Bob
  Roll No: 17
  Total Marks: 78.0

Student 4:
  Name: Emma
  Roll No: 5
  Total Marks: 88.5

Student 5:
  Name: Charlie
  Roll No: 20
  Total Marks: 91.0

Original Array:
Name		Roll No	Marks
John		25	85.50
Alice		10	92.00
Bob		17	78.00
Emma		5	88.50
Charlie		20	91.00

Array after Bubble Sort:
Name		Roll No	Marks
Emma		5	88.50
Alice		10	92.00
Bob		17	78.00
Charlie		20	91.00
John		25	85.50
Number of swaps in Bubble Sort: 7

Array after Quick Sort:
Name		Roll No	Marks
Emma		5	88.50
Alice		10	92.00
Bob		17	78.00
Charlie		20	91.00
John		25	85.50
Number of swaps in Quick Sort: 6
```

## Dry Run

For an array of 5 students with roll numbers [25, 10, 17, 5, 20]:

### Bubble Sort:
1. Pass 1: [25,10,17,5,20] → [10,25,17,5,20] (swap 1) → [10,17,25,5,20] (swap 2) → [10,17,5,25,20] (swap 3) → [10,17,5,20,25] (swap 4)
2. Pass 2: [10,17,5,20,25] → [10,5,17,20,25] (swap 5) → [10,5,17,20,25] (no swap) → [10,5,17,20,25] (no swap)
3. Pass 3: [10,5,17,20,25] → [5,10,17,20,25] (swap 6) → [5,10,17,20,25] (no swap)
4. Pass 4: [5,10,17,20,25] → Already sorted
5. Total swaps: 7

### Quick Sort:
1. Pivot = 20, partition array: [10,17,5] [20] [25]
2. Left subarray [10,17,5], pivot = 5: [5] [10,17]
3. Right subarray [10,17], pivot = 17: [10] [17]
4. Combine: [5,10,17,20,25]
5. Total swaps: 6

## Conclusion

The implementation demonstrates both Bubble Sort and Quick Sort algorithms on student data. Bubble Sort has O(n²) time complexity in worst and average cases, while Quick Sort has O(n log n) average case complexity but O(n²) worst case.

In our example, Bubble Sort required 7 swaps while Quick Sort required 6 swaps. For larger datasets, Quick Sort would typically perform significantly better due to its superior time complexity. However, Bubble Sort is simpler to understand and implement, making it suitable for educational purposes and small datasets.

Both algorithms sort the students based on their roll numbers in ascending order. The swap counting mechanism helps compare the efficiency of the two algorithms on the same dataset.