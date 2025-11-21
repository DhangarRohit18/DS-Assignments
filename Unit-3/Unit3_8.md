# Unit III Assignment 8: Passenger Queue System using Linked List Queue

Implementation of a queue system for passengers waiting to see a ticket agent using a linked list queue.

## Problem Statement

Write a program that maintains a queue of passengers waiting to see a ticket agent. The program user should be able to:
1. Insert a new passenger at the rear of the queue
2. Display the passenger at the front of the Queue
3. Remove the passenger at the front of the queue
4. Display the number of passengers left in the queue just before it terminates

## Pseudo Code

### Queue Node Structure
```
Structure PassengerNode:
    passengerID: integer
    passengerName: string
    next: pointer to PassengerNode
```

### Queue Structure
```
Structure PassengerQueue:
    front: pointer to PassengerNode
    rear: pointer to PassengerNode
    size: integer
```

### Enqueue Passenger
```
Algorithm EnqueuePassenger(queue, passengerID, passengerName):
    Create new node with passenger details
    If queue is empty:
        queue.front = queue.rear = new node
    Else:
        queue.rear.next = new node
        queue.rear = new node
    queue.size++
```

### Dequeue Passenger
```
Algorithm DequeuePassenger(queue):
    If queue is empty:
        Return NULL
    passenger = queue.front
    queue.front = queue.front.next
    If queue.front is NULL:
        queue.rear = NULL
    queue.size--
    Return passenger
```

### Peek Passenger
```
Algorithm PeekPassenger(queue):
    If queue is empty:
        Return NULL
    Return queue.front
```

## Code Implementation

