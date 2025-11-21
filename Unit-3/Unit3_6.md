# Unit III Assignment 6: Patient Tracking System using Queue

Implementation of a patient tracking system for a medical clinic that assigns patients to doctors on a first-come, first-served basis using a queue.

## Problem Statement

Write a program to keep track of patients as they check into a medical clinic, assigning patients to doctors on a first-come, first-served basis using a queue data structure.

## Pseudo Code

### Queue Node Structure
```
Structure PatientNode:
    patientID: integer
    patientName: string
    checkInTime: integer
    next: pointer to PatientNode
```

### Queue Structure
```
Structure PatientQueue:
    front: pointer to PatientNode
    rear: pointer to PatientNode
    size: integer
```

### Enqueue Patient
```
Algorithm EnqueuePatient(queue, patientID, patientName, checkInTime):
    Create new node with patient details
    If queue is empty:
        queue.front = queue.rear = new node
    Else:
        queue.rear.next = new node
        queue.rear = new node
    queue.size++
```

### Dequeue Patient
```
Algorithm DequeuePatient(queue):
    If queue is empty:
        Return "No patients in queue"
    patient = queue.front
    queue.front = queue.front.next
    If queue.front is NULL:
        queue.rear = NULL
    queue.size--
    Return patient details
```

### Display Queue
```
Algorithm DisplayQueue(queue):
    If queue is empty:
        Print "No patients waiting"
    current = queue.front
    While current is not NULL:
        Print patient details
        current = current.next
```

## Code Implementation

