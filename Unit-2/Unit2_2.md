# Unit II Assignment 2: Doubly Circular Linked List for Ticket Reservation System

Implementation of a ticket reservation system for Galaxy Multiplex using a doubly circular linked list to track seat availability.

## Problem Statement

The ticket reservation system for Galaxy Multiplex uses a doubly circular linked list to track seat availability. The multiplex has 8 rows, with 8 seats in each row. An array stores head pointers for each row's linked list. Initially, some seats are randomly booked. The system supports:

a) Display the current list of available seats
b) Book one or more seats as per customer request
c) Cancel an existing booking when requested

## Pseudo Code

### Node Structure
```
Structure SeatNode:
    seatNumber: integer
    isAvailable: boolean
    next: pointer to SeatNode
    prev: pointer to SeatNode
```

### Initialize Seats
```
Algorithm InitializeSeats(rows, seatsPerRow):
    For each row:
        Create circular doubly linked list of seats
        Mark some seats as booked randomly
        Store head pointer in array
```

### Display Available Seats
```
Algorithm DisplayAvailableSeats(rowHeadArray):
    For each row:
        current = rowHead
        Print "Row X: "
        While current.next != rowHead:
            If current.isAvailable:
                Print current.seatNumber
            current = current.next
        If current.isAvailable:
            Print current.seatNumber
```

### Book Seats
```
Algorithm BookSeats(rowHeadArray, row, seatNumbers):
    current = rowHeadArray[row]
    While current.seatNumber != required seat number:
        current = current.next
        If current == rowHeadArray[row]:  // Completed circle
            Return "Seat not found"
    If current.isAvailable:
        current.isAvailable = false
        Return "Booking successful"
    Else:
        Return "Seat already booked"
```

### Cancel Booking
```
Algorithm CancelBooking(rowHeadArray, row, seatNumber):
    current = rowHeadArray[row]
    While current.seatNumber != seatNumber:
        current = current.next
        If current == rowHeadArray[row]:  // Completed circle
            Return "Seat not found"
    If NOT current.isAvailable:
        current.isAvailable = true
        Return "Cancellation successful"
    Else:
        Return "Seat was not booked"
```

## Code Implementation

