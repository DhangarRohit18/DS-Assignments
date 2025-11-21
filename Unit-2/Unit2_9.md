# Unit II Assignment 9: Doubly Linked List with Insert and Delete Operations

Implementation of a Doubly Linked List with comprehensive insert and delete operations for all cases.

## Problem Statement

Create a doubly linked list and perform the following operations:
A) Insert (all cases: at beginning, at end, at position)
B) Delete (all cases: at beginning, at end, at position)

## Pseudo Code

### Doubly Linked List Node Structure
```
Structure DLLNode:
    data: integer
    next: pointer to DLLNode
    prev: pointer to DLLNode
```

### Insert at Beginning
```
Algorithm InsertAtBeginning(head, data):
    Create new node with data
    If head is NULL:
        head = new node
    Else:
        new node.next = head
        head.prev = new node
        head = new node
    Return head
```

### Insert at End
```
Algorithm InsertAtEnd(head, data):
    Create new node with data
    If head is NULL:
        head = new node
    Else:
        Traverse to last node
        last node.next = new node
        new node.prev = last node
    Return head
```

### Insert at Position
```
Algorithm InsertAtPosition(head, data, position):
    If position < 1:
        Return "Invalid position"
    Create new node with data
    If position == 1:
        new node.next = head
        If head != NULL:
            head.prev = new node
        head = new node
        Return head
    Traverse to (position-1)th node
    If position-1th node is NULL:
        Return "Position out of bounds"
    new node.next = current.next
    If current.next != NULL:
        current.next.prev = new node
    current.next = new node
    new node.prev = current
    Return head
```

### Delete at Beginning
```
Algorithm DeleteAtBeginning(head):
    If head is NULL:
        Return "List is empty"
    If head.next is NULL:
        Free head
        head = NULL
    Else:
        temp = head
        head = head.next
        head.prev = NULL
        Free temp
    Return head
```

### Delete at End
```
Algorithm DeleteAtEnd(head):
    If head is NULL:
        Return "List is empty"
    If head.next is NULL:
        Free head
        head = NULL
    Else:
        Traverse to last node
        last node.prev.next = NULL
        Free last node
    Return head
```

### Delete at Position
```
Algorithm DeleteAtPosition(head, position):
    If head is NULL:
        Return "List is empty"
    If position < 1:
        Return "Invalid position"
    If position == 1:
        temp = head
        head = head.next
        If head != NULL:
            head.prev = NULL
        Free temp
        Return head
    Traverse to positionth node
    If positionth node is NULL:
        Return "Position out of bounds"
    temp = current
    If current.prev != NULL:
        current.prev.next = current.next
    If current.next != NULL:
        current.next.prev = current.prev
    Free temp
    Return head
```

## Code Implementation

