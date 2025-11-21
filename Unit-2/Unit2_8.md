# Unit II Assignment 8: Bubble Sort using Doubly Linked List

Implementation of Bubble Sort algorithm using Doubly Linked List to sort data elements in ascending order.

## Problem Statement

Implement Bubble Sort using Doubly Linked List to sort a list of elements in ascending order.

## Pseudo Code

### Doubly Linked List Node Structure
```
Structure DLLNode:
    data: integer
    next: pointer to DLLNode
    prev: pointer to DLLNode
```

### Bubble Sort Algorithm
```
Algorithm BubbleSortDLL(head):
    If head is NULL or head.next is NULL:
        Return head
    swapped = true
    While swapped:
        swapped = false
        current = head
        While current.next != NULL:
            If current.data > current.next.data:
                Swap current.data and current.next.data
                swapped = true
            current = current.next
    Return head
```

### Swap Adjacent Nodes (Alternative Approach)
```
Algorithm SwapNodes(current, next_node):
    If current.prev != NULL:
        current.prev.next = next_node
    Else:
        head = next_node
    If next_node.next != NULL:
        next_node.next.prev = current
    current.next = next_node.next
    next_node.prev = current.prev
    current.prev = next_node
    next_node.next = current
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
void insertAtEnd_rrd(struct DLLNode_rrd** head_rrd, int data_rrd);
void displayList_rrd(struct DLLNode_rrd* head_rrd);
void displayListReverse_rrd(struct DLLNode_rrd* tail_rrd);
int getCount_rrd(struct DLLNode_rrd* head_rrd);
struct DLLNode_rrd* bubbleSortDLL_rrd(struct DLLNode_rrd* head_rrd);
void swapData_rrd(struct DLLNode_rrd* a_rrd, struct DLLNode_rrd* b_rrd);
struct DLLNode_rrd* getTail_rrd(struct DLLNode_rrd* head_rrd);
void freeList_rrd(struct DLLNode_rrd* head_rrd);

int main() {
    struct DLLNode_rrd* head_rrd = NULL;
    int n_rrd, data_rrd, i_rrd;
    
    cout << "Bubble Sort using Doubly Linked List" << endl;
    cout << "===================================" << endl;
    
    cout << "Enter number of elements: ";
    cin >> n_rrd;
    
    cout << "Enter " << n_rrd << " elements:" << endl;
    for (i_rrd = 0; i_rrd < n_rrd; i_rrd++) {
        cin >> data_rrd;
        insertAtEnd_rrd(&head_rrd, data_rrd);
    }
    
    cout << "\nOriginal list: ";
    displayList_rrd(head_rrd);
    
    head_rrd = bubbleSortDLL_rrd(head_rrd);
    
    cout << "Sorted list: ";
    displayList_rrd(head_rrd);
    
    cout << "Sorted list (reverse): ";
    struct DLLNode_rrd* tail_rrd = getTail_rrd(head_rrd);
    displayListReverse_rrd(tail_rrd);
    

    freeList_rrd(head_rrd);
    
    return 0;
}

struct DLLNode_rrd* createNode_rrd(int data_rrd) {
    struct DLLNode_rrd* newNode_rrd = (struct DLLNode_rrd*)malloc(sizeof(struct DLLNode_rrd));
    newNode_rrd->data_rrd = data_rrd;
    newNode_rrd->next_rrd = NULL;
    newNode_rrd->prev_rrd = NULL;
    return newNode_rrd;
}

void insertAtEnd_rrd(struct DLLNode_rrd** head_rrd, int data_rrd) {
    struct DLLNode_rrd* newNode_rrd = createNode_rrd(data_rrd);
    

    if (*head_rrd == NULL) {
        *head_rrd = newNode_rrd;
        return;
    }
    

    struct DLLNode_rrd* current_rrd = *head_rrd;
    while (current_rrd->next_rrd != NULL) {
        current_rrd = current_rrd->next_rrd;
    }
    

    current_rrd->next_rrd = newNode_rrd;
    newNode_rrd->prev_rrd = current_rrd;
}

void displayList_rrd(struct DLLNode_rrd* head_rrd) {
    if (head_rrd == NULL) {
        cout << "List is empty" << endl;
        return;
    }
    
    struct DLLNode_rrd* current_rrd = head_rrd;
    while (current_rrd != NULL) {
        cout << "" << current_rrd->data_rrd << " ";
        current_rrd = current_rrd->next_rrd;
    }
    cout << "" << endl;
}

void displayListReverse_rrd(struct DLLNode_rrd* tail_rrd) {
    if (tail_rrd == NULL) {
        cout << "List is empty" << endl;
        return;
    }
    
    struct DLLNode_rrd* current_rrd = tail_rrd;
    while (current_rrd != NULL) {
        cout << "" << current_rrd->data_rrd << " ";
        current_rrd = current_rrd->prev_rrd;
    }
    cout << "" << endl;
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

void swapData_rrd(struct DLLNode_rrd* a_rrd, struct DLLNode_rrd* b_rrd) {
    int temp_rrd = a_rrd->data_rrd;
    a_rrd->data_rrd = b_rrd->data_rrd;
    b_rrd->data_rrd = temp_rrd;
}

struct DLLNode_rrd* bubbleSortDLL_rrd(struct DLLNode_rrd* head_rrd) {

    if (head_rrd == NULL || head_rrd->next_rrd == NULL) {
        return head_rrd;
    }
    
    int swapped_rrd;
    struct DLLNode_rrd* current_rrd;
    struct DLLNode_rrd* last_rrd = NULL;
    
    do {
        swapped_rrd = 0;
        current_rrd = head_rrd;
        

        while (current_rrd->next_rrd != last_rrd) {

            if (current_rrd->data_rrd > current_rrd->next_rrd->data_rrd) {
                swapData_rrd(current_rrd, current_rrd->next_rrd);
                swapped_rrd = 1;
            }
            current_rrd = current_rrd->next_rrd;
        }
        

        last_rrd = current_rrd;
    } while (swapped_rrd);
    
    return head_rrd;
}

void freeList_rrd(struct DLLNode_rrd* head_rrd) {
    struct DLLNode_rrd* temp_rrd;
    while (head_rrd != NULL) {
        temp_rrd = head_rrd;
        head_rrd = head_rrd->next_rrd;
        free(temp_rrd);
    }
}
```