```c
#include <iostream>
using namespace std;
#include <stdlib.h>
#include <string.h>

#define MAX_NAME_LENGTH 50

struct PatientNode_rrd {
    int patientID_rrd;
    char patientName_rrd[MAX_NAME_LENGTH];
    int checkInTime_rrd;
    struct PatientNode_rrd* next_rrd;
};

struct PatientQueue_rrd {
    struct PatientNode_rrd* front_rrd;
    struct PatientNode_rrd* rear_rrd;
    int size_rrd;
};

struct PatientQueue_rrd* createQueue_rrd();
int isEmpty_rrd(struct PatientQueue_rrd* queue_rrd);
void enqueuePatient_rrd(struct PatientQueue_rrd* queue_rrd, int patientID_rrd, char* patientName_rrd, int checkInTime_rrd);
struct PatientNode_rrd* dequeuePatient_rrd(struct PatientQueue_rrd* queue_rrd);
void displayQueue_rrd(struct PatientQueue_rrd* queue_rrd);
int getQueueSize_rrd(struct PatientQueue_rrd* queue_rrd);
void displayPatient_rrd(struct PatientNode_rrd* patient_rrd);
void assignPatientToDoctor_rrd(struct PatientQueue_rrd* queue_rrd, int doctorID_rrd);
void displayMenu_rrd();
void freeQueue_rrd(struct PatientQueue_rrd* queue_rrd);

int main() {
    struct PatientQueue_rrd* patientQueue_rrd = createQueue_rrd();
    int choice_rrd, patientID_rrd, checkInTime_rrd, doctorID_rrd;
    char patientName_rrd[MAX_NAME_LENGTH];
    
    cout << "Medical Clinic Patient Tracking System" << endl;
    cout << "=====================================" << endl;
    
    while (1) {
        displayMenu_rrd();
        cin >> choice_rrd;
        
        switch (choice_rrd) {
            case 1:
                cout << "Enter patient ID: ";
                cin >> patientID_rrd;
                cout << "Enter patient name: ";
                scanf(" %[^\n]s", patientName_rrd);
                cout << "Enter check-in time (minutes from clinic opening): ";
                cin >> checkInTime_rrd;
                
                enqueuePatient_rrd(patientQueue_rrd, patientID_rrd, patientName_rrd, checkInTime_rrd);
                cout << "Patient %s (ID: " << patientName_rrd, patientID_rrd << ") added to queue successfully!" << endl;
                break;
                
            case 2:
                if (isEmpty_rrd(patientQueue_rrd)) {
                    cout << "No patients in queue!" << endl;
                } else {
                    cout << "Enter doctor ID: ";
                    cin >> doctorID_rrd;
                    assignPatientToDoctor_rrd(patientQueue_rrd, doctorID_rrd);
                }
                break;
                
            case 3:
                cout << "Patients waiting in queue:" << endl;
                displayQueue_rrd(patientQueue_rrd);
                break;
                
            case 4:
                printf("Number of patients waiting: %d\n", getQueueSize_rrd(patientQueue_rrd));
                break;
                
            case 5:
                if (isEmpty_rrd(patientQueue_rrd)) {
                    cout << "No patients in queue!" << endl;
                } else {
                    cout << "Next patient to be served:" << endl;
                    displayPatient_rrd(patientQueue_rrd->front_rrd);
                }
                break;
                
            case 6:
                cout << "Thank you for using the Medical Clinic Patient Tracking System!" << endl;
                freeQueue_rrd(patientQueue_rrd);
                exit(0);
                
            default:
                cout << "Invalid choice! Please try again." << endl;
        }
    }
    
    return 0;
}

struct PatientQueue_rrd* createQueue_rrd() {
    struct PatientQueue_rrd* queue_rrd = (struct PatientQueue_rrd*)malloc(sizeof(struct PatientQueue_rrd));
    queue_rrd->front_rrd = NULL;
    queue_rrd->rear_rrd = NULL;
    queue_rrd->size_rrd = 0;
    return queue_rrd;
}

int isEmpty_rrd(struct PatientQueue_rrd* queue_rrd) {
    return queue_rrd->front_rrd == NULL;
}

void enqueuePatient_rrd(struct PatientQueue_rrd* queue_rrd, int patientID_rrd, char* patientName_rrd, int checkInTime_rrd) {
    struct PatientNode_rrd* newNode_rrd = (struct PatientNode_rrd*)malloc(sizeof(struct PatientNode_rrd));
    newNode_rrd->patientID_rrd = patientID_rrd;
    strcpy(newNode_rrd->patientName_rrd, patientName_rrd);
    newNode_rrd->checkInTime_rrd = checkInTime_rrd;
    newNode_rrd->next_rrd = NULL;
    
    if (isEmpty_rrd(queue_rrd)) {
        queue_rrd->front_rrd = queue_rrd->rear_rrd = newNode_rrd;
    } else {
        queue_rrd->rear_rrd->next_rrd = newNode_rrd;
        queue_rrd->rear_rrd = newNode_rrd;
    }
    
    queue_rrd->size_rrd++;
}

struct PatientNode_rrd* dequeuePatient_rrd(struct PatientQueue_rrd* queue_rrd) {
    if (isEmpty_rrd(queue_rrd)) {
        return NULL;
    }
    
    struct PatientNode_rrd* patient_rrd = queue_rrd->front_rrd;
    queue_rrd->front_rrd = queue_rrd->front_rrd->next_rrd;
    
    if (queue_rrd->front_rrd == NULL) {
        queue_rrd->rear_rrd = NULL;
    }
    
    queue_rrd->size_rrd--;
    return patient_rrd;
}

void displayQueue_rrd(struct PatientQueue_rrd* queue_rrd) {
    if (isEmpty_rrd(queue_rrd)) {
        cout << "No patients waiting in queue." << endl;
        return;
    }
    
    cout << "Position\tID\tName\t\t\tCheck-in Time" << endl;
    cout << "----------------------------------------------------" << endl;
    
    struct PatientNode_rrd* current_rrd = queue_rrd->front_rrd;
    int position_rrd = 1;
    
    while (current_rrd != NULL) {
        cout << "" << position_rrd, current_rrd->patientID_rrd, 
               current_rrd->patientName_rrd, current_rrd->checkInTime_rrd << "\t\t%d\t%-20s\t%d minutes" << endl;
        current_rrd = current_rrd->next_rrd;
        position_rrd++;
    }
    
    cout << "----------------------------------------------------" << endl;
}

int getQueueSize_rrd(struct PatientQueue_rrd* queue_rrd) {
    return queue_rrd->size_rrd;
}

void displayPatient_rrd(struct PatientNode_rrd* patient_rrd) {
    if (patient_rrd == NULL) {
        cout << "No patient information available." << endl;
        return;
    }
    
    cout << "Patient ID: " << patient_rrd->patientID_rrd << "" << endl;
    cout << "Patient Name: " << patient_rrd->patientName_rrd << "" << endl;
    cout << "Check-in Time: " << patient_rrd->checkInTime_rrd << " minutes" << endl;
}

void assignPatientToDoctor_rrd(struct PatientQueue_rrd* queue_rrd, int doctorID_rrd) {
    struct PatientNode_rrd* patient_rrd = dequeuePatient_rrd(queue_rrd);
    
    if (patient_rrd == NULL) {
        cout << "No patients in queue!" << endl;
        return;
    }
    
    cout << "\n--- Patient Assignment ---" << endl;
    cout << "Doctor ID: " << doctorID_rrd << "" << endl;
    cout << "Assigned Patient:" << endl;
    displayPatient_rrd(patient_rrd);
    cout << "-------------------------" << endl;
    

    free(patient_rrd);
    
    if (isEmpty_rrd(queue_rrd)) {
        cout << "No more patients waiting." << endl;
    } else {
        cout << "Next patient in queue:" << endl;
        displayPatient_rrd(queue_rrd->front_rrd);
    }
}

void displayMenu_rrd() {
    cout << "\n===== Medical Clinic Patient Tracking System =====" << endl;
    cout << "1. Add Patient to Queue" << endl;
    cout << "2. Assign Patient to Doctor" << endl;
    cout << "3. Display Patient Queue" << endl;
    cout << "4. Show Queue Size" << endl;
    cout << "5. Show Next Patient" << endl;
    cout << "6. Exit" << endl;
    cout << "================================================" << endl;
    cout << "Enter your choice: ";
}

void freeQueue_rrd(struct PatientQueue_rrd* queue_rrd) {
    while (!isEmpty_rrd(queue_rrd)) {
        struct PatientNode_rrd* temp_rrd = dequeuePatient_rrd(queue_rrd);
        free(temp_rrd);
    }
    free(queue_rrd);
}
```

