# Unit III Assignment 3: Multiple Stack Implementation using Array

Implementation of multiple stacks (more than two) using a single array.

## Problem Statement

Write a program to implement multiple stack i.e more than two stack using array and perform following operations on it:
A. Push
B. Pop
C. Stack Overflow
D. Stack Underflow
E. Display

## Pseudo Code

### Multiple Stack Structure
```
Structure MultipleStack:
    array: fixed size array
    tops: array to store top indices for each stack
    size: total size of array
    numStacks: number of stacks
    stackSize: size allocated to each stack
```

### Push Operation
```
Algorithm Push(stackNum, value):
    If stackNum is invalid:
        Return error
    If tops[stackNum] >= (stackNum+1) * stackSize - 1:
        Return "Stack Overflow"
    tops[stackNum]++
    array[tops[stackNum]] = value
```

### Pop Operation
```
Algorithm Pop(stackNum):
    If stackNum is invalid:
        Return error
    If tops[stackNum] < stackNum * stackSize:
        Return "Stack Underflow"
    value = array[tops[stackNum]]
    tops[stackNum]--
    Return value
```

### Display Stack
```
Algorithm DisplayStack(stackNum):
    If stackNum is invalid:
        Return error
    For i from tops[stackNum] down to stackNum * stackSize:
        Print array[i]
```

## Code Implementation