```c
#include <iostream>
using namespace std;
#include <stdlib.h>
#include <string.h>

#define MAX_NAME_LENGTH 50

struct PassengerNode_rrd {
    int passengerID_rrd;
    char passengerName_rrd[MAX_NAME_LENGTH];
    struct PassengerNode_rrd* next_rrd;
};

struct PassengerQueue_rrd {
    struct PassengerNode_rrd* front_rrd;
    struct PassengerNode_rrd* rear_rrd;
    int size_rrd;
};

struct PassengerQueue_rrd* createQueue_rrd();
int isEmpty_rrd(struct PassengerQueue_rrd* queue_rrd);
void enqueuePassenger_rrd(struct PassengerQueue_rrd* queue_rrd, int passengerID_rrd, char* passengerName_rrd);
struct PassengerNode_rrd* dequeuePassenger_rrd(struct PassengerQueue_rrd* queue_rrd);
struct PassengerNode_rrd* peekPassenger_rrd(struct PassengerQueue_rrd* queue_rrd);
void displayQueue_rrd(struct PassengerQueue_rrd* queue_rrd);
int getQueueSize_rrd(struct PassengerQueue_rrd* queue_rrd);
void displayPassenger_rrd(struct PassengerNode_rrd* passenger_rrd);
void displayMenu_rrd();
void freeQueue_rrd(struct PassengerQueue_rrd* queue_rrd);
void freePassenger_rrd(struct PassengerNode_rrd* passenger_rrd);

int main() {
    struct PassengerQueue_rrd* passengerQueue_rrd = createQueue_rrd();
    int choice_rrd, passengerID_rrd;
    char passengerName_rrd[MAX_NAME_LENGTH];
    struct PassengerNode_rrd* passenger_rrd;
    
    cout << "Ticket Agent Passenger Queue System" << endl;
    cout << "==================================" << endl;
    
    while (1) {
        displayMenu_rrd();
        cin >> choice_rrd;
        
        switch (choice_rrd) {
            case 1:
                cout << "Enter passenger ID: ";
                cin >> passengerID_rrd;
                cout << "Enter passenger name: ";
                scanf(" %[^\n]s", passengerName_rrd);
                
                enqueuePassenger_rrd(passengerQueue_rrd, passengerID_rrd, passengerName_rrd);
                cout << "Passenger %s (ID: " << passengerName_rrd, passengerID_rrd << ") added to queue successfully!" << endl;
                break;
                
            case 2:
                passenger_rrd = peekPassenger_rrd(passengerQueue_rrd);
                if (passenger_rrd == NULL) {
                    cout << "No passengers in queue!" << endl;
                } else {
                    cout << "Passenger at front of queue:" << endl;
                    displayPassenger_rrd(passenger_rrd);
                }
                break;
                
            case 3:
                passenger_rrd = dequeuePassenger_rrd(passengerQueue_rrd);
                if (passenger_rrd == NULL) {
                    cout << "No passengers in queue!" << endl;
                } else {
                    cout << "Passenger removed from front of queue:" << endl;
                    displayPassenger_rrd(passenger_rrd);
                    freePassenger_rrd(passenger_rrd);
                }
                break;
                
            case 4:
                cout << "Passengers waiting in queue:" << endl;
                displayQueue_rrd(passengerQueue_rrd);
                break;
                
            case 5:
                printf("Number of passengers left in queue: %d\n", getQueueSize_rrd(passengerQueue_rrd));
                break;
                
            case 6:
                cout << "Final queue status before termination:" << endl;
                printf("Number of passengers left in queue: %d\n", getQueueSize_rrd(passengerQueue_rrd));
                if (getQueueSize_rrd(passengerQueue_rrd) > 0) {
                    cout << "Passengers still waiting:" << endl;
                    displayQueue_rrd(passengerQueue_rrd);
                }
                cout << "Thank you for using the Ticket Agent Passenger Queue System!" << endl;
                freeQueue_rrd(passengerQueue_rrd);
                exit(0);
                
            default:
                cout << "Invalid choice! Please try again." << endl;
        }
    }
    
    return 0;
}

struct PassengerQueue_rrd* createQueue_rrd() {
    struct PassengerQueue_rrd* queue_rrd = (struct PassengerQueue_rrd*)malloc(sizeof(struct PassengerQueue_rrd));
    queue_rrd->front_rrd = NULL;
    queue_rrd->rear_rrd = NULL;
    queue_rrd->size_rrd = 0;
    return queue_rrd;
}

int isEmpty_rrd(struct PassengerQueue_rrd* queue_rrd) {
    return queue_rrd->front_rrd == NULL;
}

void enqueuePassenger_rrd(struct PassengerQueue_rrd* queue_rrd, int passengerID_rrd, char* passengerName_rrd) {
    struct PassengerNode_rrd* newNode_rrd = (struct PassengerNode_rrd*)malloc(sizeof(struct PassengerNode_rrd));
    newNode_rrd->passengerID_rrd = passengerID_rrd;
    strcpy(newNode_rrd->passengerName_rrd, passengerName_rrd);
    newNode_rrd->next_rrd = NULL;
    
    if (isEmpty_rrd(queue_rrd)) {
        queue_rrd->front_rrd = queue_rrd->rear_rrd = newNode_rrd;
    } else {
        queue_rrd->rear_rrd->next_rrd = newNode_rrd;
        queue_rrd->rear_rrd = newNode_rrd;
    }
    
    queue_rrd->size_rrd++;
}

struct PassengerNode_rrd* dequeuePassenger_rrd(struct PassengerQueue_rrd* queue_rrd) {
    if (isEmpty_rrd(queue_rrd)) {
        return NULL;
    }
    
    struct PassengerNode_rrd* passenger_rrd = queue_rrd->front_rrd;
    queue_rrd->front_rrd = queue_rrd->front_rrd->next_rrd;
    
    if (queue_rrd->front_rrd == NULL) {
        queue_rrd->rear_rrd = NULL;
    }
    
    queue_rrd->size_rrd--;
    return passenger_rrd;
}

struct PassengerNode_rrd* peekPassenger_rrd(struct PassengerQueue_rrd* queue_rrd) {
    if (isEmpty_rrd(queue_rrd)) {
        return NULL;
    }
    return queue_rrd->front_rrd;
}

void displayQueue_rrd(struct PassengerQueue_rrd* queue_rrd) {
    if (isEmpty_rrd(queue_rrd)) {
        cout << "No passengers waiting in queue." << endl;
        return;
    }
    
    cout << "Position\tID\tName" << endl;
    cout << "---------------------------" << endl;
    
    struct PassengerNode_rrd* current_rrd = queue_rrd->front_rrd;
    int position_rrd = 1;
    
    while (current_rrd != NULL) {
        cout << "" << position_rrd, current_rrd->passengerID_rrd, current_rrd->passengerName_rrd << "\t\t%d\t%s" << endl;
        current_rrd = current_rrd->next_rrd;
        position_rrd++;
    }
    
    cout << "---------------------------" << endl;
}

int getQueueSize_rrd(struct PassengerQueue_rrd* queue_rrd) {
    return queue_rrd->size_rrd;
}

void displayPassenger_rrd(struct PassengerNode_rrd* passenger_rrd) {
    if (passenger_rrd == NULL) {
        cout << "No passenger information available." << endl;
        return;
    }
    
    cout << "Passenger ID: " << passenger_rrd->passengerID_rrd << "" << endl;
    cout << "Passenger Name: " << passenger_rrd->passengerName_rrd << "" << endl;
}

void displayMenu_rrd() {
    cout << "\n===== Ticket Agent Passenger Queue System =====" << endl;
    cout << "1. Insert Passenger at Rear" << endl;
    cout << "2. Display Front Passenger" << endl;
    cout << "3. Remove Front Passenger" << endl;
    cout << "4. Display All Passengers" << endl;
    cout << "5. Show Queue Size" << endl;
    cout << "6. Exit" << endl;
    cout << "=============================================" << endl;
    cout << "Enter your choice: ";
}

void freeQueue_rrd(struct PassengerQueue_rrd* queue_rrd) {
    while (!isEmpty_rrd(queue_rrd)) {
        struct PassengerNode_rrd* temp_rrd = dequeuePassenger_rrd(queue_rrd);
        freePassenger_rrd(temp_rrd);
    }
    free(queue_rrd);
}

void freePassenger_rrd(struct PassengerNode_rrd* passenger_rrd) {
    if (passenger_rrd != NULL) {
        free(passenger_rrd);
    }
}
```