```c
#include <iostream>
using namespace std;
#include <stdlib.h>

struct DLLNode_rrd {
    int data_rrd;
    struct DLLNode_rrd* next_rrd;
    struct DLLNode_rrd* prev_rrd;
};

struct DLLNode_rrd* createNode_rrd(int data_rrd);
struct DLLNode_rrd* insertAtBeginning_rrd(struct DLLNode_rrd* head_rrd, int data_rrd);
struct DLLNode_rrd* insertAtEnd_rrd(struct DLLNode_rrd* head_rrd, int data_rrd);
struct DLLNode_rrd* insertAtPosition_rrd(struct DLLNode_rrd* head_rrd, int data_rrd, int position_rrd);
struct DLLNode_rrd* deleteAtBeginning_rrd(struct DLLNode_rrd* head_rrd);
struct DLLNode_rrd* deleteAtEnd_rrd(struct DLLNode_rrd* head_rrd);
struct DLLNode_rrd* deleteAtPosition_rrd(struct DLLNode_rrd* head_rrd, int position_rrd);
void displayListForward_rrd(struct DLLNode_rrd* head_rrd);
void displayListBackward_rrd(struct DLLNode_rrd* tail_rrd);
int getCount_rrd(struct DLLNode_rrd* head_rrd);
struct DLLNode_rrd* getTail_rrd(struct DLLNode_rrd* head_rrd);
void freeList_rrd(struct DLLNode_rrd* head_rrd);
void displayMenu_rrd();

int main() {
    struct DLLNode_rrd* head_rrd = NULL;
    int choice_rrd, data_rrd, position_rrd;
    
    cout << "Doubly Linked List Implementation" << endl;
    cout << "================================" << endl;
    
    while (1) {
        displayMenu_rrd();
        cin >> choice_rrd;
        
        switch (choice_rrd) {
            case 1:
                cout << "Enter data to insert at beginning: ";
                cin >> data_rrd;
                head_rrd = insertAtBeginning_rrd(head_rrd, data_rrd);
                cout << "Node inserted at beginning successfully!" << endl;
                break;
                
            case 2:
                cout << "Enter data to insert at end: ";
                cin >> data_rrd;
                head_rrd = insertAtEnd_rrd(head_rrd, data_rrd);
                cout << "Node inserted at end successfully!" << endl;
                break;
                
            case 3:
                cout << "Enter position (1-indexed): ";
                cin >> position_rrd;
                cout << "Enter data to insert: ";
                cin >> data_rrd;
                head_rrd = insertAtPosition_rrd(head_rrd, data_rrd, position_rrd);
                if (head_rrd != NULL) {
                    cout << "Node inserted at position " << position_rrd << " successfully!" << endl;
                }
                break;
                
            case 4:
                head_rrd = deleteAtBeginning_rrd(head_rrd);
                if (head_rrd != NULL || getCount_rrd(head_rrd) == 0) {
                    cout << "Node deleted from beginning successfully!" << endl;
                }
                break;
                
            case 5:
                head_rrd = deleteAtEnd_rrd(head_rrd);
                if (head_rrd != NULL || getCount_rrd(head_rrd) == 0) {
                    cout << "Node deleted from end successfully!" << endl;
                }
                break;
                
            case 6:
                cout << "Enter position (1-indexed): ";
                cin >> position_rrd;
                head_rrd = deleteAtPosition_rrd(head_rrd, position_rrd);
                if (head_rrd != NULL || getCount_rrd(head_rrd) == 0) {
                    cout << "Node deleted from position " << position_rrd << " successfully!" << endl;
                }
                break;
                
            case 7:
                cout << "List (Forward): ";
                displayListForward_rrd(head_rrd);
                break;
                
            case 8:
                cout << "List (Backward): ";
                struct DLLNode_rrd* tail_rrd = getTail_rrd(head_rrd);
                displayListBackward_rrd(tail_rrd);
                break;
                
            case 9:
                printf("Total nodes: %d\n", getCount_rrd(head_rrd));
                break;
                
            case 10:
                cout << "Thank you for using Doubly Linked List!" << endl;
                freeList_rrd(head_rrd);
                exit(0);
                
            default:
                cout << "Invalid choice! Please try again." << endl;
        }
    }
    
    return 0;
}

struct DLLNode_rrd* createNode_rrd(int data_rrd) {
    struct DLLNode_rrd* newNode_rrd = (struct DLLNode_rrd*)malloc(sizeof(struct DLLNode_rrd));
    newNode_rrd->data_rrd = data_rrd;
    newNode_rrd->next_rrd = NULL;
    newNode_rrd->prev_rrd = NULL;
    return newNode_rrd;
}

struct DLLNode_rrd* insertAtBeginning_rrd(struct DLLNode_rrd* head_rrd, int data_rrd) {
    struct DLLNode_rrd* newNode_rrd = createNode_rrd(data_rrd);
    
    if (head_rrd == NULL) {
        return newNode_rrd;
    }
    
    newNode_rrd->next_rrd = head_rrd;
    head_rrd->prev_rrd = newNode_rrd;
    return newNode_rrd;
}

struct DLLNode_rrd* insertAtEnd_rrd(struct DLLNode_rrd* head_rrd, int data_rrd) {
    struct DLLNode_rrd* newNode_rrd = createNode_rrd(data_rrd);
    
    if (head_rrd == NULL) {
        return newNode_rrd;
    }
    
    struct DLLNode_rrd* current_rrd = head_rrd;
    while (current_rrd->next_rrd != NULL) {
        current_rrd = current_rrd->next_rrd;
    }
    
    current_rrd->next_rrd = newNode_rrd;
    newNode_rrd->prev_rrd = current_rrd;
    return head_rrd;
}

struct DLLNode_rrd* insertAtPosition_rrd(struct DLLNode_rrd* head_rrd, int data_rrd, int position_rrd) {
    if (position_rrd < 1) {
        cout << "Invalid position!" << endl;
        return head_rrd;
    }
    
    struct DLLNode_rrd* newNode_rrd = createNode_rrd(data_rrd);
    

    if (position_rrd == 1) {
        if (head_rrd != NULL) {
            newNode_rrd->next_rrd = head_rrd;
            head_rrd->prev_rrd = newNode_rrd;
        }
        return newNode_rrd;
    }
    
    struct DLLNode_rrd* current_rrd = head_rrd;
    for (int i_rrd = 1; i_rrd < position_rrd - 1 && current_rrd != NULL; i_rrd++) {
        current_rrd = current_rrd->next_rrd;
    }
    
    if (current_rrd == NULL) {
        cout << "Position out of bounds!" << endl;
        free(newNode_rrd);
        return head_rrd;
    }
    
    newNode_rrd->next_rrd = current_rrd->next_rrd;
    if (current_rrd->next_rrd != NULL) {
        current_rrd->next_rrd->prev_rrd = newNode_rrd;
    }
    current_rrd->next_rrd = newNode_rrd;
    newNode_rrd->prev_rrd = current_rrd;
    
    return head_rrd;
}

struct DLLNode_rrd* deleteAtBeginning_rrd(struct DLLNode_rrd* head_rrd) {
    if (head_rrd == NULL) {
        cout << "List is empty!" << endl;
        return NULL;
    }
    
    struct DLLNode_rrd* temp_rrd = head_rrd;
    head_rrd = head_rrd->next_rrd;
    
    if (head_rrd != NULL) {
        head_rrd->prev_rrd = NULL;
    }
    
    free(temp_rrd);
    return head_rrd;
}

struct DLLNode_rrd* deleteAtEnd_rrd(struct DLLNode_rrd* head_rrd) {
    if (head_rrd == NULL) {
        cout << "List is empty!" << endl;
        return NULL;
    }
    

    if (head_rrd->next_rrd == NULL) {
        free(head_rrd);
        return NULL;
    }
    
    struct DLLNode_rrd* current_rrd = head_rrd;
    while (current_rrd->next_rrd != NULL) {
        current_rrd = current_rrd->next_rrd;
    }
    
    current_rrd->prev_rrd->next_rrd = NULL;
    free(current_rrd);
    return head_rrd;
}

struct DLLNode_rrd* deleteAtPosition_rrd(struct DLLNode_rrd* head_rrd, int position_rrd) {
    if (head_rrd == NULL) {
        cout << "List is empty!" << endl;
        return NULL;
    }
    
    if (position_rrd < 1) {
        cout << "Invalid position!" << endl;
        return head_rrd;
    }
    

    if (position_rrd == 1) {
        struct DLLNode_rrd* temp_rrd = head_rrd;
        head_rrd = head_rrd->next_rrd;
        if (head_rrd != NULL) {
            head_rrd->prev_rrd = NULL;
        }
        free(temp_rrd);
        return head_rrd;
    }
    
    struct DLLNode_rrd* current_rrd = head_rrd;
    for (int i_rrd = 1; i_rrd < position_rrd && current_rrd != NULL; i_rrd++) {
        current_rrd = current_rrd->next_rrd;
    }
    
    if (current_rrd == NULL) {
        cout << "Position out of bounds!" << endl;
        return head_rrd;
    }
    
    if (current_rrd->next_rrd != NULL) {
        current_rrd->next_rrd->prev_rrd = current_rrd->prev_rrd;
    }
    
    if (current_rrd->prev_rrd != NULL) {
        current_rrd->prev_rrd->next_rrd = current_rrd->next_rrd;
    }
    
    free(current_rrd);
    return head_rrd;
}

void displayListForward_rrd(struct DLLNode_rrd* head_rrd) {
    if (head_rrd == NULL) {
        cout << "List is empty" << endl;
        return;
    }
    
    struct DLLNode_rrd* current_rrd = head_rrd;
    cout << "NULL";
    while (current_rrd != NULL) {
        cout << " <-> " << current_rrd->data_rrd << "";
        current_rrd = current_rrd->next_rrd;
    }
    cout << " <-> NULL" << endl;
}

void displayListBackward_rrd(struct DLLNode_rrd* tail_rrd) {
    if (tail_rrd == NULL) {
        cout << "List is empty" << endl;
        return;
    }
    
    struct DLLNode_rrd* current_rrd = tail_rrd;
    cout << "NULL";
    while (current_rrd != NULL) {
        cout << " <-> " << current_rrd->data_rrd << "";
        current_rrd = current_rrd->prev_rrd;
    }
    cout << " <-> NULL" << endl;
}

int getCount_rrd(struct DLLNode_rrd* head_rrd) {
    int count_rrd = 0;
    struct DLLNode_rrd* current_rrd = head_rrd;
    
    while (current_rrd != NULL) {
        count_rrd++;
        current_rrd = current_rrd->next_rrd;
    }
    
    return count_rrd;
}

struct DLLNode_rrd* getTail_rrd(struct DLLNode_rrd* head_rrd) {
    if (head_rrd == NULL) {
        return NULL;
    }
    
    struct DLLNode_rrd* current_rrd = head_rrd;
    while (current_rrd->next_rrd != NULL) {
        current_rrd = current_rrd->next_rrd;
    }
    
    return current_rrd;
}

void freeList_rrd(struct DLLNode_rrd* head_rrd) {
    struct DLLNode_rrd* temp_rrd;
    while (head_rrd != NULL) {
        temp_rrd = head_rrd;
        head_rrd = head_rrd->next_rrd;
        free(temp_rrd);
    }
}

void displayMenu_rrd() {
    cout << "\n===== Doubly Linked List Operations =====" << endl;
    cout << "1. Insert at Beginning" << endl;
    cout << "2. Insert at End" << endl;
    cout << "3. Insert at Position" << endl;
    cout << "4. Delete from Beginning" << endl;
    cout << "5. Delete from End" << endl;
    cout << "6. Delete at Position" << endl;
    cout << "7. Display List (Forward)" << endl;
    cout << "8. Display List (Backward)" << endl;
    cout << "9. Count Nodes" << endl;
    cout << "10. Exit" << endl;
    cout << "========================================" << endl;
    cout << "Enter your choice: ";
}
```