```c
#include <iostream>
using namespace std;
#include <stdlib.h>
#define MAX_SIZE 100
#define MAX_STACKS 5
struct MultipleStack_rrd {
    int array_rrd[MAX_SIZE];
    int tops_rrd[MAX_STACKS];
    int size_rrd;
    int numStacks_rrd;
    int stackSize_rrd;
};

struct MultipleStack_rrd* createMultipleStack_rrd(int numStacks_rrd);
int isEmpty_rrd(struct MultipleStack_rrd* mStack_rrd, int stackNum_rrd);
int isFull_rrd(struct MultipleStack_rrd* mStack_rrd, int stackNum_rrd);
int push_rrd(struct MultipleStack_rrd* mStack_rrd, int stackNum_rrd, int value_rrd);
int pop_rrd(struct MultipleStack_rrd* mStack_rrd, int stackNum_rrd, int* poppedValue_rrd);
int peek_rrd(struct MultipleStack_rrd* mStack_rrd, int stackNum_rrd, int* peekedValue_rrd);
void displayStack_rrd(struct MultipleStack_rrd* mStack_rrd, int stackNum_rrd);
void displayAllStacks_rrd(struct MultipleStack_rrd* mStack_rrd);
int getStackSize_rrd(struct MultipleStack_rrd* mStack_rrd, int stackNum_rrd);
int areAllStacksEmpty_rrd(struct MultipleStack_rrd* mStack_rrd);
void clearStack_rrd(struct MultipleStack_rrd* mStack_rrd, int stackNum_rrd);
void clearAllStacks_rrd(struct MultipleStack_rrd* mStack_rrd);
void freeMultipleStack_rrd(struct MultipleStack_rrd* mStack_rrd);
void demonstrateOperations_rrd(struct MultipleStack_rrd* mStack_rrd);
void displayMenu_rrd();
struct MultipleStack_rrd* createMultipleStack_rrd(int numStacks_rrd) {
    if (numStacks_rrd <= 0 || numStacks_rrd > MAX_STACKS)
{
        cout << "Invalid number of stacks! Must be between 1 and " << MAX_STACKS << "." << endl;
        return NULL;
    }

    struct MultipleStack_rrd* mStack_rrd = (struct MultipleStack_rrd*)malloc(sizeof(struct MultipleStack_rrd));
    mStack_rrd->numStacks_rrd = numStacks_rrd;
    mStack_rrd->size_rrd = MAX_SIZE;
    mStack_rrd->stackSize_rrd = MAX_SIZE / numStacks_rrd;
    for (int i_rrd = 0; i_rrd < numStacks_rrd; i_rrd++)
{
        mStack_rrd->tops_rrd[i_rrd] = (i_rrd * mStack_rrd->stackSize_rrd) - 1;
    }

    cout << "Multiple stack created with " << numStacks_rrd, mStack_rrd->stackSize_rrd << " stacks, each of size %d" << endl;
    return mStack_rrd;
}

int isEmpty_rrd(struct MultipleStack_rrd* mStack_rrd, int stackNum_rrd) {
    if (stackNum_rrd < 0 || stackNum_rrd >= mStack_rrd->numStacks_rrd)
{
        cout << "Invalid stack number!" << endl;
        return -1;
    }
    return mStack_rrd->tops_rrd[stackNum_rrd] < (stackNum_rrd * mStack_rrd->stackSize_rrd);
}

int isFull_rrd(struct MultipleStack_rrd* mStack_rrd, int stackNum_rrd) {
    if (stackNum_rrd < 0 || stackNum_rrd >= mStack_rrd->numStacks_rrd)
{
        cout << "Invalid stack number!" << endl;
        return -1;
    }
    return mStack_rrd->tops_rrd[stackNum_rrd] >= ((stackNum_rrd + 1) * mStack_rrd->stackSize_rrd) - 1;
}

int push_rrd(struct MultipleStack_rrd* mStack_rrd, int stackNum_rrd, int value_rrd) {
    if (stackNum_rrd < 0 || stackNum_rrd >= mStack_rrd->numStacks_rrd)
{
        cout << "Invalid stack number! Please use stack number between 0 and " << mStack_rrd->numStacks_rrd - 1 << "." << endl;
        return 0;
    }

    if (isFull_rrd(mStack_rrd, stackNum_rrd))
{
        cout << "Stack Overflow! Stack " << stackNum_rrd << " is full." << endl;
        return 0;
    }

    mStack_rrd->tops_rrd[stackNum_rrd]++;
    mStack_rrd->array_rrd[mStack_rrd->tops_rrd[stackNum_rrd]] = value_rrd;
    cout << "Value " << value_rrd, stackNum_rrd << " pushed to stack %d successfully!" << endl;
    return 1;
}

int pop_rrd(struct MultipleStack_rrd* mStack_rrd, int stackNum_rrd, int* poppedValue_rrd) {
    if (stackNum_rrd < 0 || stackNum_rrd >= mStack_rrd->numStacks_rrd)
{
        cout << "Invalid stack number! Please use stack number between 0 and " << mStack_rrd->numStacks_rrd - 1 << "." << endl;
        return 0;
    }

    if (isEmpty_rrd(mStack_rrd, stackNum_rrd))
{
        cout << "Stack Underflow! Stack " << stackNum_rrd << " is empty." << endl;
        return 0;
    }

    *poppedValue_rrd = mStack_rrd->array_rrd[mStack_rrd->tops_rrd[stackNum_rrd]];
    mStack_rrd->tops_rrd[stackNum_rrd]--;
    cout << "Value " << *poppedValue_rrd, stackNum_rrd << " popped from stack %d successfully!" << endl;
    return 1;
}

int peek_rrd(struct MultipleStack_rrd* mStack_rrd, int stackNum_rrd, int* peekedValue_rrd) {
    if (stackNum_rrd < 0 || stackNum_rrd >= mStack_rrd->numStacks_rrd)
{
        cout << "Invalid stack number! Please use stack number between 0 and " << mStack_rrd->numStacks_rrd - 1 << "." << endl;
        return 0;
    }

    if (isEmpty_rrd(mStack_rrd, stackNum_rrd))
{
        cout << "Stack " << stackNum_rrd << " is empty!" << endl;
        return 0;
    }

    *peekedValue_rrd = mStack_rrd->array_rrd[mStack_rrd->tops_rrd[stackNum_rrd]];
    return 1;
}

void displayStack_rrd(struct MultipleStack_rrd* mStack_rrd, int stackNum_rrd) {
    if (stackNum_rrd < 0 || stackNum_rrd >= mStack_rrd->numStacks_rrd)
{
        cout << "Invalid stack number! Please use stack number between 0 and " << mStack_rrd->numStacks_rrd - 1 << "." << endl;
        return;
    }

    if (isEmpty_rrd(mStack_rrd, stackNum_rrd))
{
        cout << "Stack " << stackNum_rrd << " is empty!" << endl;
        return;
    }

    cout << "Stack " << stackNum_rrd << " contents (top to bottom): ";
    for (int i_rrd = mStack_rrd->tops_rrd[stackNum_rrd]; i_rrd >= (stackNum_rrd * mStack_rrd->stackSize_rrd); i_rrd--)
{
        cout << "" << mStack_rrd->array_rrd[i_rrd] << " ";
    }

    cout << "" << endl;
}

void displayAllStacks_rrd(struct MultipleStack_rrd* mStack_rrd) {
    cout << "\n===== All Stacks =====" << endl;
    for (int i_rrd = 0; i_rrd < mStack_rrd->numStacks_rrd; i_rrd++)
{
        cout << "Stack " << i_rrd << ": ";
        if (isEmpty_rrd(mStack_rrd, i_rrd))
{
            cout << "Empty" << endl;
        } else
{

            for (int j_rrd = mStack_rrd->tops_rrd[i_rrd]; j_rrd >= (i_rrd * mStack_rrd->stackSize_rrd); j_rrd--)
{
                cout << "" << mStack_rrd->array_rrd[j_rrd] << " ";
            }

            cout << "" << endl;
        }
    }

    cout << "=====================" << endl;
}

int getStackSize_rrd(struct MultipleStack_rrd* mStack_rrd, int stackNum_rrd) {
    if (stackNum_rrd < 0 || stackNum_rrd >= mStack_rrd->numStacks_rrd)
{
        cout << "Invalid stack number!" << endl;
        return -1;
    }
    return mStack_rrd->tops_rrd[stackNum_rrd] - (stackNum_rrd * mStack_rrd->stackSize_rrd) + 1;
}

int areAllStacksEmpty_rrd(struct MultipleStack_rrd* mStack_rrd) {
    for (int i_rrd = 0; i_rrd < mStack_rrd->numStacks_rrd; i_rrd++)
{
        if (!isEmpty_rrd(mStack_rrd, i_rrd))
{
            return 0;
        }
    }
    return 1;
}

void clearStack_rrd(struct MultipleStack_rrd* mStack_rrd, int stackNum_rrd) {
    if (stackNum_rrd < 0 || stackNum_rrd >= mStack_rrd->numStacks_rrd)
{
        cout << "Invalid stack number!" << endl;
        return;
    }

    mStack_rrd->tops_rrd[stackNum_rrd] = (stackNum_rrd * mStack_rrd->stackSize_rrd) - 1;
    cout << "Stack " << stackNum_rrd << " cleared successfully!" << endl;
}

void clearAllStacks_rrd(struct MultipleStack_rrd* mStack_rrd) {
    for (int i_rrd = 0; i_rrd < mStack_rrd->numStacks_rrd; i_rrd++)
{
        clearStack_rrd(mStack_rrd, i_rrd);
    }

    cout << "All stacks cleared successfully!" << endl;
}

void freeMultipleStack_rrd(struct MultipleStack_rrd* mStack_rrd) {
    free(mStack_rrd);
}

void demonstrateOperations_rrd(struct MultipleStack_rrd* mStack_rrd) {
    cout << "\n===== Demonstration of Stack Operations =====" << endl;
    cout << "\n1. Push Operations:" << endl;
    push_rrd(mStack_rrd, 0, 10);
    push_rrd(mStack_rrd, 0, 20);
    push_rrd(mStack_rrd, 1, 30);
    push_rrd(mStack_rrd, 1, 40);
    push_rrd(mStack_rrd, 2, 50);
    cout << "\n2. Display Individual Stacks:" << endl;
    displayStack_rrd(mStack_rrd, 0);
    displayStack_rrd(mStack_rrd, 1);
    displayStack_rrd(mStack_rrd, 2);
    cout << "\n3. Display All Stacks:" << endl;
    displayAllStacks_rrd(mStack_rrd);
    cout << "\n4. Peek Operations:" << endl;
    int peekedValue_rrd;
    if (peek_rrd(mStack_rrd, 0, &peekedValue_rrd))
{
        cout << "Top of stack 0: " << peekedValue_rrd << "" << endl;
    }

    if (peek_rrd(mStack_rrd, 1, &peekedValue_rrd))
{
        cout << "Top of stack 1: " << peekedValue_rrd << "" << endl;
    }

    cout << "\n5. Pop Operations:" << endl;
    int poppedValue_rrd;
    pop_rrd(mStack_rrd, 0, &poppedValue_rrd);
    pop_rrd(mStack_rrd, 1, &poppedValue_rrd);
    cout << "\n6. Display After Pop Operations:" << endl;
    displayAllStacks_rrd(mStack_rrd);
    cout << "\n7. Stack Size Information:" << endl;
    for (int i_rrd = 0; i_rrd < mStack_rrd->numStacks_rrd; i_rrd++)
{
        int size_rrd = getStackSize_rrd(mStack_rrd, i_rrd);
        if (size_rrd >= 0)
{
            cout << "Size of stack " << i_rrd, size_rrd << ": %d" << endl;
        }
    }
}

void displayMenu_rrd() {
    cout << "\n===== Multiple Stack Operations =====" << endl;
    cout << "1. Push to Stack" << endl;
    cout << "2. Pop from Stack" << endl;
    cout << "3. Peek at Stack" << endl;
    cout << "4. Display Stack" << endl;
    cout << "5. Display All Stacks" << endl;
    cout << "6. Check if Stack is Empty" << endl;
    cout << "7. Check if Stack is Full" << endl;
    cout << "8. Get Stack Size" << endl;
    cout << "9. Clear Stack" << endl;
    cout << "10. Clear All Stacks" << endl;
    cout << "11. Demonstrate Operations" << endl;
    cout << "12. Exit" << endl;
    cout << "====================================" << endl;
    cout << "Enter your choice: ";
}

int main() {
    cout << "Welcome to Multiple Stack Implementation!" << endl;
    int numStacks_rrd;
    cout << "Enter the number of stacks to create (1-" << MAX_STACKS << "): ";
    cin >> numStacks_rrd;
    struct MultipleStack_rrd* mStack_rrd = createMultipleStack_rrd(numStacks_rrd);
    if (mStack_rrd == NULL)
{
        return 1;
    }

    int choice_rrd;
    while (1)
{
        displayMenu_rrd();
        cin >> choice_rrd;
        switch (choice_rrd)
{
{
                int stackNum_rrd, value_rrd;
                cout << "Enter stack number (0-" << mStack_rrd->numStacks_rrd - 1 << "): ";
                cin >> stackNum_rrd;
                cout << "Enter value to push: ";
                cin >> value_rrd;
                push_rrd(mStack_rrd, stackNum_rrd, value_rrd);
                break;
            }

{
                int stackNum_rrd;
                cout << "Enter stack number (0-" << mStack_rrd->numStacks_rrd - 1 << "): ";
                cin >> stackNum_rrd;
                int poppedValue_rrd;
                if (pop_rrd(mStack_rrd, stackNum_rrd, &poppedValue_rrd))
{
                    cout << "Popped value: " << poppedValue_rrd << "" << endl;
                }
                break;
            }

{
                int stackNum_rrd;
                cout << "Enter stack number (0-" << mStack_rrd->numStacks_rrd - 1 << "): ";
                cin >> stackNum_rrd;
                int peekedValue_rrd;
                if (peek_rrd(mStack_rrd, stackNum_rrd, &peekedValue_rrd))
{
                    cout << "Top value of stack " << stackNum_rrd, peekedValue_rrd << ": %d" << endl;
                }
                break;
            }

{
                int stackNum_rrd;
                cout << "Enter stack number (0-" << mStack_rrd->numStacks_rrd - 1 << "): ";
                cin >> stackNum_rrd;
                displayStack_rrd(mStack_rrd, stackNum_rrd);
                break;
            }

{
                displayAllStacks_rrd(mStack_rrd);
                break;
            }

{
                int stackNum_rrd;
                cout << "Enter stack number (0-" << mStack_rrd->numStacks_rrd - 1 << "): ";
                cin >> stackNum_rrd;
                if (isEmpty_rrd(mStack_rrd, stackNum_rrd) == 1)
{
                    cout << "Stack " << stackNum_rrd << " is empty." << endl;
                } else if (isEmpty_rrd(mStack_rrd, stackNum_rrd) == 0)

{
                    cout << "Stack " << stackNum_rrd << " is not empty." << endl;
                }
                break;
            }

{
                int stackNum_rrd;
                cout << "Enter stack number (0-" << mStack_rrd->numStacks_rrd - 1 << "): ";
                cin >> stackNum_rrd;
                if (isFull_rrd(mStack_rrd, stackNum_rrd) == 1)
{
                    cout << "Stack " << stackNum_rrd << " is full." << endl;
                } else if (isFull_rrd(mStack_rrd, stackNum_rrd) == 0)

{
                    cout << "Stack " << stackNum_rrd << " is not full." << endl;
                }
                break;
            }

{
                int stackNum_rrd;
                cout << "Enter stack number (0-" << mStack_rrd->numStacks_rrd - 1 << "): ";
                cin >> stackNum_rrd;
                int size_rrd = getStackSize_rrd(mStack_rrd, stackNum_rrd);
                if (size_rrd >= 0)
{
                    cout << "Size of stack " << stackNum_rrd, size_rrd << ": %d" << endl;
                }
                break;
            }

{
                int stackNum_rrd;
                cout << "Enter stack number (0-" << mStack_rrd->numStacks_rrd - 1 << "): ";
                cin >> stackNum_rrd;
                clearStack_rrd(mStack_rrd, stackNum_rrd);
                break;
            }

{
                clearAllStacks_rrd(mStack_rrd);
                break;
            }

{
                demonstrateOperations_rrd(mStack_rrd);
                break;
            }

{
                cout << "Thank you for using Multiple Stack Implementation!" << endl;
                freeMultipleStack_rrd(mStack_rrd);
                exit(0);
            }

{
                cout << "Invalid choice! Please try again." << endl;
            }
        }
    }
    return 0;
}
```