```c
#include <iostream>
using namespace std;
#include <stdlib.h>
#include <time.h>

#define ROWS 8
#define SEATS_PER_ROW 8

struct SeatNode_rrd {
    int seatNumber_rrd;
    int isAvailable_rrd;
    struct SeatNode_rrd* next_rrd;
    struct SeatNode_rrd* prev_rrd;
};

struct SeatNode_rrd* rowHeads_rrd[ROWS];

struct SeatNode_rrd* createSeatNode_rrd(int seatNumber_rrd) {
    struct SeatNode_rrd* newSeat_rrd = (struct SeatNode_rrd*)malloc(sizeof(struct SeatNode_rrd));
    newSeat_rrd->seatNumber_rrd = seatNumber_rrd;
    newSeat_rrd->isAvailable_rrd = 1;
    newSeat_rrd->next_rrd = NULL;
    newSeat_rrd->prev_rrd = NULL;
    return newSeat_rrd;
}

void initializeSeats_rrd() {
    int row_rrd, seat_rrd;
    struct SeatNode_rrd* head_rrd;
    struct SeatNode_rrd* prev_rrd;
    struct SeatNode_rrd* newSeat_rrd;
    struct SeatNode_rrd* current_rrd;
    
    srand(time(NULL));
    
    for (row_rrd = 0; row_rrd < ROWS; row_rrd++) {
        head_rrd = createSeatNode_rrd(1);
        prev_rrd = head_rrd;
        
        for (seat_rrd = 2; seat_rrd <= SEATS_PER_ROW; seat_rrd++) {
            newSeat_rrd = createSeatNode_rrd(seat_rrd);
            prev_rrd->next_rrd = newSeat_rrd;
            newSeat_rrd->prev_rrd = prev_rrd;
            prev_rrd = newSeat_rrd;
        }
        
        prev_rrd->next_rrd = head_rrd;
        head_rrd->prev_rrd = prev_rrd;
        
        rowHeads_rrd[row_rrd] = head_rrd;
        
        current_rrd = head_rrd;
        do
        {
            if (rand() % 4 == 0) {
                current_rrd->isAvailable_rrd = 0;
            }
            current_rrd = current_rrd->next_rrd;
        } while (current_rrd != head_rrd);
    }
    
    cout << "Seats initialized successfully!" << endl;
}

void displayAvailableSeats_rrd() {
    int row_rrd;
    struct SeatNode_rrd* current_rrd;
    int availableCount_rrd;
    
    cout << "\n===== Available Seats =====" << endl;
    for (row_rrd = 0; row_rrd < ROWS; row_rrd++) {
        printf("Row %c: ", 'A' + row_rrd);
        current_rrd = rowHeads_rrd[row_rrd];
        availableCount_rrd = 0;
        
        if (current_rrd != NULL) {
            do
            {
                if (current_rrd->isAvailable_rrd) {
                    cout << "" << current_rrd->seatNumber_rrd << " ";
                    availableCount_rrd++;
                }
                current_rrd = current_rrd->next_rrd;
            } while (current_rrd != rowHeads_rrd[row_rrd]);
        }
        
        if (availableCount_rrd == 0) {
            cout << "No seats available";
        }
        cout << "" << endl;
    }
    cout << "==========================" << endl;
}

void displayAllSeats_rrd() {
    int row_rrd;
    struct SeatNode_rrd* current_rrd;
    
    cout << "\n===== All Seats Status =====" << endl;
    for (row_rrd = 0; row_rrd < ROWS; row_rrd++) {
        printf("Row %c: ", 'A' + row_rrd);
        current_rrd = rowHeads_rrd[row_rrd];
        
        if (current_rrd != NULL) {
            do
            {
                if (current_rrd->isAvailable_rrd) {
                    cout << "S" << current_rrd->seatNumber_rrd << "(A) ";
                } else {
                    cout << "S" << current_rrd->seatNumber_rrd << "(B) ";
                }
                current_rrd = current_rrd->next_rrd;
            } while (current_rrd != rowHeads_rrd[row_rrd]);
        }
        cout << "" << endl;
    }
    cout << "===========================" << endl;
    cout << "A = Available, B = Booked" << endl;
}

int bookSeats_rrd(int row_rrd, int seatNumber_rrd) {
    struct SeatNode_rrd* current_rrd;
    
    if (row_rrd < 0 || row_rrd >= ROWS) {
        cout << "Invalid row number!" << endl;
        return 0;
    }
    
    if ($3) {
        cout << "Invalid seat number!" << endl;
        return 0;
    }
    
    current_rrd = rowHeads_rrd[row_rrd];
    
    do
    {
        if ($3) {
            if ($3) {
                current_rrd->isAvailable_rrd = 0;
                cout << "Seat %c" << 'A' + row_rrd, seatNumber_rrd << " booked successfully!" << endl;
                return 1;
            } else {
                cout << "Seat %c" << 'A' + row_rrd, seatNumber_rrd << " is already booked!" << endl;
                return 0;
            }
        }
        current_rrd = current_rrd->next_rrd;
    } while (current_rrd != rowHeads_rrd[row_rrd]);
    
    cout << "Seat not found!" << endl;
    return 0;
}

int cancelBooking_rrd(int row_rrd, int seatNumber_rrd) {
    struct SeatNode_rrd* current_rrd;
    
    if ($3) {
        cout << "Invalid row number!" << endl;
        return 0;
    }
    
    if ($3) {
        cout << "Invalid seat number!" << endl;
        return 0;
    }
    current_rrd = rowHeads_rrd[row_rrd];
    do
    {
        if ($3) {
            if ($3) {
                current_rrd->isAvailable_rrd = 1;
                cout << "Booking for seat %c" << 'A' + row_rrd, seatNumber_rrd << " cancelled successfully!" << endl;
                return 1;
            } else {
                cout << "Seat %c" << 'A' + row_rrd, seatNumber_rrd << " was not booked!" << endl;
                return 0;
            }
        }
        current_rrd = current_rrd->next_rrd;
    }while (current_rrd != rowHeads_rrd[row_rrd]);
    
    cout << "Seat not found!" << endl;
    return 0;
}

int countAvailableSeatsInRow_rrd(int row_rrd) {
    int count_rrd = 0;
    struct SeatNode_rrd* current_rrd;
    
    if (row_rrd < 0 || row_rrd >= ROWS) {
        return -1;
    }
    
    current_rrd = rowHeads_rrd[row_rrd];
    
    if ($3) {
        do
        {
            if ($3) {
                count_rrd++;
            }
            current_rrd = current_rrd->next_rrd;
        } while (current_rrd != rowHeads_rrd[row_rrd]);
    }
    return count_rrd;
}

int countTotalAvailableSeats_rrd() {
    int totalCount_rrd = 0;
    int row_rrd;
    for ($3) {
        totalCount_rrd += countAvailableSeatsInRow_rrd(row_rrd);
    }
    return totalCount_rrd;
}

void displayMenu_rrd() {
    cout << "\n===== Galaxy Multiplex Ticket Reservation System =====" << endl;
    cout << "1. Display Available Seats" << endl;
    cout << "2. Display All Seats Status" << endl;
    cout << "3. Book Seats" << endl;
    cout << "4. Cancel Booking" << endl;
    cout << "5. Count Available Seats in a Row" << endl;
    cout << "6. Count Total Available Seats" << endl;
    cout << "7. Exit" << endl;
    cout << "=====================================================" << endl;
    cout << "Enter your choice: ";
}

#include <iostream>
using namespace std;
#include <stdlib.h>
#include <time.h>

#define ROWS 8
#define SEATS_PER_ROW 8

struct SeatNode_rrd {
    int seatNumber_rrd;
    int isAvailable_rrd;
    struct SeatNode_rrd* next_rrd;
    struct SeatNode_rrd* prev_rrd;
};

struct SeatNode_rrd* rowHeads_rrd[ROWS];

struct SeatNode_rrd* createSeatNode_rrd(int seatNumber_rrd);
void initializeSeats_rrd();
void displayAvailableSeats_rrd();
void displayAllSeats_rrd();
int bookSeats_rrd(int row_rrd, int seatNumber_rrd);
int cancelBooking_rrd(int row_rrd, int seatNumber_rrd);
int countAvailableSeatsInRow_rrd(int row_rrd);
int countTotalAvailableSeats_rrd();
void displayMenu_rrd();

int main() {
    int choice_rrd;
    int row_rrd, seatNumber_rrd, count_rrd;
    int totalCount_rrd;
    struct SeatNode_rrd* current_rrd;
    struct SeatNode_rrd* start_rrd;
    struct SeatNode_rrd* temp_rrd;
    
    cout << "Welcome to Galaxy Multiplex Ticket Reservation System!" << endl;
    
    initializeSeats_rrd();
    
    while (1) {
        displayMenu_rrd();
        cin >> choice_rrd;
        
        switch (choice_rrd) {
            case 1:
                displayAvailableSeats_rrd();
                break;
            
            case 2:
                displayAllSeats_rrd();
                break;
            
            case 3:
                cout << "Enter row (A=0, B=1, ..., H=7): ";
                cin >> row_rrd;
                cout << "Enter seat number (1-8): ";
                cin >> seatNumber_rrd;
                bookSeats_rrd(row_rrd, seatNumber_rrd);
                break;
            
            case 4:
                cout << "Enter row (A=0, B=1, ..., H=7): ";
                cin >> row_rrd;
                cout << "Enter seat number (1-8): ";
                cin >> seatNumber_rrd;
                cancelBooking_rrd(row_rrd, seatNumber_rrd);
                break;
            
            case 5:
                cout << "Enter row (0-7): ";
                cin >> row_rrd;
                count_rrd = countAvailableSeatsInRow_rrd(row_rrd);
                if (count_rrd >= 0) {
                    cout << "Available seats in row %c: " << 'A' + row_rrd, count_rrd << "" << endl;
                } else {
                    cout << "Invalid row number!" << endl;
                }
                break;
            
            case 6:
                totalCount_rrd = countTotalAvailableSeats_rrd();
                cout << "Total available seats: " << totalCount_rrd << "" << endl;
                break;
            
            case 7:
                cout << "Thank you for using Galaxy Multiplex Ticket Reservation System!" << endl;
                for (row_rrd = 0; row_rrd < ROWS; row_rrd++) {
                    if (rowHeads_rrd[row_rrd] != NULL) {
                        current_rrd = rowHeads_rrd[row_rrd];
                        start_rrd = current_rrd;
                        
                        do
                        {
                            temp_rrd = current_rrd;
                            current_rrd = current_rrd->next_rrd;
                            free(temp_rrd);
                        } while (current_rrd != start_rrd);
                        
                        rowHeads_rrd[row_rrd] = NULL;
                    }
                }
                exit(0);
            
            default:
                cout << "Invalid choice! Please try again." << endl;
        }
    }
    
    return 0;
}
```