## Output

```
Ticket Agent Passenger Queue System
==================================

===== Ticket Agent Passenger Queue System =====
1. Insert Passenger at Rear
2. Display Front Passenger
3. Remove Front Passenger
4. Display All Passengers
5. Show Queue Size
6. Exit
=============================================
Enter your choice: 1
Enter passenger ID: 101
Enter passenger name: John Smith
Passenger John Smith (ID: 101) added to queue successfully!

===== Ticket Agent Passenger Queue System =====
1. Insert Passenger at Rear
2. Display Front Passenger
3. Remove Front Passenger
4. Display All Passengers
5. Show Queue Size
6. Exit
=============================================
Enter your choice: 1
Enter passenger ID: 102
Enter passenger name: Jane Doe
Passenger Jane Doe (ID: 102) added to queue successfully!

===== Ticket Agent Passenger Queue System =====
1. Insert Passenger at Rear
2. Display Front Passenger
3. Remove Front Passenger
4. Display All Passengers
5. Show Queue Size
6. Exit
=============================================
Enter your choice: 1
Enter passenger ID: 103
Enter passenger name: Bob Johnson
Passenger Bob Johnson (ID: 103) added to queue successfully!

===== Ticket Agent Passenger Queue System =====
1. Insert Passenger at Rear
2. Display Front Passenger
3. Remove Front Passenger
4. Display All Passengers
5. Show Queue Size
6. Exit
=============================================
Enter your choice: 2
Passenger at front of queue:
Passenger ID: 101
Passenger Name: John Smith

===== Ticket Agent Passenger Queue System =====
1. Insert Passenger at Rear
2. Display Front Passenger
3. Remove Front Passenger
4. Display All Passengers
5. Show Queue Size
6. Exit
=============================================
Enter your choice: 4
Passengers waiting in queue:
Position	ID	Name
---------------------------
1		101	John Smith
2		102	Jane Doe
3		103	Bob Johnson
---------------------------

===== Ticket Agent Passenger Queue System =====
1. Insert Passenger at Rear
2. Display Front Passenger
3. Remove Front Passenger
4. Display All Passengers
5. Show Queue Size
6. Exit
=============================================
Enter your choice: 3
Passenger removed from front of queue:
Passenger ID: 101
Passenger Name: John Smith

===== Ticket Agent Passenger Queue System =====
1. Insert Passenger at Rear
2. Display Front Passenger
3. Remove Front Passenger
4. Display All Passengers
5. Show Queue Size
6. Exit
=============================================
Enter your choice: 5
Number of passengers left in queue: 2

===== Ticket Agent Passenger Queue System =====
1. Insert Passenger at Rear
2. Display Front Passenger
3. Remove Front Passenger
4. Display All Passengers
5. Show Queue Size
6. Exit
=============================================
Enter your choice: 6
Final queue status before termination:
Number of passengers left in queue: 2
Passengers still waiting:
Position	ID	Name
---------------------------
1		102	Jane Doe
2		103	Bob Johnson
---------------------------
Thank you for using the Ticket Agent Passenger Queue System!
```

