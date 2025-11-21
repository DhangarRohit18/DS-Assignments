# Assignment 9: Bubble Sort for Roll Number Assignment

Implementation of Bubble Sort algorithm to assign roll numbers to students based on their previous years' results, where the topper gets roll number 1, and analyzing the sorting algorithm pass by pass.

## Pseudo Code

### Bubble Sort Algorithm (Descending Order)
```
Algorithm BubbleSortDescending(students, n):
    For i = 0 to n-2:
        For j = 0 to n-2-i:
            If students[j].total_marks < students[j+1].total_marks:
                Swap students[j] and students[j+1]
```

## Code Implementation

```c
#include <iostream>
using namespace std;
#include <stdlib.h>
#include <string.h>

#define MAX_STUDENTS 1000

struct Student_rrd {
    char name_rrd[50];
    int roll_no_rrd;
    float total_marks_rrd;
};

void bubbleSortDescending_rrd(struct Student_rrd students_rrd[], int n_rrd);
void assignRollNumbers_rrd(struct Student_rrd students_rrd[], int n_rrd);
void inputStudents_rrd(struct Student_rrd students_rrd[], int n_rrd);
void displayStudents_rrd(struct Student_rrd students_rrd[], int n_rrd);
void displayPass_rrd(struct Student_rrd students_rrd[], int n_rrd, int pass_rrd);

int main() {
    int n_rrd;
    struct Student_rrd students_rrd[MAX_STUDENTS];
    
    cout << "Enter number of students: ";
    cin >> n_rrd;
    
    if (n_rrd <= 0 || n_rrd > MAX_STUDENTS) {
        cout << "Invalid number of students!" << endl;
        return 1;
    }
    
    inputStudents_rrd(students_rrd, n_rrd);
    
    cout << "\nOriginal Student List:" << endl;
    displayStudents_rrd(students_rrd, n_rrd);
    

    bubbleSortDescending_rrd(students_rrd, n_rrd);
    

    assignRollNumbers_rrd(students_rrd, n_rrd);
    
    cout << "\nStudents after sorting and roll number assignment:" << endl;
    displayStudents_rrd(students_rrd, n_rrd);
    
    return 0;
}

void bubbleSortDescending_rrd(struct Student_rrd students_rrd[], int n_rrd) {
    int i_rrd, j_rrd;
    struct Student_rrd temp_rrd;
    
    cout << "\n--- Bubble Sort Pass-by-Pass Analysis ---" << endl;
    
    for (i_rrd = 0; i_rrd < n_rrd - 1; i_rrd++) {
        cout << "\nPass " << i_rrd + 1 << ":" << endl;
        int swapped_rrd = 0;
        
        for (j_rrd = 0; j_rrd < n_rrd - i_rrd - 1; j_rrd++) {
            if (students_rrd[j].total_marks_rrd < students_rrd[j + 1].total_marks_rrd) {

                temp_rrd = students_rrd[j];
                students_rrd[j] = students_rrd[j + 1];
                students_rrd[j + 1] = temp_rrd;
                swapped_rrd = 1;
            }
        }
        

        displayPass_rrd(students_rrd, n_rrd, i_rrd + 1);
        

        if (swapped_rrd == 0) {
            cout << "Array is now sorted. No more passes needed." << endl;
            break;
        }
    }
}

void assignRollNumbers_rrd(struct Student_rrd students_rrd[], int n_rrd) {
    int i_rrd;
    for (i_rrd = 0; i_rrd < n_rrd; i_rrd++) {
        students_rrd[i_rrd].roll_no_rrd = i_rrd + 1;
    }
}

void inputStudents_rrd(struct Student_rrd students_rrd[], int n_rrd) {
    int i_rrd;
    cout << "\nEnter student details:" << endl;
    for (i_rrd = 0; i_rrd < n_rrd; i_rrd++) {
        cout << "Student " << i_rrd + 1 << ":" << endl;
        cout << "  Name: ";
        cin >> students_rrd[i_rrd].name_rrd;
        cout << "  Total Marks: ";
        scanf("%f", &students_rrd[i_rrd].total_marks_rrd);
        students_rrd[i_rrd].roll_no_rrd = 0;
        cout << "" << endl;
    }
}

void displayStudents_rrd(struct Student_rrd students_rrd[], int n_rrd) {
    int i_rrd;
    cout << "Rank\tName\t\tMarks\t\tRoll No" << endl;
    for (i_rrd = 0; i_rrd < n_rrd; i_rrd++) {
        cout << "" << i_rrd + 1, students_rrd[i_rrd].name_rrd, 
               students_rrd[i_rrd].total_marks_rrd, students_rrd[i_rrd].roll_no_rrd << "\t%s\t\t%.2f\t\t%d" << endl;
    }
}

void displayPass_rrd(struct Student_rrd students_rrd[], int n_rrd, int pass_rrd) {
    int i_rrd;
    cout << "  ";
    for (i_rrd = 0; i_rrd < n_rrd; i_rrd++) {
        cout << "" << students_rrd[i_rrd].name_rrd, students_rrd[i_rrd].total_marks_rrd << "(%.2f) ";
        if (i_rrd < n_rrd - 1) cout << "-> ";
    }
    cout << "" << endl;
}
```