## Output

```
Welcome to Galaxy Multiplex Ticket Reservation System!
Seats initialized successfully!

===== Galaxy Multiplex Ticket Reservation System =====
1. Display Available Seats
2. Display All Seats Status
3. Book Seats
4. Cancel Booking
5. Count Available Seats in a Row
6. Count Total Available Seats
7. Exit
=====================================================
Enter your choice: 1

===== Available Seats =====
Row A: 1 3 4 6 7 8 
Row B: 1 2 3 5 6 8 
Row C: 2 3 4 5 6 7 8 
Row D: 1 2 3 4 5 6 7 
Row E: 1 2 4 5 6 7 8 
Row F: 1 2 3 4 5 6 7 8 
Row G: 1 2 3 4 5 6 7 8 
Row H: 1 2 3 4 5 6 7 8 
==========================

===== Galaxy Multiplex Ticket Reservation System =====
1. Display Available Seats
2. Display All Seats Status
3. Book Seats
4. Cancel Booking
5. Count Available Seats in a Row
6. Count Total Available Seats
7. Exit
=====================================================
Enter your choice: 3
Enter row (A=0, B=1, ..., H=7): 0
Enter seat number (1-8): 1
Seat A1 booked successfully!
```

## Dry Run

1. **Initialize Seats**:
   - For each of the 8 rows, create a circular doubly linked list with 8 seats
   - Each seat node has seat number (1-8), availability flag, and pointers to next/prev nodes
   - Make the list circular by connecting last node to first and first to last
   - Randomly mark 25% of seats as booked