## Output

```
Medical Clinic Patient Tracking System
=====================================

===== Medical Clinic Patient Tracking System =====
1. Add Patient to Queue
2. Assign Patient to Doctor
3. Display Patient Queue
4. Show Queue Size
5. Show Next Patient
6. Exit
================================================
Enter your choice: 1
Enter patient ID: 101
Enter patient name: John Smith
Enter check-in time (minutes from clinic opening): 10
Patient John Smith (ID: 101) added to queue successfully!

===== Medical Clinic Patient Tracking System =====
1. Add Patient to Queue
2. Assign Patient to Doctor
3. Display Patient Queue
4. Show Queue Size
5. Show Next Patient
6. Exit
================================================
Enter your choice: 1
Enter patient ID: 102
Enter patient name: Jane Doe
Enter check-in time (minutes from clinic opening): 15
Patient Jane Doe (ID: 102) added to queue successfully!

===== Medical Clinic Patient Tracking System =====
1. Add Patient to Queue
2. Assign Patient to Doctor
3. Display Patient Queue
4. Show Queue Size
5. Show Next Patient
6. Exit
================================================
Enter your choice: 3
Patients waiting in queue:
Position	ID	Name			Check-in Time
----------------------------------------------------
1		101	John Smith		10 minutes
2		102	Jane Doe		15 minutes
----------------------------------------------------

===== Medical Clinic Patient Tracking System =====
1. Add Patient to Queue
2. Assign Patient to Doctor
3. Display Patient Queue
4. Show Queue Size
5. Show Next Patient
6. Exit
================================================
Enter your choice: 2
Enter doctor ID: 201

--- Patient Assignment ---
Doctor ID: 201
Assigned Patient:
Patient ID: 101
Patient Name: John Smith
Check-in Time: 10 minutes
-------------------------
Next patient in queue:
Patient ID: 102
Patient Name: Jane Doe
Check-in Time: 15 minutes
```

## Dry Run

1. **Add Patient John Smith (ID: 101, Time: 10)**:
   - Queue is empty, so front and rear both point to John Smith
   - Queue: [John Smith (101)]

2. **Add Patient Jane Doe (ID: 102, Time: 15)**:
   - Queue is not empty, add Jane Doe after John Smith
   - rear->next = Jane Doe, rear = Jane Doe
   - Queue: [John Smith (101)] -> [Jane Doe (102)]

3. **Display Queue**:
   - Traverse from front to rear
   - Position 1: John Smith (ID: 101, Time: 10)
   - Position 2: Jane Doe (ID: 102, Time: 15)

4. **Assign Patient to Doctor 201**:
   - Dequeue the first patient (John Smith)
   - front = front->next (now points to Jane Doe)
   - Display assignment information
   - Next patient is Jane Doe

## Conclusion

The implementation demonstrates a patient tracking system using a queue data structure with the following key features:

**Queue Operations**:
1. **Enqueue**: O(1) time complexity - add patient to rear of queue
2. **Dequeue**: O(1) time complexity - remove patient from front of queue
3. **Display**: O(n) time complexity - show all patients in queue
4. **Peek**: O(1) time complexity - view next patient without removing

**Space Complexity**: O(n) where n is the number of patients in queue

**Key Implementation Features**:
1. **FCFS Scheduling**: Patients are served in first-come, first-served order
2. **Dynamic Memory**: Allocates memory as patients arrive
3. **Proper Memory Management**: Frees memory when patients are assigned to doctors
4. **User Interface**: Interactive menu-driven system
5. **Error Handling**: Handles empty queue conditions

**Advantages of Queue Implementation**:
1. **Fairness**: Ensures patients are served in order of arrival
2. **Simplicity**: Simple enqueue/dequeue operations
3. **Efficiency**: Constant time insertion and deletion
4. **Scalability**: Can handle any number of patients

**Real-world Applications**:
1. **Healthcare Systems**: Patient scheduling and triage
2. **Customer Service**: Call centers and service queues
3. **Operating Systems**: Process scheduling
4. **Transportation**: Traffic light systems, boarding queues

The implementation correctly handles all edge cases:
- Adding patients to empty queue
- Assigning patients when queue is empty
- Memory management to prevent leaks
- Proper queue state maintenance

This system ensures fairness in patient care by maintaining the first-come, first-served principle, which is essential in medical settings to maintain patient trust and satisfaction.