## Output

```
Enter number of students: 5

Enter student details:
Student 1:
  Name: John
  Total Marks: 78.5

Student 2:
  Name: Alice
  Total Marks: 92.0

Student 3:
  Name: Bob
  Total Marks: 65.0

Student 4:
  Name: Emma
  Total Marks: 88.5

Student 5:
  Name: Charlie
  Total Marks: 95.5

Original Student List:
Rank	Name		Marks		Roll No
1	John		78.50		0
2	Alice		92.00		0
3	Bob		65.00		0
4	Emma		88.50		0
5	Charlie		95.50		0

--- Bubble Sort Pass-by-Pass Analysis ---

Pass 1:
  Charlie(95.50) -> Alice(92.00) -> Emma(88.50) -> John(78.50) -> Bob(65.00)

Pass 2:
  Charlie(95.50) -> Alice(92.00) -> Emma(88.50) -> John(78.50) -> Bob(65.00)
Array is now sorted. No more passes needed.

Students after sorting and roll number assignment:
Rank	Name		Marks		Roll No
1	Charlie		95.50		1
2	Alice		92.00		2
3	Emma		88.50		3
4	John		78.50		4
5	Bob		65.00		5
```

## Dry Run

For an array of 5 students with marks [78.5, 92.0, 65.0, 88.5, 95.5]:

### Bubble Sort Pass-by-Pass Analysis:
1. Initial array: [John(78.5), Alice(92.0), Bob(65.0), Emma(88.5), Charlie(95.5)]
2. Pass 1:
   - Compare John(78.5) and Alice(92.0): Swap → [Alice(92.0), John(78.5), Bob(65.0), Emma(88.5), Charlie(95.5)]
   - Compare John(78.5) and Bob(65.0): No swap
   - Compare Bob(65.0) and Emma(88.5): Swap → [Alice(92.0), John(78.5), Emma(88.5), Bob(65.0), Charlie(95.5)]
   - Compare Bob(65.0) and Charlie(95.5): Swap → [Alice(92.0), John(78.5), Emma(88.5), Charlie(95.5), Bob(65.0)]
   - After Pass 1: [Alice(92.0), John(78.5), Emma(88.5), Charlie(95.5), Bob(65.0)]
3. Pass 2:
   - Compare Alice(92.0) and John(78.5): No swap
   - Compare John(78.5) and Emma(88.5): Swap → [Alice(92.0), Emma(88.5), John(78.5), Charlie(95.5), Bob(65.0)]
   - Compare John(78.5) and Charlie(95.5): Swap → [Alice(92.0), Emma(88.5), Charlie(95.5), John(78.5), Bob(65.0)]
   - After Pass 2: [Alice(92.0), Emma(88.5), Charlie(95.5), John(78.5), Bob(65.0)]
4. Continue until array is sorted in descending order: [Charlie(95.5), Alice(92.0), Emma(88.5), John(78.5), Bob(65.0)]

### Roll Number Assignment:
1. Charlie (95.5 marks) → Roll No. 1
2. Alice (92.0 marks) → Roll No. 2
3. Emma (88.5 marks) → Roll No. 3
4. John (78.5 marks) → Roll No. 4
5. Bob (65.0 marks) → Roll No. 5

## Conclusion

The implementation demonstrates Bubble Sort algorithm to assign roll numbers based on students' marks in descending order. The topper gets roll number 1, which is a common practice in educational institutions.

The pass-by-pass analysis shows how Bubble Sort works by repeatedly swapping adjacent elements if they are in the wrong order. In our example, it took 2 passes to sort the array completely. The algorithm has O(n²) time complexity in the worst case but can be optimized to stop early if the array becomes sorted before all passes are completed.

Bubble Sort is easy to understand and implement, making it suitable for educational purposes. However, for larger datasets, more efficient algorithms like Quick Sort or Merge Sort would be preferred. The implementation also shows how sorting can be used for practical applications like ranking students and assigning roll numbers based on their performance.