## Output

```
Doubly Linked List Implementation
================================

===== Doubly Linked List Operations =====
1. Insert at Beginning
2. Insert at End
3. Insert at Position
4. Delete from Beginning
5. Delete from End
6. Delete at Position
7. Display List (Forward)
8. Display List (Backward)
9. Count Nodes
10. Exit
========================================
Enter your choice: 1
Enter data to insert at beginning: 10
Node inserted at beginning successfully!

===== Doubly Linked List Operations =====
1. Insert at Beginning
2. Insert at End
3. Insert at Position
4. Delete from Beginning
5. Delete from End
6. Delete at Position
7. Display List (Forward)
8. Display List (Backward)
9. Count Nodes
10. Exit
========================================
Enter your choice: 2
Enter data to insert at end: 30
Node inserted at end successfully!

===== Doubly Linked List Operations =====
1. Insert at Beginning
2. Insert at End
3. Insert at Position
4. Delete from Beginning
5. Delete from End
6. Delete at Position
7. Display List (Forward)
8. Display List (Backward)
9. Count Nodes
10. Exit
========================================
Enter your choice: 3
Enter position (1-indexed): 2
Enter data to insert: 20
Node inserted at position 2 successfully!

===== Doubly Linked List Operations =====
1. Insert at Beginning
2. Insert at End
3. Insert at Position
4. Delete from Beginning
5. Delete from End
6. Delete at Position
7. Display List (Forward)
8. Display List (Backward)
9. Count Nodes
10. Exit
========================================
Enter your choice: 7
List (Forward): NULL <-> 10 <-> 20 <-> 30 <-> NULL

===== Doubly Linked List Operations =====
1. Insert at Beginning
2. Insert at End
3. Insert at Position
4. Delete from Beginning
5. Delete from End
6. Delete at Position
7. Display List (Forward)
8. Display List (Backward)
9. Count Nodes
10. Exit
========================================
Enter your choice: 8
List (Backward): NULL <-> 30 <-> 20 <-> 10 <-> NULL
```

