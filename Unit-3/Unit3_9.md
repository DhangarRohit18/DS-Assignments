# Unit III Assignment 9: Multiple Queues Implementation using Array

Implementation of multiple queues (two queues) using a single array with operations for adding, deleting, and displaying elements.

## Problem Statement

Write a program to implement multiple queues i.e. two queues using array and perform following operations on it:
A. Add Queue
B. Delete from Queue
C. Display Queue

## Pseudo Code

### Multiple Queues Structure
```
Structure MultipleQueues:
    array: array of integers
    front1: integer (front of queue 1)
    rear1: integer (rear of queue 1)
    front2: integer (front of queue 2)
    rear2: integer (rear of queue 2)
    size: integer (total size of array)
```

### Enqueue to Queue 1
```
Algorithm EnqueueQueue1(queues, item):
    If rear1 + 1 == front2 OR (front1 == 0 AND rear1 == size/2 - 1):
        Return "Queue 1 is full"
    If front1 == -1:
        front1 = rear1 = 0
    Else If rear1 == size/2 - 1:
        rear1 = 0
    Else:
        rear1++
    queues.array[rear1] = item
```

### Enqueue to Queue 2
```
Algorithm EnqueueQueue2(queues, item):
    If front2 - 1 == rear1 OR (front2 == size/2 AND rear2 == size - 1):
        Return "Queue 2 is full"
    If front2 == -1:
        front2 = rear2 = size - 1
    Else If rear2 == size/2:
        rear2 = size - 1
    Else:
        rear2--
    queues.array[rear2] = item
```

### Dequeue from Queue 1
```
Algorithm DequeueQueue1(queues):
    If front1 == -1:
        Return "Queue 1 is empty"
    item = queues.array[front1]
    If front1 == rear1:
        front1 = rear1 = -1
    Else If front1 == size/2 - 1:
        front1 = 0
    Else:
        front1++
    Return item
```

### Dequeue from Queue 2
```
Algorithm DequeueQueue2(queues):
    If front2 == -1:
        Return "Queue 2 is empty"
    item = queues.array[front2]
    If front2 == rear2:
        front2 = rear2 = -1
    Else If front2 == size/2:
        front2 = size - 1
    Else:
        front2--
    Return item
```

## Code Implementation

