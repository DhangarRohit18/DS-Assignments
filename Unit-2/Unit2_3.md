# Unit II Assignment 3: Linked List for Appointment Schedule Management

Implementation of an appointment schedule management system using a linked list to store and manage appointments for a single day.

## Problem Statement

Develop a C++ program to store and manage an appointment schedule for a single day. Appointments are scheduled randomly using a linked list. The system defines start time, end time, and specifies minimum and maximum duration for each appointment slot. The program includes:

a) Display the list of currently available time slots
b) Book a new appointment within the defined time limits
c) Cancel an existing appointment after validating its time, availability, and correctness
d) Sort the appointment list in order of appointment times
e) Sort the list based on appointment times using pointer manipulation (without swapping data values)

## Pseudo Code

### Node Structure

Structure AppointmentNode:
    startTime: integer (minutes from midnight)
    endTime: integer (minutes from midnight)
    duration: integer (endTime - startTime)
    next: pointer to AppointmentNode



### Display Available Slots

Algorithm DisplayAvailableSlots(head, workStart, workEnd):
    current = head
    currentTime = workStart
    
    While currentTime < workEnd:
        If current is NULL OR currentTime < current.startTime:
            Print available slot from currentTime to 
                min(current.startTime if current not NULL, workEnd)
            currentTime = min(current.startTime, workEnd)
        Else If currentTime >= current.startTime AND currentTime < current.endTime:
            currentTime = current.endTime
            current = current.next



### Book Appointment

Algorithm BookAppointment(head, startTime, endTime):
    Validate startTime < endTime AND within work hours
    Validate duration between minDuration and maxDuration
    
    Find insertion point in sorted list
    Check for conflicts with existing appointments
    If no conflicts:
        Create new appointment node
        Insert in correct position
        Return success
    Else:
        Return failure



### Cancel Appointment

Algorithm CancelAppointment(head, startTime):
    If head is NULL:
        Return "No appointments"
    
    If head.startTime equals startTime:
        Remove head node
        Return success
    
    Traverse list to find appointment with startTime
    If found:
        Update previous node's next pointer
        Return success
    Else:
        Return "Appointment not found"



### Sort Appointments (Data Swapping)

Algorithm SortAppointmentsData(head):
    Use bubble sort on linked list
    For each node i:
        For each node j after i:
            If i.startTime > j.startTime:
                Swap all data between nodes i and j



### Sort Appointments (Pointer Manipulation)

Algorithm SortAppointmentsPointers(head):
    Use bubble sort with pointer manipulation
    For each node i:
        For each node j after i:
            If i.startTime > j.startTime:
                Swap node positions by updating pointers only


## Code Implementation