## Output

```
Welcome to Multiple Stack Implementation!
Enter the number of stacks to create (1-5): 3
Multiple stack created with 3 stacks, each of size 33
===== Multiple Stack Operations =====
1. Push to Stack
2. Pop from Stack
3. Peek at Stack
4. Display Stack
5. Display All Stacks
6. Check if Stack is Empty
7. Check if Stack is Full
8. Get Stack Size
9. Clear Stack
10. Clear All Stacks
11. Demonstrate Operations
12. Exit
====================================
Enter your choice: 11
===== Demonstration of Stack Operations =====
1. Push Operations:
Value 10 pushed to stack 0 successfully!
Value 20 pushed to stack 0 successfully!
Value 30 pushed to stack 1 successfully!
Value 40 pushed to stack 1 successfully!
Value 50 pushed to stack 2 successfully!
2. Display Individual Stacks:
Stack 0 contents (top to bottom): 20 10 
Stack 1 contents (top to bottom): 40 30 
Stack 2 contents (top to bottom): 50 
3. Display All Stacks:
===== All Stacks =====
Stack 0: 20 10 
Stack 1: 40 30 
Stack 2: 50 
=====================
4. Peek Operations:
Top of stack 0: 20
Top of stack 1: 40
5. Pop Operations:
Value 20 popped from stack 0 successfully!
Value 40 popped from stack 1 successfully!
6. Display After Pop Operations:
===== All Stacks =====
Stack 0: 10 
Stack 1: 30 
Stack 2: 50 
=====================
7. Stack Size Information:
Size of stack 0: 1
Size of stack 1: 1
Size of stack 2: 1
```