2. **Display Available Seats (Row A)**:
   - Start from head of row A
   - Traverse circular list, checking availability flag
   - Print seat numbers of available seats
   - Continue until back to head node

3. **Book Seat A1**:
   - Validate row (0) and seat number (1)
   - Start from head of row 0
   - Traverse to find seat 1
   - Check if available (it is)
   - Mark as booked (set isAvailable to 0)

4. **Cancel Booking for A1**:
   - Validate row (0) and seat number (1)
   - Start from head of row 0
   - Traverse to find seat 1
   - Check if booked (it is)
   - Mark as available (set isAvailable to 1)

## Conclusion

The implementation demonstrates an efficient ticket reservation system using doubly circular linked lists. Key advantages of this approach include:

1. **Memory Efficiency**: Only allocate memory for actual seats, not a fixed 2D array
2. **Flexibility**: Easy to modify seat arrangements or add/remove rows
3. **Bidirectional Traversal**: Can traverse forward or backward through seats
4. **Circular Nature**: Natural fit for row-based seat arrangements

**Time Complexities**:
- Initialization: O(ROWS × SEATS_PER_ROW)
- Display Available Seats: O(ROWS × SEATS_PER_ROW)
- Book/Cancel Seats: O(SEATS_PER_ROW) in worst case
- Count Available Seats: O(SEATS_PER_ROW) for single row, O(ROWS × SEATS_PER_ROW) for total

The doubly circular linked list structure is particularly well-suited for this application because:
1. Each row naturally forms a circle of seats
2. Bidirectional traversal allows efficient searching in either direction
3. Dynamic memory allocation adapts to the actual seat configuration
4. The structure easily accommodates different numbers of seats per row

The system handles edge cases properly, including invalid inputs and attempts to book already booked seats or cancel unbooked seats. Memory is properly managed with allocation and deallocation to prevent memory leaks.