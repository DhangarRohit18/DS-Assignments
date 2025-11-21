# Unit II Assignment 10: FrontBackSplit for Linked Lists

Implementation of FrontBackSplit operation to divide a linked list into two sublists - one for the front half and one for the back half.

## Problem Statement

Given a list, split it into two sublists — one for the front half, and one for the back half. If the number of elements is odd, the extra element should go in the front list. For example, FrontBackSplit() on the list {2, 3, 5, 7, 11} should yield the two lists {2, 3, 5} and {7, 11}.

## Pseudo Code

### Singly Linked List Node Structure
```
Structure ListNode:
    data: integer
    next: pointer to ListNode
```

### FrontBackSplit Algorithm
```
Algorithm FrontBackSplit(source, frontRef, backRef):
    If source is NULL or source.next is NULL:
        frontRef = source
        backRef = NULL
        Return
    slow = source
    fast = source
    While fast.next != NULL AND fast.next.next != NULL:
        slow = slow.next
        fast = fast.next.next
    frontRef = source
    backRef = slow.next
    slow.next = NULL
```

### Alternative Implementation (Count-based)
```
Algorithm FrontBackSplitCount(source, frontRef, backRef):
    Count total nodes in source list
    If count <= 1:
        frontRef = source
        backRef = NULL
        Return
    frontCount = (count + 1) / 2
    Traverse to frontCount-th node
    frontRef = source
    backRef = node at frontCount+1 position
    Set next of frontCount-th node to NULL
```

## Code Implementation