## Dry Run

For 3 stacks with array size 100:
- Stack 0: indices 0-32
- Stack 1: indices 33-65
- Stack 2: indices 66-98

1. **Push Operations**:
   - Push 10 to stack 0: tops[0] = -1 → 0, array[0] = 10
   - Push 20 to stack 0: tops[0] = 0 → 1, array[1] = 20
   - Push 30 to stack 1: tops[1] = 32 → 33, array[33] = 30
   - Push 40 to stack 1: tops[1] = 33 → 34, array[34] = 40
   - Push 50 to stack 2: tops[2] = 65 → 66, array[66] = 50

2. **Display Stack 0**:
   - Traverse from tops[0] (1) down to 0
   - Print array[1] (20), then array[0] (10)
   - Output: "20 10"

3. **Pop from Stack 1**:
   - Store array[tops[1]] = array[34] = 40
   - tops[1] = 34 → 33
   - Return 40

4. **Check if Stack 2 is Empty**:
   - tops[2] = 66, base index = 66
   - tops[2] >= base index, so not empty

5. **Check if Stack 0 is Full**:
   - tops[0] = 1, max index = 32
   - tops[0] < max index, so not full

## Conclusion

The implementation demonstrates multiple stack management using a single array. Key features include:

1. **Fixed Partitioning**: Each stack gets an equal portion of the array
2. **Independent Operations**: Each stack operates independently
3. **Complete Functionality**: All required stack operations plus additional utilities