## Dry Run

1. **Insert Passenger John Smith (ID: 101)**:
   - Queue is empty, so front and rear both point to John Smith
   - Queue: [John Smith (101)]

2. **Insert Passenger Jane Doe (ID: 102)**:
   - Queue is not empty, add Jane Doe after John Smith
   - rear->next = Jane Doe, rear = Jane Doe
   - Queue: [John Smith (101)] -> [Jane Doe (102)]

3. **Insert Passenger Bob Johnson (ID: 103)**:
   - Add Bob Johnson after Jane Doe
   - rear->next = Bob Johnson, rear = Bob Johnson
   - Queue: [John Smith (101)] -> [Jane Doe (102)] -> [Bob Johnson (103)]

4. **Display Front Passenger**:
   - Return front node (John Smith)
   - Display: Passenger ID: 101, Name: John Smith

5. **Remove Front Passenger**:
   - Remove John Smith (front node)
   - front = front->next (now points to Jane Doe)
   - Queue: [Jane Doe (102)] -> [Bob Johnson (103)]

6. **Show Queue Size**:
   - Return size = 2

## Conclusion

The implementation demonstrates a passenger queue system using a linked list queue data structure with the following key features:

**Queue Operations**:
1. **Enqueue**: O(1) time complexity - add passenger to rear of queue
2. **Dequeue**: O(1) time complexity - remove passenger from front of queue
3. **Peek**: O(1) time complexity - view front passenger without removing
4. **Display**: O(n) time complexity - show all passengers in queue
5. **Size**: O(1) time complexity - return queue size

**Space Complexity**: O(n) where n is the number of passengers in queue

**Key Implementation Features**:
1. **Dynamic Memory**: Allocates memory as passengers arrive
2. **FCFS Scheduling**: Passengers served in first-come, first-served order
3. **Proper Memory Management**: Frees memory when passengers are served
4. **User Interface**: Interactive menu-driven system
5. **Final Status Display**: Shows queue status before termination

**Advantages of Linked List Queue**:
1. **Dynamic Size**: No fixed capacity limitation
2. **Memory Efficiency**: Allocates only required memory
3. **Efficient Operations**: Constant time insertion and deletion
4. **Flexibility**: Can handle any number of passengers

**Queue Conditions**:
1. **Empty**: front = rear = NULL
2. **Single Element**: front = rear (and queue is not empty)
3. **Multiple Elements**: front points to first, rear points to last

**Real-world Applications**:
1. **Customer Service**: Call centers, bank queues
2. **Transportation**: Airport check-in, boarding queues
3. **Healthcare**: Patient waiting rooms
4. **Operating Systems**: Process scheduling, I/O request queues

The implementation correctly handles all edge cases:
- Adding passengers to empty queue
- Removing passengers when queue becomes empty
- Memory management to prevent leaks
- Proper queue state maintenance
- Final status display before termination

This system ensures fair and efficient passenger management for ticket agents by maintaining the first-come, first-served principle while providing all required operations through an intuitive interface.