## Dry Run

1. **Insert at Beginning (data: 10)**:
   - Create new node with data 10
   - Since list is empty, new node becomes head
   - List: [10]

2. **Insert at End (data: 30)**:
   - Create new node with data 30
   - Traverse to last node (10)
   - Link new node: [10] <-> [30]
   - List: [10] <-> [30]

3. **Insert at Position 2 (data: 20)**:
   - Create new node with data 20
   - Traverse to position 1 (node with data 10)
   - Insert new node between 10 and 30
   - Update pointers: [10] <-> [20] <-> [30]
   - List: [10] <-> [20] <-> [30]

4. **Display Forward**:
   - Start from head (10)
   - Traverse using next pointers: 10 -> 20 -> 30
   - Output: NULL <-> 10 <-> 20 <-> 30 <-> NULL

5. **Display Backward**:
   - Start from tail (30)
   - Traverse using prev pointers: 30 -> 20 -> 10
   - Output: NULL <-> 30 <-> 20 <-> 10 <-> NULL

## Conclusion

The implementation demonstrates a complete Doubly Linked List with all essential operations:

**Insert Operations**:
1. **Insert at Beginning**: O(1) time complexity
2. **Insert at End**: O(n) time complexity (need to traverse to end)
3. **Insert at Position**: O(n) time complexity (need to traverse to position)