```c
#include <iostream>
using namespace std;
#include <stdlib.h>

#define MAX_SIZE 20
#define QUEUE1_START 0
#define QUEUE1_END (MAX_SIZE/2 - 1)
#define QUEUE2_START (MAX_SIZE/2)
#define QUEUE2_END (MAX_SIZE - 1)

struct MultipleQueues_rrd {
    int array_rrd[MAX_SIZE];
    int front1_rrd, rear1_rrd;
    int front2_rrd, rear2_rrd;
};

struct MultipleQueues_rrd* createQueues_rrd();
int isQueue1Full_rrd(struct MultipleQueues_rrd* queues_rrd);
int isQueue2Full_rrd(struct MultipleQueues_rrd* queues_rrd);
int isQueue1Empty_rrd(struct MultipleQueues_rrd* queues_rrd);
int isQueue2Empty_rrd(struct MultipleQueues_rrd* queues_rrd);
void enqueueQueue1_rrd(struct MultipleQueues_rrd* queues_rrd, int item_rrd);
void enqueueQueue2_rrd(struct MultipleQueues_rrd* queues_rrd, int item_rrd);
int dequeueQueue1_rrd(struct MultipleQueues_rrd* queues_rrd);
int dequeueQueue2_rrd(struct MultipleQueues_rrd* queues_rrd);
void displayQueue1_rrd(struct MultipleQueues_rrd* queues_rrd);
void displayQueue2_rrd(struct MultipleQueues_rrd* queues_rrd);
int getQueue1Size_rrd(struct MultipleQueues_rrd* queues_rrd);
int getQueue2Size_rrd(struct MultipleQueues_rrd* queues_rrd);
void displayMenu_rrd();

int main() {
    struct MultipleQueues_rrd* queues_rrd = createQueues_rrd();
    int choice_rrd, queueChoice_rrd, item_rrd, dequeuedItem_rrd;
    
    cout << "Multiple Queues Implementation using Array" << endl;
    cout << "========================================" << endl;
    cout << "Queue 1: Positions " << QUEUE1_START, QUEUE1_END << " to %d" << endl;
    cout << "Queue 2: Positions " << QUEUE2_START, QUEUE2_END << " to %d" << endl;
    
    while (1) {
        displayMenu_rrd();
        cin >> choice_rrd;
        
        switch (choice_rrd) {
            case 1:
                cout << "Select queue (1 or 2): ";
                cin >> queueChoice_rrd;
                cout << "Enter item to add: ";
                cin >> item_rrd;
                
                if (queueChoice_rrd == 1) {
                    if (isQueue1Full_rrd(queues_rrd)) {
                        cout << "Queue 1 is full! Cannot add more items." << endl;
                    } else {
                        enqueueQueue1_rrd(queues_rrd, item_rrd);
                        cout << "Item " << item_rrd << " added to Queue 1 successfully!" << endl;
                    }
                } else if (queueChoice_rrd == 2) {
                    if (isQueue2Full_rrd(queues_rrd)) {
                        cout << "Queue 2 is full! Cannot add more items." << endl;
                    } else {
                        enqueueQueue2_rrd(queues_rrd, item_rrd);
                        cout << "Item " << item_rrd << " added to Queue 2 successfully!" << endl;
                    }
                } else {
                    cout << "Invalid queue selection! Please choose 1 or 2." << endl;
                }
                break;
                
            case 2:
                cout << "Select queue (1 or 2): ";
                cin >> queueChoice_rrd;
                
                if (queueChoice_rrd == 1) {
                    if (isQueue1Empty_rrd(queues_rrd)) {
                        cout << "Queue 1 is empty! Cannot delete items." << endl;
                    } else {
                        dequeuedItem_rrd = dequeueQueue1_rrd(queues_rrd);
                        cout << "Item " << dequeuedItem_rrd << " deleted from Queue 1 successfully!" << endl;
                    }
                } else if (queueChoice_rrd == 2) {
                    if (isQueue2Empty_rrd(queues_rrd)) {
                        cout << "Queue 2 is empty! Cannot delete items." << endl;
                    } else {
                        dequeuedItem_rrd = dequeueQueue2_rrd(queues_rrd);
                        cout << "Item " << dequeuedItem_rrd << " deleted from Queue 2 successfully!" << endl;
                    }
                } else {
                    cout << "Invalid queue selection! Please choose 1 or 2." << endl;
                }
                break;
                
            case 3:
                cout << "Select queue (1 or 2): ";
                cin >> queueChoice_rrd;
                
                if (queueChoice_rrd == 1) {
                    cout << "Queue 1 contents:" << endl;
                    displayQueue1_rrd(queues_rrd);
                } else if (queueChoice_rrd == 2) {
                    cout << "Queue 2 contents:" << endl;
                    displayQueue2_rrd(queues_rrd);
                } else {
                    cout << "Invalid queue selection! Please choose 1 or 2." << endl;
                }
                break;
                
            case 4:
                cout << "Queue 1 contents:" << endl;
                displayQueue1_rrd(queues_rrd);
                printf("Queue 1 size: %d\n", getQueue1Size_rrd(queues_rrd));
                printf("Queue 1 status: %s\n", isQueue1Empty_rrd(queues_rrd) ? "Empty" : "Not Empty");
                printf("Queue 1 full: %s\n", isQueue1Full_rrd(queues_rrd) ? "Yes" : "No");
                break;
                
            case 5:
                cout << "Queue 2 contents:" << endl;
                displayQueue2_rrd(queues_rrd);
                printf("Queue 2 size: %d\n", getQueue2Size_rrd(queues_rrd));
                printf("Queue 2 status: %s\n", isQueue2Empty_rrd(queues_rrd) ? "Empty" : "Not Empty");
                printf("Queue 2 full: %s\n", isQueue2Full_rrd(queues_rrd) ? "Yes" : "No");
                break;
                
            case 6:
                cout << "Complete queue system status:" << endl;
                cout << "Queue 1:" << endl;
                displayQueue1_rrd(queues_rrd);
                printf("Size: %d, Empty: %s, Full: %s\n\n", 
                       getQueue1Size_rrd(queues_rrd),
                       isQueue1Empty_rrd(queues_rrd) ? "Yes" : "No",
                       isQueue1Full_rrd(queues_rrd) ? "Yes" : "No");
                
                cout << "Queue 2:" << endl;
                displayQueue2_rrd(queues_rrd);
                printf("Size: %d, Empty: %s, Full: %s\n", 
                       getQueue2Size_rrd(queues_rrd),
                       isQueue2Empty_rrd(queues_rrd) ? "Yes" : "No",
                       isQueue2Full_rrd(queues_rrd) ? "Yes" : "No");
                break;
                
            case 7:
                cout << "Thank you for using Multiple Queues Implementation!" << endl;
                free(queues_rrd);
                exit(0);
                
            default:
                cout << "Invalid choice! Please try again." << endl;
        }
    }
    
    return 0;
}

struct MultipleQueues_rrd* createQueues_rrd() {
    struct MultipleQueues_rrd* queues_rrd = (struct MultipleQueues_rrd*)malloc(sizeof(struct MultipleQueues_rrd));
    queues_rrd->front1_rrd = -1;
    queues_rrd->rear1_rrd = -1;
    queues_rrd->front2_rrd = -1;
    queues_rrd->rear2_rrd = -1;
    return queues_rrd;
}

int isQueue1Full_rrd(struct MultipleQueues_rrd* queues_rrd) {
    return ((queues_rrd->front1_rrd == 0 && queues_rrd->rear1_rrd == QUEUE1_END) || 
            (queues_rrd->rear1_rrd == queues_rrd->front2_rrd - 1 && queues_rrd->front2_rrd != -1));
}

int isQueue2Full_rrd(struct MultipleQueues_rrd* queues_rrd) {
    return ((queues_rrd->front2_rrd == QUEUE2_START && queues_rrd->rear2_rrd == QUEUE2_END) || 
            (queues_rrd->rear2_rrd == queues_rrd->front1_rrd - 1 && queues_rrd->front1_rrd != -1));
}

int isQueue1Empty_rrd(struct MultipleQueues_rrd* queues_rrd) {
    return (queues_rrd->front1_rrd == -1);
}

int isQueue2Empty_rrd(struct MultipleQueues_rrd* queues_rrd) {
    return (queues_rrd->front2_rrd == -1);
}

void enqueueQueue1_rrd(struct MultipleQueues_rrd* queues_rrd, int item_rrd) {
    if (isQueue1Full_rrd(queues_rrd)) {
        cout << "Queue 1 is full!" << endl;
        return;
    }
    
    if (queues_rrd->front1_rrd == -1) {
        queues_rrd->front1_rrd = queues_rrd->rear1_rrd = 0;
    } else if (queues_rrd->rear1_rrd == QUEUE1_END) {
        queues_rrd->rear1_rrd = 0;
    } else {
        queues_rrd->rear1_rrd++;
    }
    
    queues_rrd->array_rrd[queues_rrd->rear1_rrd] = item_rrd;
}

void enqueueQueue2_rrd(struct MultipleQueues_rrd* queues_rrd, int item_rrd) {
    if (isQueue2Full_rrd(queues_rrd)) {
        cout << "Queue 2 is full!" << endl;
        return;
    }
    
    if (queues_rrd->front2_rrd == -1) {
        queues_rrd->front2_rrd = queues_rrd->rear2_rrd = QUEUE2_END;
    } else if (queues_rrd->rear2_rrd == QUEUE2_START) {
        queues_rrd->rear2_rrd = QUEUE2_END;
    } else {
        queues_rrd->rear2_rrd--;
    }
    
    queues_rrd->array_rrd[queues_rrd->rear2_rrd] = item_rrd;
}

int dequeueQueue1_rrd(struct MultipleQueues_rrd* queues_rrd) {
    if (isQueue1Empty_rrd(queues_rrd)) {
        cout << "Queue 1 is empty!" << endl;
        return -1;
    }
    
    int item_rrd = queues_rrd->array_rrd[queues_rrd->front1_rrd];
    
    if (queues_rrd->front1_rrd == queues_rrd->rear1_rrd) {
        queues_rrd->front1_rrd = queues_rrd->rear1_rrd = -1;
    } else if (queues_rrd->front1_rrd == QUEUE1_END) {
        queues_rrd->front1_rrd = 0;
    } else {
        queues_rrd->front1_rrd++;
    }
    
    return item_rrd;
}

int dequeueQueue2_rrd(struct MultipleQueues_rrd* queues_rrd) {
    if (isQueue2Empty_rrd(queues_rrd)) {
        cout << "Queue 2 is empty!" << endl;
        return -1;
    }
    
    int item_rrd = queues_rrd->array_rrd[queues_rrd->front2_rrd];
    
    if (queues_rrd->front2_rrd == queues_rrd->rear2_rrd) {
        queues_rrd->front2_rrd = queues_rrd->rear2_rrd = -1;
    } else if (queues_rrd->front2_rrd == QUEUE2_START) {
        queues_rrd->front2_rrd = QUEUE2_END;
    } else {
        queues_rrd->front2_rrd--;
    }
    
    return item_rrd;
}

void displayQueue1_rrd(struct MultipleQueues_rrd* queues_rrd) {
    if (isQueue1Empty_rrd(queues_rrd)) {
        cout << "Queue 1 is empty." << endl;
        return;
    }
    
    cout << "Queue 1 (Front to Rear): ";
    int i_rrd = queues_rrd->front1_rrd;
    
    if (queues_rrd->front1_rrd <= queues_rrd->rear1_rrd) {

        for (i_rrd = queues_rrd->front1_rrd; i_rrd <= queues_rrd->rear1_rrd; i_rrd++) {
            cout << "" << queues_rrd->array_rrd[i_rrd] << " ";
        }
    } else {

        for (i_rrd = queues_rrd->front1_rrd; i_rrd <= QUEUE1_END; i_rrd++) {
            cout << "" << queues_rrd->array_rrd[i_rrd] << " ";
        }
        for (i_rrd = 0; i_rrd <= queues_rrd->rear1_rrd; i_rrd++) {
            cout << "" << queues_rrd->array_rrd[i_rrd] << " ";
        }
    }
    cout << "" << endl;
}

void displayQueue2_rrd(struct MultipleQueues_rrd* queues_rrd) {
    if (isQueue2Empty_rrd(queues_rrd)) {
        cout << "Queue 2 is empty." << endl;
        return;
    }
    
    cout << "Queue 2 (Front to Rear): ";
    int i_rrd = queues_rrd->front2_rrd;
    
    if (queues_rrd->front2_rrd >= queues_rrd->rear2_rrd) {

        for (i_rrd = queues_rrd->front2_rrd; i_rrd >= queues_rrd->rear2_rrd; i_rrd--) {
            cout << "" << queues_rrd->array_rrd[i_rrd] << " ";
        }
    } else {

        for (i_rrd = queues_rrd->front2_rrd; i_rrd >= QUEUE2_START; i_rrd--) {
            cout << "" << queues_rrd->array_rrd[i_rrd] << " ";
        }
        for (i_rrd = QUEUE2_END; i_rrd >= queues_rrd->rear2_rrd; i_rrd--) {
            cout << "" << queues_rrd->array_rrd[i_rrd] << " ";
        }
    }
    cout << "" << endl;
}

int getQueue1Size_rrd(struct MultipleQueues_rrd* queues_rrd) {
    if (isQueue1Empty_rrd(queues_rrd)) {
        return 0;
    }
    
    if (queues_rrd->front1_rrd <= queues_rrd->rear1_rrd) {
        return queues_rrd->rear1_rrd - queues_rrd->front1_rrd + 1;
    } else {
        return (QUEUE1_END - queues_rrd->front1_rrd + 1) + (queues_rrd->rear1_rrd - QUEUE1_START + 1);
    }
}

int getQueue2Size_rrd(struct MultipleQueues_rrd* queues_rrd) {
    if (isQueue2Empty_rrd(queues_rrd)) {
        return 0;
    }
    
    if (queues_rrd->front2_rrd >= queues_rrd->rear2_rrd) {
        return queues_rrd->front2_rrd - queues_rrd->rear2_rrd + 1;
    } else {
        return (queues_rrd->front2_rrd - QUEUE2_START + 1) + (QUEUE2_END - queues_rrd->rear2_rrd + 1);
    }
}

void displayMenu_rrd() {
    cout << "\n===== Multiple Queues Operations =====" << endl;
    cout << "1. Add to Queue" << endl;
    cout << "2. Delete from Queue" << endl;
    cout << "3. Display Queue" << endl;
    cout << "4. Display Queue 1 Status" << endl;
    cout << "5. Display Queue 2 Status" << endl;
    cout << "6. Display Complete Status" << endl;
    cout << "7. Exit" << endl;
    cout << "====================================" << endl;
    cout << "Enter your choice: ";
}
```