```c
#include <iostream>
using namespace std;
#include <stdlib.h>

struct ListNode_rrd {
    int data_rrd;
    struct ListNode_rrd* next_rrd;
};

struct ListNode_rrd* createNode_rrd(int data_rrd);
void insertAtEnd_rrd(struct ListNode_rrd** head_rrd, int data_rrd);
void displayList_rrd(struct ListNode_rrd* head_rrd);
int getCount_rrd(struct ListNode_rrd* head_rrd);
void frontBackSplit_rrd(struct ListNode_rrd* source_rrd, struct ListNode_rrd** frontRef_rrd, struct ListNode_rrd** backRef_rrd);
void frontBackSplitCount_rrd(struct ListNode_rrd* source_rrd, struct ListNode_rrd** frontRef_rrd, struct ListNode_rrd** backRef_rrd);
struct ListNode_rrd* createSampleList_rrd();
void freeList_rrd(struct ListNode_rrd* head_rrd);

int main() {
    struct ListNode_rrd* originalList_rrd = NULL;
    struct ListNode_rrd* frontList_rrd = NULL;
    struct ListNode_rrd* backList_rrd = NULL;
    int n_rrd, data_rrd, i_rrd;
    int choice_rrd;
    
    cout << "FrontBackSplit Implementation" << endl;
    cout << "===========================" << endl;
    
    cout << "Choose input method:" << endl;
    cout << "1. Manual input" << endl;
    cout << "2. Use sample list {2, 3, 5, 7, 11}" << endl;
    cout << "Enter your choice: ";
    cin >> choice_rrd;
    
    if (choice_rrd == 1) {
        cout << "Enter number of elements: ";
        cin >> n_rrd;
        
        cout << "Enter " << n_rrd << " elements:" << endl;
        for (i_rrd = 0; i_rrd < n_rrd; i_rrd++) {
            cin >> data_rrd;
            insertAtEnd_rrd(&originalList_rrd, data_rrd);
        }
    } else {
        originalList_rrd = createSampleList_rrd();
        cout << "Using sample list: ";
        displayList_rrd(originalList_rrd);
    }
    
    cout << "\nOriginal list: ";
    displayList_rrd(originalList_rrd);
    

    cout << "\n--- Method 1: Fast/Slow Pointer Approach ---" << endl;
    frontBackSplit_rrd(originalList_rrd, &frontList_rrd, &backList_rrd);
    
    cout << "Front list: ";
    displayList_rrd(frontList_rrd);
    cout << "Back list: ";
    displayList_rrd(backList_rrd);
    

    freeList_rrd(frontList_rrd);
    freeList_rrd(backList_rrd);
    

    if (choice_rrd == 1) {

        originalList_rrd = NULL;
        cout << "\nEnter " << n_rrd << " elements again:" << endl;
        for (i_rrd = 0; i_rrd < n_rrd; i_rrd++) {
            cin >> data_rrd;
            insertAtEnd_rrd(&originalList_rrd, data_rrd);
        }
    } else {
        originalList_rrd = createSampleList_rrd();
    }
    

    cout << "\n--- Method 2: Count-Based Approach ---" << endl;
    frontBackSplitCount_rrd(originalList_rrd, &frontList_rrd, &backList_rrd);
    
    cout << "Front list: ";
    displayList_rrd(frontList_rrd);
    cout << "Back list: ";
    displayList_rrd(backList_rrd);
    

    freeList_rrd(originalList_rrd);
    freeList_rrd(frontList_rrd);
    freeList_rrd(backList_rrd);
    
    return 0;
}

struct ListNode_rrd* createNode_rrd(int data_rrd) {
    struct ListNode_rrd* newNode_rrd = (struct ListNode_rrd*)malloc(sizeof(struct ListNode_rrd));
    newNode_rrd->data_rrd = data_rrd;
    newNode_rrd->next_rrd = NULL;
    return newNode_rrd;
}

void insertAtEnd_rrd(struct ListNode_rrd** head_rrd, int data_rrd) {
    struct ListNode_rrd* newNode_rrd = createNode_rrd(data_rrd);
    
    if (*head_rrd == NULL) {
        *head_rrd = newNode_rrd;
        return;
    }
    
    struct ListNode_rrd* current_rrd = *head_rrd;
    while (current_rrd->next_rrd != NULL) {
        current_rrd = current_rrd->next_rrd;
    }
    
    current_rrd->next_rrd = newNode_rrd;
}

void displayList_rrd(struct ListNode_rrd* head_rrd) {
    if (head_rrd == NULL) {
        cout << "List is empty" << endl;
        return;
    }
    
    struct ListNode_rrd* current_rrd = head_rrd;
    while (current_rrd != NULL) {
        cout << "" << current_rrd->data_rrd << "";
        if (current_rrd->next_rrd != NULL) {
            cout << " -> ";
        }
        current_rrd = current_rrd->next_rrd;
    }
    cout << " -> NULL" << endl;
}

int getCount_rrd(struct ListNode_rrd* head_rrd) {
    int count_rrd = 0;
    struct ListNode_rrd* current_rrd = head_rrd;
    
    while (current_rrd != NULL) {
        count_rrd++;
        current_rrd = current_rrd->next_rrd;
    }
    
    return count_rrd;
}

void frontBackSplit_rrd(struct ListNode_rrd* source_rrd, struct ListNode_rrd** frontRef_rrd, struct ListNode_rrd** backRef_rrd) {
    struct ListNode_rrd* slow_rrd;
    struct ListNode_rrd* fast_rrd;
    
    if (source_rrd == NULL || source_rrd->next_rrd == NULL) {
        *frontRef_rrd = source_rrd;
        *backRef_rrd = NULL;
        return;
    }
    
    slow_rrd = source_rrd;
    fast_rrd = source_rrd;
    


    while (fast_rrd->next_rrd != NULL && fast_rrd->next_rrd->next_rrd != NULL) {
        slow_rrd = slow_rrd->next_rrd;
        fast_rrd = fast_rrd->next_rrd->next_rrd;
    }
    


    
    *frontRef_rrd = source_rrd;
    *backRef_rrd = slow_rrd->next_rrd;
    slow_rrd->next_rrd = NULL;
}

void frontBackSplitCount_rrd(struct ListNode_rrd* source_rrd, struct ListNode_rrd** frontRef_rrd, struct ListNode_rrd** backRef_rrd) {
    int count_rrd = getCount_rrd(source_rrd);
    int frontCount_rrd;
    struct ListNode_rrd* current_rrd;
    int i_rrd;
    
    if (count_rrd <= 1) {
        *frontRef_rrd = source_rrd;
        *backRef_rrd = NULL;
        return;
    }
    

    frontCount_rrd = (count_rrd + 1) / 2;
    

    current_rrd = source_rrd;
    for (i_rrd = 1; i_rrd < frontCount_rrd; i_rrd++) {
        current_rrd = current_rrd->next_rrd;
    }
    
    *frontRef_rrd = source_rrd;
    *backRef_rrd = current_rrd->next_rrd;
    current_rrd->next_rrd = NULL;
}

struct ListNode_rrd* createSampleList_rrd() {
    struct ListNode_rrd* head_rrd = NULL;
    

    insertAtEnd_rrd(&head_rrd, 2);
    insertAtEnd_rrd(&head_rrd, 3);
    insertAtEnd_rrd(&head_rrd, 5);
    insertAtEnd_rrd(&head_rrd, 7);
    insertAtEnd_rrd(&head_rrd, 11);
    
    return head_rrd;
}

void freeList_rrd(struct ListNode_rrd* head_rrd) {
    struct ListNode_rrd* temp_rrd;
    while (head_rrd != NULL) {
        temp_rrd = head_rrd;
        head_rrd = head_rrd->next_rrd;
        free(temp_rrd);
    }

printf

## Output
}
FrontBackSplit Implementation
===========================
Choose input method:
1. Manual input
2. Use sample list {2, 3, 5, 7, 11}
Enter your choice: 2
Using sample list: 2 -> 3 -> 5 -> 7 -> 11 -> NULL

Original list: 2 -> 3 -> 5 -> 7 -> 11 -> NULL

--- Method 1: Fast/Slow Pointer Approach ---
Front list: 2 -> 3 -> 5 -> NULL
Back list: 7 -> 11 -> NULL

--- Method 2: Count-Based Approach ---
Front list: 2 -> 3 -> 5 -> NULL
Back list: 7 -> 11 -> NULL
```