**Time Complexities**:
- Push: O(1) - constant time operation
- Pop: O(1) - constant time operation
- Peek: O(1) - constant time operation
- Display: O(n) where n is the number of elements in the stack
- isEmpty/isFull: O(1) - simple index comparisons

**Space Complexity**: O(MAX_SIZE) for the array, O(numStacks) for the tops array

The fixed partitioning approach has advantages and disadvantages:

**Advantages**:
1. **Simple Implementation**: Easy to understand and implement
2. **No Memory Wastage**: Each stack gets exactly its allocated space
3. **Predictable Performance**: No interference between stacks
4. **Memory Efficient**: No extra pointers needed

**Disadvantages**:
1. **Rigid Allocation**: Space cannot be shared between stacks
2. **Potential Wastage**: If one stack grows large while others are small, space is wasted
3. **Limited Flexibility**: Cannot accommodate varying stack sizes dynamically

The implementation handles edge cases properly:
- Invalid stack numbers
- Stack overflow and underflow conditions
- Empty stack operations
- Memory management

Additional features beyond requirements:
- Stack size tracking
- Peek operation
- Clear individual/all stacks
- Comprehensive demonstration
- Detailed error handling

In real-world applications, this system could be extended to:
1. Implement flexible partitioning (variable size stacks)
2. Add dynamic resizing capabilities
3. Support different data types
4. Implement priority-based stack allocation
5. Add thread safety for concurrent access

The multiple stack implementation is useful in scenarios where:
1. Multiple independent data streams need to be managed
2. Memory needs to be partitioned for different purposes
3. Recursive algorithms with multiple state tracking are implemented
4. Compiler design for managing different symbol tables

This implementation provides a solid foundation for understanding how multiple data structures can coexist in a single memory space while maintaining their individual integrity and functionality.