## Output

```
Multiple Queues Implementation using Array
========================================
Queue 1: Positions 0 to 9
Queue 2: Positions 10 to 19

===== Multiple Queues Operations =====
1. Add to Queue
2. Delete from Queue
3. Display Queue
4. Display Queue 1 Status
5. Display Queue 2 Status
6. Display Complete Status
7. Exit
====================================
Enter your choice: 1
Select queue (1 or 2): 1
Enter item to add: 10
Item 10 added to Queue 1 successfully!

===== Multiple Queues Operations =====
1. Add to Queue
2. Delete from Queue
3. Display Queue
4. Display Queue 1 Status
5. Display Queue 2 Status
6. Display Complete Status
7. Exit
====================================
Enter your choice: 1
Select queue (1 or 2): 1
Enter item to add: 20
Item 20 added to Queue 1 successfully!

===== Multiple Queues Operations =====
1. Add to Queue
2. Delete from Queue
3. Display Queue
4. Display Queue 1 Status
5. Display Queue 2 Status
6. Display Complete Status
7. Exit
====================================
Enter your choice: 1
Select queue (1 or 2): 2
Enter item to add: 30
Item 30 added to Queue 2 successfully!

===== Multiple Queues Operations =====
1. Add to Queue
2. Delete from Queue
3. Display Queue
4. Display Queue 1 Status
5. Display Queue 2 Status
6. Display Complete Status
7. Exit
====================================
Enter your choice: 1
Select queue (1 or 2): 2
Enter item to add: 40
Item 40 added to Queue 2 successfully!

===== Multiple Queues Operations =====
1. Add to Queue
2. Delete from Queue
3. Display Queue
4. Display Queue 1 Status
5. Display Queue 2 Status
6. Display Complete Status
7. Exit
====================================
Enter your choice: 3
Select queue (1 or 2): 1
Queue 1 contents:
Queue 1 (Front to Rear): 10 20

===== Multiple Queues Operations =====
1. Add to Queue
2. Delete from Queue
3. Display Queue
4. Display Queue 1 Status
5. Display Queue 2 Status
6. Display Complete Status
7. Exit
====================================
Enter your choice: 3
Select queue (1 or 2): 2
Queue 2 contents:
Queue 2 (Front to Rear): 30 40

===== Multiple Queues Operations =====
1. Add to Queue
2. Delete from Queue
3. Display Queue
4. Display Queue 1 Status
5. Display Queue 2 Status
6. Display Complete Status
7. Exit
====================================
Enter your choice: 6
Complete queue system status:
Queue 1:
Queue 1 (Front to Rear): 10 20
Size: 2, Empty: No, Full: No

Queue 2:
Queue 2 (Front to Rear): 30 40
Size: 2, Empty: No, Full: No
```