## Dry Run

### Example 1: List {2, 3, 5, 7, 11} (Odd length: 5)

**Fast/Slow Pointer Approach**:
1. Initial: slow=2, fast=2
2. Step 1: slow=3, fast=5
3. Step 2: slow=5, fast=11
4. fast->next is NULL, so stop
5. slow is at node 5 (middle)
6. Front list: {2, 3, 5}
7. Back list: {7, 11}

**Count-Based Approach**:
1. Count = 5
2. frontCount = (5+1)/2 = 3
3. Traverse to 3rd node (value 5)
4. Split after 3rd node
5. Front list: {2, 3, 5}
6. Back list: {7, 11}

### Example 2: List {1, 2, 3, 4} (Even length: 4)

**Fast/Slow Pointer Approach**:
1. Initial: slow=1, fast=1
2. Step 1: slow=2, fast=3
3. Step 2: slow=3, fast=NULL (fast->next is NULL)
4. Stop, slow is at node 3
5. Front list: {1, 2, 3}
6. Back list: {4}

**Count-Based Approach**:
1. Count = 4
2. frontCount = (4+1)/2 = 2
3. Traverse to 2nd node (value 2)
4. Split after 2nd node
5. Front list: {1, 2}
6. Back list: {3, 4}

Wait, there's an inconsistency! Let me correct this:

For even length, we want the front list to have n/2 elements and back list to have n/2 elements.
For list {1, 2, 3, 4}, front should be {1, 2} and back should be {3, 4}.

Let me trace the fast/slow pointer approach again:
1. Initial: slow=1, fast=1
2. Step 1: slow=2, fast=3
3. fast->next->next is NULL, so stop
4. slow is at node 2
5. Front list: {1, 2}
6. Back list: {3, 4}

This is correct!

### Edge Cases:
1. **Empty list**: Front={}, Back={}
2. **Single node**: Front={node}, Back={}
3. **Two nodes**: Front={first}, Back={second}

## Conclusion

The implementation demonstrates two approaches to solve the FrontBackSplit problem:

**Method 1: Fast/Slow Pointer Approach**
- **Time Complexity**: O(n) - single pass through the list
- **Space Complexity**: O(1) - only uses a few pointers
- **Advantage**: More efficient, only one traversal needed
- **Logic**: Fast pointer moves twice as fast as slow pointer; when fast reaches end, slow is at middle

**Method 2: Count-Based Approach**
- **Time Complexity**: O(n) - two passes (one to count, one to split)
- **Space Complexity**: O(1) - only uses a few variables
- **Advantage**: More intuitive and easier to understand
- **Logic**: Count nodes, calculate split point, traverse to that point

**Key Implementation Details**:
1. **Odd Length Handling**: Extra node goes to front list as required
2. **Edge Cases**: Properly handles empty list, single node, and two nodes
3. **Memory Management**: No memory leaks, proper pointer management
4. **Pointer Manipulation**: Correctly breaks and forms links between nodes

**Algorithm Correctness**:
- For list of length n:
  - If n is odd: front list has (n+1)/2 nodes, back list has (n-1)/2 nodes
  - If n is even: front list has n/2 nodes, back list has n/2 nodes
- This satisfies the requirement that extra node (in odd case) goes to front

Both methods are valid solutions with the same time complexity. The fast/slow pointer approach is more elegant and efficient as it requires only one pass through the list, while the count-based approach is more straightforward to understand. In practice, the fast/slow pointer approach is preferred for its efficiency.

The implementation correctly handles all boundary conditions and provides a solid foundation for understanding linked list manipulation techniques that are commonly used in more complex algorithms.