## Output

```
Bubble Sort using Doubly Linked List
===================================
Enter number of elements: 7
Enter 7 elements:
64 34 25 12 22 11 90

Original list: 64 34 25 12 22 11 90
Sorted list: 11 12 22 25 34 64 90
Sorted list (reverse): 90 64 34 25 22 12 11
```

## Dry Run

1. **Initial List**: [64] ↔ [34] ↔ [25] ↔ [12] ↔ [22] ↔ [11] ↔ [90]

2. **Pass 1**:
   - Compare 64 and 34: Swap → [34] ↔ [64] ↔ [25] ↔ [12] ↔ [22] ↔ [11] ↔ [90]
   - Compare 64 and 25: Swap → [34] ↔ [25] ↔ [64] ↔ [12] ↔ [22] ↔ [11] ↔ [90]
   - Compare 64 and 12: Swap → [34] ↔ [25] ↔ [12] ↔ [64] ↔ [22] ↔ [11] ↔ [90]
   - Compare 64 and 22: Swap → [34] ↔ [25] ↔ [12] ↔ [22] ↔ [64] ↔ [11] ↔ [90]
   - Compare 64 and 11: Swap → [34] ↔ [25] ↔ [12] ↔ [22] ↔ [11] ↔ [64] ↔ [90]
   - Compare 64 and 90: No swap
   - After Pass 1: Largest element (90) is at the end

3. **Pass 2**:
   - Compare 34 and 25: Swap → [25] ↔ [34] ↔ [12] ↔ [22] ↔ [11] ↔ [64] ↔ [90]
   - Compare 34 and 12: Swap → [25] ↔ [12] ↔ [34] ↔ [22] ↔ [11] ↔ [64] ↔ [90]
   - Compare 34 and 22: Swap → [25] ↔ [12] ↔ [22] ↔ [34] ↔ [11] ↔ [64] ↔ [90]
   - Compare 34 and 11: Swap → [25] ↔ [12] ↔ [22] ↔ [11] ↔ [34] ↔ [64] ↔ [90]
   - Compare 34 and 64: No swap
   - After Pass 2: Second largest element (64) is in correct position

4. **Continue until sorted**:
   - Eventually: [11] ↔ [12] ↔ [22] ↔ [25] ↔ [34] ↔ [64] ↔ [90]

## Conclusion

The implementation demonstrates Bubble Sort using Doubly Linked List with the following key features:

1. **Bidirectional Traversal**: Can traverse in both forward and backward directions
2. **In-place Sorting**: Sorts by swapping data rather than rearranging nodes
3. **Adaptive**: Optimized to stop early if the list becomes sorted
4. **Stable**: Maintains relative order of equal elements

**Time Complexities**:
- Best Case: O(n) when list is already sorted
- Average Case: O(n²)
- Worst Case: O(n²) when list is reverse sorted

**Space Complexity**: O(1) as it sorts in-place

**Advantages of Doubly Linked List for Bubble Sort**:
1. **Easy Navigation**: Can move in both directions
2. **Efficient Swapping**: Adjacent nodes can be swapped by changing pointers
3. **Reverse Traversal**: Can display list in reverse order without additional processing
4. **Flexibility**: Easy to implement other operations like insertion/deletion

**Comparison with Singly Linked List**:
- Doubly linked list requires more memory (extra pointer per node)
- But provides more flexibility in traversal and operations
- For bubble sort, the difference is minimal since we're swapping data, not nodes

The implementation correctly handles edge cases:
- Empty list
- Single element list
- Already sorted list
- Reverse sorted list

The bidirectional nature of the doubly linked list is demonstrated by the reverse display function, which traverses from tail to head using the previous pointers.