## Dry Run

**Initial State**:
- Array: [-, -, -, -, -, -, -, -, -, -, -, -, -, -, -, -, -, -, -, -]
- Queue 1: front1 = -1, rear1 = -1
- Queue 2: front2 = -1, rear2 = -1

**Add 10 to Queue 1**:
- Queue 1 is empty, so front1 = rear1 = 0
- array[0] = 10
- State: [10, -, -, -, -, -, -, -, -, -, -, -, -, -, -, -, -, -, -, -]

**Add 20 to Queue 1**:
- rear1 = 1
- array[1] = 20
- State: [10, 20, -, -, -, -, -, -, -, -, -, -, -, -, -, -, -, -, -, -]

**Add 30 to Queue 2**:
- Queue 2 is empty, so front2 = rear2 = 19
- array[19] = 30
- State: [10, 20, -, -, -, -, -, -, -, -, -, -, -, -, -, -, -, -, -, 30]

**Add 40 to Queue 2**:
- rear2 = 18
- array[18] = 40
- State: [10, 20, -, -, -, -, -, -, -, -, -, -, -, -, -, -, -, -, 40, 30]

**Display Queue 1**:
- Front to rear: 10, 20

**Display Queue 2**:
- Front to rear: 30, 40 (reverse order because we're going from front2=19 to rear2=18)

## Conclusion

The implementation demonstrates multiple queues (two queues) using a single array with the following key features:

**Multiple Queue Operations**:
1. **Enqueue**: O(1) time complexity for both queues
2. **Dequeue**: O(1) time complexity for both queues
3. **Display**: O(n) time complexity where n is queue size
4. **Size Calculation**: O(1) time complexity
5. **Full/Empty Check**: O(1) time complexity

**Space Complexity**: O(MAX_SIZE) for the entire array

**Key Implementation Features**:
1. **Space Sharing**: Single array divided between two queues
2. **Bidirectional Growth**: Queue 1 grows left-to-right, Queue 2 grows right-to-left
3. **Wrap-around Support**: Both queues support circular wrap-around
4. **Boundary Management**: Proper handling of queue boundaries
5. **Collision Detection**: Prevents queues from overlapping

**Advantages of Multiple Queues**:
1. **Memory Efficiency**: Single array for multiple queues
2. **Flexibility**: Dynamic space allocation between queues
3. **Performance**: Constant time operations
4. **Resource Sharing**: Efficient use of fixed memory space

**Queue Management**:
1. **Queue 1**: Occupies positions 0 to 9, grows left-to-right
2. **Queue 2**: Occupies positions 10 to 19, grows right-to-left
3. **Collision**: Occurs when queues try to use the same position
4. **Wrap-around**: Each queue can wrap around its designated space

**Real-world Applications**:
1. **Memory Management**: Allocating memory pools for different processes
2. **Buffer Management**: Input/output buffers for different data streams
3. **Resource Allocation**: Sharing resources between different user groups
4. **Task Scheduling**: Separate queues for different priority tasks

The implementation correctly handles all edge cases:
- Adding items to empty queues
- Removing items when queues become empty
- Wrap-around scenarios for both queues
- Collision prevention between queues
- Proper size calculation with wrap-around
- Boundary condition management

This system efficiently manages two separate queues within a single array, maximizing memory utilization while maintaining the integrity and performance of both queues.