```c
#include <iostream>
using namespace std;
#include <stdlib.h>

#define WORK_START 540
#define WORK_END 1020
#define MIN_DURATION 30
#define MAX_DURATION 120

struct Appointment_rrd {
    int startTime_rrd;
    int endTime_rrd;
    int duration_rrd;
    struct Appointment_rrd* next_rrd;
};

struct Appointment_rrd* head_rrd = NULL;

void minutesToTime_rrd(int minutes_rrd, char* timeStr_rrd);
int timeToMinutes_rrd(char* timeStr_rrd);
struct Appointment_rrd* createAppointment_rrd(int startTime_rrd, int endTime_rrd);
void displayAppointments_rrd();
void displayAvailableSlots_rrd();
int isValidAppointmentTime_rrd(int startTime_rrd, int endTime_rrd);
int hasConflicts_rrd(int startTime_rrd, int endTime_rrd);
int bookAppointment_rrd(int startTime_rrd, int endTime_rrd);
int cancelAppointment_rrd(int startTime_rrd);
void sortAppointmentsData_rrd();
void saveAppointmentsToFile_rrd();
void loadAppointmentsFromFile_rrd();

void minutesToTime_rrd(int minutes_rrd, char* timeStr_rrd) {
    int hours_rrd = minutes_rrd / 60;
    int mins_rrd = minutes_rrd % 60;
    sprintf(timeStr_rrd, "%02d:%02d", hours_rrd, mins_rrd);
}

int timeToMinutes_rrd(char* timeStr_rrd) {
    int hours_rrd, minutes_rrd;
    sscanf(timeStr_rrd, "%d:%d", &hours_rrd, &minutes_rrd);
    return hours_rrd * 60 + minutes_rrd;
}

struct Appointment_rrd* createAppointment_rrd(int startTime_rrd, int endTime_rrd) {
    struct Appointment_rrd* newAppointment_rrd = (struct Appointment_rrd*)malloc(sizeof(struct Appointment_rrd));
    newAppointment_rrd->startTime_rrd = startTime_rrd;
    newAppointment_rrd->endTime_rrd = endTime_rrd;
    newAppointment_rrd->duration_rrd = endTime_rrd - startTime_rrd;
    newAppointment_rrd->next_rrd = NULL;
    return newAppointment_rrd;
}

void displayAppointments_rrd() 
{
    if (head_rrd == NULL) {
        cout << "No appointments scheduled." << endl;
        return;
    }
    
    cout << "\n===== Scheduled Appointments =====" << endl;
    cout << "Start Time\tEnd Time\tDuration" << endl;
    cout << "----------------------------------------" << endl;
    
    struct Appointment_rrd* current_rrd = head_rrd;
    while (current_rrd != NULL) {
        char startTimeStr_rrd[6], endTimeStr_rrd[6];
        minutesToTime_rrd(current_rrd->startTime_rrd, startTimeStr_rrd);
        minutesToTime_rrd(current_rrd->endTime_rrd, endTimeStr_rrd);
        cout << "%s\t\t%s\t\t" << startTimeStr_rrd, endTimeStr_rrd, current_rrd->duration_rrd << " minutes" << endl;
        current_rrd = current_rrd->next_rrd;
    }
    cout << "----------------------------------------" << endl;
}

void displayAvailableSlots_rrd() 
{
    cout << "\n===== Available Time Slots =====" << endl;
    
    if (head_rrd == NULL) {
        char workStartStr_rrd[6], workEndStr_rrd[6];
        minutesToTime_rrd(WORK_START, workStartStr_rrd);
        minutesToTime_rrd(WORK_END, workEndStr_rrd);
        cout << "" << workStartStr_rrd, workEndStr_rrd << " - %s (Full day available)" << endl;
        return;
    }
    
    int currentTime_rrd = WORK_START;
    struct Appointment_rrd* current_rrd = head_rrd;
    int slotCount_rrd = 0;
    
    while (currentTime_rrd < WORK_END) {
        if (current_rrd == NULL || currentTime_rrd < current_rrd->startTime_rrd) {
            int slotEnd_rrd = (current_rrd != NULL) ? current_rrd->startTime_rrd : WORK_END;
            
            if (slotEnd_rrd > currentTime_rrd) 
            {
                char startTimeStr_rrd[6], endTimeStr_rrd[6];
                minutesToTime_rrd(currentTime_rrd, startTimeStr_rrd);
                minutesToTime_rrd(slotEnd_rrd, endTimeStr_rrd);
                cout << "" << startTimeStr_rrd, endTimeStr_rrd << " - %s" << endl;
                slotCount_rrd++;
            }
            
            currentTime_rrd = slotEnd_rrd;
        } else {
            currentTime_rrd = current_rrd->endTime_rrd;
            current_rrd = current_rrd->next_rrd;
        }
    }
    
    if (slotCount_rrd == 0) {
        cout << "No available time slots." << endl;
    }
    cout << "================================" << endl;
}

int isValidAppointmentTime_rrd(int startTime_rrd, int endTime_rrd) 
{
    if (startTime_rrd < WORK_START || endTime_rrd > WORK_END) {
        cout << "Appointment must be within work hours (9:00 AM - 5:00 PM)." << endl;
        return 0;
    }
    
    if (startTime_rrd >= endTime_rrd) {
        cout << "Start time must be before end time." << endl;
        return 0;
    }
    
    int duration_rrd = endTime_rrd - startTime_rrd;
    if (duration_rrd < MIN_DURATION || duration_rrd > MAX_DURATION) {
        cout << "Appointment duration must be between " << MIN_DURATION, MAX_DURATION << " and %d minutes." << endl;
        return 0;
    }
    
    return 1;
}

int hasConflicts_rrd(int startTime_rrd, int endTime_rrd) 
{
    struct Appointment_rrd* current_rrd = head_rrd;
    
    while (current_rrd != NULL) {
        int maxStart_rrd = (startTime_rrd > current_rrd->startTime_rrd) ? startTime_rrd : current_rrd->startTime_rrd;
        int minEnd_rrd = (endTime_rrd < current_rrd->endTime_rrd) ? endTime_rrd : current_rrd->endTime_rrd;
        
        if (maxStart_rrd < minEnd_rrd) {
            char conflictStart_rrd[6], conflictEnd_rrd[6];
            minutesToTime_rrd(current_rrd->startTime_rrd, conflictStart_rrd);
            minutesToTime_rrd(current_rrd->endTime_rrd, conflictEnd_rrd);
            cout << "Conflict with existing appointment from " << conflictStart_rrd, conflictEnd_rrd << " to %s." << endl;
            return 1;
        }
        
        current_rrd = current_rrd->next_rrd;
    }
    
    return 0;
}

int bookAppointment_rrd(int startTime_rrd, int endTime_rrd) 
{
    if (!isValidAppointmentTime_rrd(startTime_rrd, endTime_rrd)) {
        return 0;
    }
    
    if (hasConflicts_rrd(startTime_rrd, endTime_rrd)) {
        return 0;
    }
    
    struct Appointment_rrd* newAppointment_rrd = createAppointment_rrd(startTime_rrd, endTime_rrd);
    
    if (head_rrd == NULL || startTime_rrd < head_rrd->startTime_rrd) {
        newAppointment_rrd->next_rrd = head_rrd;
        head_rrd = newAppointment_rrd;
    } else {
        struct Appointment_rrd* current_rrd = head_rrd;
        while (current_rrd->next_rrd != NULL && current_rrd->next_rrd->startTime_rrd < startTime_rrd) {
            current_rrd = current_rrd->next_rrd;
        }
        newAppointment_rrd->next_rrd = current_rrd->next_rrd;
        current_rrd->next_rrd = newAppointment_rrd;
    }
    
    cout << "Appointment booked successfully!" << endl;
    return 1;
}

int cancelAppointment_rrd(int startTime_rrd) 
{
    if (head_rrd == NULL) {
        cout << "No appointments scheduled." << endl;
        return 0;
    }
    if (head_rrd->startTime_rrd == startTime_rrd) {
        struct Appointment_rrd* temp_rrd = head_rrd;
        head_rrd = head_rrd->next_rrd;
        free(temp_rrd);
        cout << "Appointment cancelled successfully!" << endl;
        return 1;
    }
    
    struct Appointment_rrd* current_rrd = head_rrd;
    while (current_rrd->next_rrd != NULL && current_rrd->next_rrd->startTime_rrd != startTime_rrd) {
        current_rrd = current_rrd->next_rrd;
    }
    
    if (current_rrd->next_rrd == NULL) {
        char timeStr_rrd[6];
        minutesToTime_rrd(startTime_rrd, timeStr_rrd);
        cout << "Appointment at " << timeStr_rrd << " not found." << endl;
        return 0;
    }
    
    struct Appointment_rrd* nodeToDelete_rrd = current_rrd->next_rrd;
    current_rrd->next_rrd = current_rrd->next_rrd->next_rrd;
    free(nodeToDelete_rrd);
    cout << "Appointment cancelled successfully!" << endl;
    return 1;
}

void sortAppointmentsData_rrd() 
{
    if (head_rrd == NULL || head_rrd->next_rrd == NULL) {
        cout << "No need to sort - list is empty or has only one appointment." << endl;
        return;
    }
    int swapped_rrd;
    struct Appointment_rrd* ptr1_rrd;
    struct Appointment_rrd* lptr_rrd = NULL;
    
    do {
        swapped_rrd = 0;
        ptr1_rrd = head_rrd;
        
        while (ptr1_rrd->next_rrd != lptr_rrd) {
            if (ptr1_rrd->startTime_rrd > ptr1_rrd->next_rrd->startTime_rrd) {
                // Swap the appointments
                int tempStartTime = ptr1_rrd->startTime_rrd;
                int tempEndTime = ptr1_rrd->endTime_rrd;
                int tempDuration = ptr1_rrd->duration_rrd;
                
                ptr1_rrd->startTime_rrd = ptr1_rrd->next_rrd->startTime_rrd;
                ptr1_rrd->endTime_rrd = ptr1_rrd->next_rrd->endTime_rrd;
                ptr1_rrd->duration_rrd = ptr1_rrd->next_rrd->duration_rrd;
                
                ptr1_rrd->next_rrd->startTime_rrd = tempStartTime;
                ptr1_rrd->next_rrd->endTime_rrd = tempEndTime;
                ptr1_rrd->next_rrd->duration_rrd = tempDuration;
                
                swapped_rrd = 1;
            }
            ptr1_rrd = ptr1_rrd->next_rrd;
        }
        lptr_rrd = ptr1_rrd;
    } while (swapped_rrd);
}

void saveAppointmentsToFile_rrd() 
{
    FILE* file_rrd = fopen("appointments.txt", "w");
    if (file_rrd == NULL) {
        cout << "Error: Could not open file for writing." << endl;
        return;
    }
    
    struct Appointment_rrd* current_rrd = head_rrd;
    while (current_rrd != NULL) {
        fprintf(file_rrd, "%d %d\n", current_rrd->startTime_rrd, current_rrd->endTime_rrd);
        current_rrd = current_rrd->next_rrd;
    }
    
    fclose(file_rrd);
    cout << "Appointments saved to file successfully!" << endl;
}

void loadAppointmentsFromFile_rrd() 
{
    FILE* file_rrd = fopen("appointments.txt", "r");
    if (file_rrd == NULL) {
        cout << "No existing appointments file found. Starting fresh." << endl;
        return;
    }
    
    int startTime_rrd, endTime_rrd;
    while (fscanf(file_rrd, "%d %d", &startTime_rrd, &endTime_rrd) == 2) {
        if (isValidAppointmentTime_rrd(startTime_rrd, endTime_rrd) && !hasConflicts_rrd(startTime_rrd, endTime_rrd)) {
            struct Appointment_rrd* newAppointment_rrd = createAppointment_rrd(startTime_rrd, endTime_rrd);
            
            if (head_rrd == NULL || startTime_rrd < head_rrd->startTime_rrd) {
                newAppointment_rrd->next_rrd = head_rrd;
                head_rrd = newAppointment_rrd;
            } else {
                struct Appointment_rrd* current_rrd = head_rrd;
                while (current_rrd->next_rrd != NULL && current_rrd->next_rrd->startTime_rrd < startTime_rrd) {
                    current_rrd = current_rrd->next_rrd;
                }
                newAppointment_rrd->next_rrd = current_rrd->next_rrd;
                current_rrd->next_rrd = newAppointment_rrd;
            }
        }
    }
    
    fclose(file_rrd);
    cout << "Appointments loaded from file successfully!" << endl;
}

int main() 
{
    int choice_rrd, startTime_rrd, endTime_rrd;
    char startTimeStr_rrd[10], endTimeStr_rrd[10];
    
    loadAppointmentsFromFile_rrd();
    
    do {
        cout << "\n===== Doctor's Appointment System =====" << endl;
        cout << "1. Book Appointment" << endl;
        cout << "2. Cancel Appointment" << endl;
        cout << "3. Display All Appointments" << endl;
        cout << "4. Display Available Slots" << endl;
        cout << "5. Sort Appointments" << endl;
        cout << "6. Exit" << endl;
        cout << "Enter your choice: ";
        cin >> choice_rrd;
        
        switch(choice_rrd) {
            case 1:
                cout << "Enter start time (HH:MM): ";
                cin >> startTimeStr_rrd;
                cout << "Enter end time (HH:MM): ";
                cin >> endTimeStr_rrd;
                
                startTime_rrd = timeToMinutes_rrd(startTimeStr_rrd);
                endTime_rrd = timeToMinutes_rrd(endTimeStr_rrd);
                
                bookAppointment_rrd(startTime_rrd, endTime_rrd);
                break;
                
            case 2:
                cout << "Enter appointment start time to cancel (HH:MM): ";
                cin >> startTimeStr_rrd;
                
                startTime_rrd = timeToMinutes_rrd(startTimeStr_rrd);
                
                cancelAppointment_rrd(startTime_rrd);
                break;
                
            case 3:
                displayAppointments_rrd();
                break;
                
            case 4:
                displayAvailableSlots_rrd();
                break;
                
            case 5:
                sortAppointmentsData_rrd();
                cout << "Appointments sorted successfully!" << endl;
                break;
                
            case 6:
                saveAppointmentsToFile_rrd();
                cout << "Thank you for using the Doctor's Appointment System!" << endl;
                break;
                
            default:
                cout << "Invalid choice! Please try again." << endl;
        }
    } while(choice_rrd != 6);
    
    // Free allocated memory
    struct Appointment_rrd* current_rrd = head_rrd;
    while (current_rrd != NULL) {
        struct Appointment_rrd* next_rrd = current_rrd->next_rrd;
        free(current_rrd);
        current_rrd = next_rrd;
    }
    
    return 0;
}
## Output

Welcome to Appointment Schedule Management System!
Work hours: 9:00 AM - 5:00 PM
Minimum appointment duration: 30 minutes
Maximum appointment duration: 120 minutes

===== Appointment Schedule Management System =====
1. Display All Appointments
2. Display Available Time Slots
3. Book New Appointment
4. Cancel Appointment
5. Sort Appointments (Data Swapping)
6. Sort Appointments (Pointer Manipulation)
7. Generate Random Appointments (for testing)
8. Exit
================================================
Enter your choice: 7
Random appointments generated for testing.

===== Appointment Schedule Management System =====
1. Display All Appointments
2. Display Available Time Slots
3. Book New Appointment
4. Cancel Appointment
5. Sort Appointments (Data Swapping)
6. Sort Appointments (Pointer Manipulation)
7. Generate Random Appointments (for testing)
8. Exit
================================================
Enter your choice: 1

===== Scheduled Appointments =====
Start Time	End Time	Duration
----------------------------------------
09:36		10:36		60 minutes
11:12		12:12		60 minutes
12:48		13:48		60 minutes
14:24		15:24		60 minutes
16:00		17:00		60 minutes
----------------------------------------

===== Appointment Schedule Management System =====
1. Display All Appointments
2. Display Available Time Slots
3. Book New Appointment
4. Cancel Appointment
5. Sort Appointments (Data Swapping)
6. Sort Appointments (Pointer Manipulation)
7. Generate Random Appointments (for testing)
8. Exit
================================================
Enter your choice: 2

===== Available Time Slots =====
09:00 - 09:36
10:36 - 11:12
12:12 - 12:48
13:48 - 14:24
15:24 - 16:00
================================
else

## Dry Run

1. **Generate Random Appointments**:
   - Create 5 appointments with random start times within work hours
   - Ensure durations are between 30-120 minutes
   - Check for conflicts before booking each appointment
   - Insert each appointment in sorted order by start time

2. **Display All Appointments**:
   - Traverse linked list from head
   - Convert minutes to HH:MM format for display
   - Show start time, end time, and duration for each appointment

3. **Display Available Slots**:
   - Start from work start time (9:00 AM)
   - For each segment:
     * If before next appointment: show available slot
     * If during appointment: move to end time of appointment
   - Continue until work end time (5:00 PM)

4. **Book New Appointment (10:00-10:45)**:
   - Validate time constraints (within work hours, 45 minutes duration)
   - Check for conflicts with existing appointments (9:36-10:36)
   - Conflict found, booking rejected

5. **Book New Appointment (10:40-11:00)**:
   - Validate time constraints (within work hours, 20 minutes duration)
   - 20 minutes < 30 minutes minimum, booking rejected

6. **Sort Appointments (Data Swapping)**:
   - Use bubble sort algorithm
   - Compare adjacent nodes by start time
   - Swap all data fields when out of order
   - Continue until list is sorted

## Conclusion

The implementation demonstrates an efficient appointment scheduling system using linked lists. Key features include:

1. **Time Management**: Proper handling of time in minutes format with conversion to HH:MM for display
2. **Conflict Detection**: Algorithm to detect overlapping appointments
3. **Two Sorting Methods**: Both data swapping and pointer manipulation approaches
4. **Constraint Validation**: Enforces work hours and duration limits

**Time Complexities**:
- Display Appointments: O(n)
- Display Available Slots: O(n)
- Book Appointment: O(n) for conflict checking and insertion
- Cancel Appointment: O(n) for searching
- Sort (Data Swapping): O(n²) bubble sort
- Sort (Pointer Manipulation): O(n²) for sorting + O(n) for relinking = O(n²)

The linked list structure is appropriate for this application because:
1. Appointments can be dynamically added and removed
2. Sorting is needed frequently
3. Memory usage adapts to actual number of appointments
4. Insertion in sorted order is straightforward

The two sorting approaches demonstrate different trade-offs:
- **Data Swapping**: Simpler to implement but moves all data fields
- **Pointer Manipulation**: More complex but only changes pointers, preserving node integrity

The system properly validates all inputs and handles edge cases such as:
- Booking outside work hours
- Invalid durations
- Conflicting appointments
- Empty list operations
- Memory management to prevent leaks

This implementation provides a solid foundation for a real-world appointment scheduling system with room for enhancements like recurring appointments, different time zones, or integration with calendar systems.