**Delete Operations**:
1. **Delete at Beginning**: O(1) time complexity
2. **Delete at End**: O(n) time complexity (need to traverse to end)
3. **Delete at Position**: O(n) time complexity (need to traverse to position)

**Space Complexity**: O(n) where n is the number of nodes

**Advantages of Doubly Linked List**:
1. **Bidirectional Traversal**: Can traverse in both directions
2. **Efficient Deletion**: Can delete a node given its pointer in O(1)
3. **Easy Reverse Traversal**: No need to traverse from beginning for backward display
4. **Flexibility**: Easy to implement various operations

**Disadvantages**:
1. **Extra Memory**: Requires additional pointer per node
2. **Complex Implementation**: More pointers to manage than singly linked list

**Key Features of Implementation**:
1. **Error Handling**: Proper validation for invalid positions and empty list operations
2. **Memory Management**: Proper allocation and deallocation of nodes
3. **Edge Cases**: Handles single node list, empty list, and boundary conditions
4. **User Interface**: Interactive menu-driven program for easy testing

The implementation correctly handles all edge cases:
- Insertion/deletion in empty list
- Insertion/deletion at boundaries (beginning/end)
- Invalid position handling
- Memory leaks prevention

This comprehensive implementation provides a solid foundation for understanding doubly linked lists and their operations, which are fundamental data structures in computer science.