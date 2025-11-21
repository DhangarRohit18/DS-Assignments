# Unit II Assignment 5: Doubly Linked List for Binary Number Operations

Implementation of binary number storage and operations using a doubly linked list.

## Problem Statement

Write a C++ program to store a binary number using a doubly linked list. Implement the following functions:

a) Calculate and display the 1's complement and 2's complement of the stored binary number
b) Perform addition of two binary numbers represented using doubly linked lists and display the result

## Pseudo Code

### Node Structure
```
Structure BinaryNode:
    bit: integer (0 or 1)
    next: pointer to BinaryNode
    prev: pointer to BinaryNode
```

### Create Binary Number
```
Algorithm CreateBinaryNumber(binaryString):
    Create empty doubly linked list
    For each character in binaryString from right to left:
        Create new node with bit value
        Add to front of list
    Return head of list
```

### 1's Complement
```
Algorithm OnesComplement(head):
    current = head
    While current is not NULL:
        current.bit = 1 - current.bit
        current = current.next
    Return head
```

### 2's Complement
```
Algorithm TwosComplement(head):
    Calculate 1's complement
    Add 1 to result
    Return result
```

### Binary Addition
```
Algorithm BinaryAddition(num1, num2):
    Initialize carry = 0
    Initialize result list
    current1 = tail of num1
    current2 = tail of num2
    
    While current1 is not NULL OR current2 is not NULL OR carry != 0:
        bit1 = current1.bit if current1 not NULL else 0
        bit2 = current2.bit if current2 not NULL else 0
        
        sum = bit1 + bit2 + carry
        resultBit = sum % 2
        carry = sum / 2
        
        Create new node with resultBit
        Add to front of result list
        
        Move current1 and current2 to previous nodes
    
    Return result list
```

### Display Binary Number
```
Algorithm DisplayBinary(head):
    current = head
    While current is not NULL:
        Print current.bit
        current = current.next
```

## Code Implementation

```c
#include <iostream>
using namespace std;
#include <stdlib.h>
#include <string.h>

struct BinaryNode_rrd {
    int bit_rrd;
    struct BinaryNode_rrd* next_rrd;
    struct BinaryNode_rrd* prev_rrd;
};

struct BinaryNode_rrd* createBinaryNode_rrd(int bit_rrd);
struct BinaryNode_rrd* createBinaryNumber_rrd(char binaryStr_rrd[]);
struct BinaryNode_rrd* getTail_rrd(struct BinaryNode_rrd* head_rrd);
void displayBinary_rrd(struct BinaryNode_rrd* head_rrd);
void displayBinaryReverse_rrd(struct BinaryNode_rrd* head_rrd);
struct BinaryNode_rrd* onesComplement_rrd(struct BinaryNode_rrd* head_rrd);
struct BinaryNode_rrd* addOne_rrd(struct BinaryNode_rrd* head_rrd);
struct BinaryNode_rrd* twosComplement_rrd(struct BinaryNode_rrd* head_rrd);
struct BinaryNode_rrd* addBinary_rrd(struct BinaryNode_rrd* num1_rrd, struct BinaryNode_rrd* num2_rrd);
void freeBinaryNumber_rrd(struct BinaryNode_rrd* head_rrd);
void displayMenu_rrd();

struct BinaryNode_rrd* createBinaryNode_rrd(int bit_rrd) {
    struct BinaryNode_rrd* newNode_rrd = (struct BinaryNode_rrd*)malloc(sizeof(struct BinaryNode_rrd));
    newNode_rrd->bit_rrd = bit_rrd;
    newNode_rrd->next_rrd = NULL;
    newNode_rrd->prev_rrd = NULL;
    return newNode_rrd;
}

struct BinaryNode_rrd* createBinaryNumber_rrd(char binaryStr_rrd[]) {
    struct BinaryNode_rrd* head_rrd = NULL;
    struct BinaryNode_rrd* tail_rrd = NULL;
    
    int len_rrd = strlen(binaryStr_rrd);
    
    for (int i_rrd = 0; i_rrd < len_rrd; i_rrd++) {
        if (binaryStr_rrd[i_rrd] != '0' && binaryStr_rrd[i_rrd] != '1') {
            cout << "Invalid binary number!" << endl;
            return NULL;
        }
    }
    
    for (int i_rrd = len_rrd - 1; i_rrd >= 0; i_rrd--) {
        struct BinaryNode_rrd* newNode_rrd = createBinaryNode_rrd(binaryStr_rrd[i_rrd] - '0');
        
        if (head_rrd == NULL) {
            head_rrd = newNode_rrd;
            tail_rrd = newNode_rrd;
        } else {
            newNode_rrd->next_rrd = head_rrd;
            head_rrd->prev_rrd = newNode_rrd;
            head_rrd = newNode_rrd;
        }
    }
    
    return head_rrd;
}

struct BinaryNode_rrd* getTail_rrd(struct BinaryNode_rrd* head_rrd) {
    if (head_rrd == NULL) return NULL;
    
    struct BinaryNode_rrd* current_rrd = head_rrd;
    while (current_rrd->next_rrd != NULL) {
        current_rrd = current_rrd->next_rrd;
    }
    return current_rrd;
}

void displayBinary_rrd(struct BinaryNode_rrd* head_rrd) {
    if (head_rrd == NULL) {
        cout << "0";
        return;
    }
    
    struct BinaryNode_rrd* current_rrd = head_rrd;
    while (current_rrd != NULL) {
        cout << "" << current_rrd->bit_rrd << "";
        current_rrd = current_rrd->next_rrd;
    }
}

void displayBinaryReverse_rrd(struct BinaryNode_rrd* head_rrd) {
    if (head_rrd == NULL) {
        cout << "0";
        return;
    }
    
    struct BinaryNode_rrd* tail_rrd = getTail_rrd(head_rrd);
    struct BinaryNode_rrd* current_rrd = tail_rrd;
    
    while (current_rrd != NULL) {
        cout << "" << current_rrd->bit_rrd << "";
        current_rrd = current_rrd->prev_rrd;
    }
}

struct BinaryNode_rrd* onesComplement_rrd(struct BinaryNode_rrd* head_rrd) {
    if (head_rrd == NULL) return NULL;
    
    struct BinaryNode_rrd* resultHead_rrd = NULL;
    struct BinaryNode_rrd* resultTail_rrd = NULL;
    
    struct BinaryNode_rrd* current_rrd = head_rrd;
    while (current_rrd != NULL) {
        struct BinaryNode_rrd* newNode_rrd = createBinaryNode_rrd(1 - current_rrd->bit_rrd);
        
        if (resultHead_rrd == NULL) {
            resultHead_rrd = newNode_rrd;
            resultTail_rrd = newNode_rrd;
        } else {
            resultTail_rrd->next_rrd = newNode_rrd;
            newNode_rrd->prev_rrd = resultTail_rrd;
            resultTail_rrd = newNode_rrd;
        }
        
        current_rrd = current_rrd->next_rrd;
    }
    
    return resultHead_rrd;
}

struct BinaryNode_rrd* addOne_rrd(struct BinaryNode_rrd* head_rrd) {
    if (head_rrd == NULL) {
        struct BinaryNode_rrd* newNode_rrd = createBinaryNode_rrd(1);
        return newNode_rrd;
    }
    
    struct BinaryNode_rrd* resultHead_rrd = NULL;
    struct BinaryNode_rrd* resultTail_rrd = NULL;
    
    struct BinaryNode_rrd* current_rrd = head_rrd;
    while (current_rrd != NULL) {
        struct BinaryNode_rrd* newNode_rrd = createBinaryNode_rrd(current_rrd->bit_rrd);
        
        if (resultHead_rrd == NULL) {
            resultHead_rrd = newNode_rrd;
            resultTail_rrd = newNode_rrd;
        } else {
            resultTail_rrd->next_rrd = newNode_rrd;
            newNode_rrd->prev_rrd = resultTail_rrd;
            resultTail_rrd = newNode_rrd;
        }
        
        current_rrd = current_rrd->next_rrd;
    }
    
    int carry_rrd = 1;
    current_rrd = resultTail_rrd;
    
    while (current_rrd != NULL && carry_rrd) {
        int sum_rrd = current_rrd->bit_rrd + carry_rrd;
        current_rrd->bit_rrd = sum_rrd % 2;
        carry_rrd = sum_rrd / 2;
        current_rrd = current_rrd->prev_rrd;
    }
    
    if (carry_rrd) {
        struct BinaryNode_rrd* newNode_rrd = createBinaryNode_rrd(1);
        newNode_rrd->next_rrd = resultHead_rrd;
        if (resultHead_rrd != NULL) {
            resultHead_rrd->prev_rrd = newNode_rrd;
        }
        resultHead_rrd = newNode_rrd;
    }
    
    return resultHead_rrd;
}

struct BinaryNode_rrd* twosComplement_rrd(struct BinaryNode_rrd* head_rrd) {
    if (head_rrd == NULL) return NULL;
    
    struct BinaryNode_rrd* onesComp_rrd = onesComplement_rrd(head_rrd);
    
    struct BinaryNode_rrd* twosComp_rrd = addOne_rrd(onesComp_rrd);
    
    return twosComp_rrd;
}

struct BinaryNode_rrd* binaryAddition_rrd(struct BinaryNode_rrd* num1_rrd, struct BinaryNode_rrd* num2_rrd) {
    struct BinaryNode_rrd* tail1_rrd = getTail_rrd(num1_rrd);
    struct BinaryNode_rrd* tail2_rrd = getTail_rrd(num2_rrd);
    
    struct BinaryNode_rrd* resultHead_rrd = NULL;
    struct BinaryNode_rrd* resultTail_rrd = NULL;
    int carry_rrd = 0;
    
    struct BinaryNode_rrd* current1_rrd = tail1_rrd;
    struct BinaryNode_rrd* current2_rrd = tail2_rrd;
    
    while (current1_rrd != NULL || current2_rrd != NULL || carry_rrd) {
        int bit1_rrd = (current1_rrd != NULL) ? current1_rrd->bit_rrd : 0;
        int bit2_rrd = (current2_rrd != NULL) ? current2_rrd->bit_rrd : 0;
        
        int sum_rrd = bit1_rrd + bit2_rrd + carry_rrd;
        int resultBit_rrd = sum_rrd % 2;
        carry_rrd = sum_rrd / 2;
        
        struct BinaryNode_rrd* newNode_rrd = createBinaryNode_rrd(resultBit_rrd);
        
        if (resultHead_rrd == NULL) {
            resultHead_rrd = newNode_rrd;
            resultTail_rrd = newNode_rrd;
        } else {
            newNode_rrd->next_rrd = resultHead_rrd;
            resultHead_rrd->prev_rrd = newNode_rrd;
            resultHead_rrd = newNode_rrd;
        }
        
        if (current1_rrd != NULL) current1_rrd = current1_rrd->prev_rrd;
        if (current2_rrd != NULL) current2_rrd = current2_rrd->prev_rrd;
    }
    
    return resultHead_rrd;
}

void freeBinaryNumber_rrd(struct BinaryNode_rrd* head_rrd) {
    struct BinaryNode_rrd* current_rrd = head_rrd;
    while (current_rrd != NULL) {
        struct BinaryNode_rrd* temp_rrd = current_rrd;
        current_rrd = current_rrd->next_rrd;
        free(temp_rrd);
    }
}

int countBits_rrd(struct BinaryNode_rrd* head_rrd) {
    int count_rrd = 0;
    struct BinaryNode_rrd* current_rrd = head_rrd;
    while (current_rrd != NULL) {
        count_rrd++;
        current_rrd = current_rrd->next_rrd;
    }
    return count_rrd;
}

struct BinaryNode_rrd* padWithZeros_rrd(struct BinaryNode_rrd* head_rrd, int targetLength_rrd) {
    int currentLength_rrd = countBits_rrd(head_rrd);
    
    if (currentLength_rrd >= targetLength_rrd)
{
        return head_rrd;
    }
    
    struct BinaryNode_rrd* newHead_rrd = head_rrd;
    for (int i_rrd = 0; i_rrd < targetLength_rrd - currentLength_rrd; i_rrd++)
{
        struct BinaryNode_rrd* zeroNode_rrd = createBinaryNode_rrd(0);
        zeroNode_rrd->next_rrd = newHead_rrd;
        if (newHead_rrd != NULL)
{
            newHead_rrd->prev_rrd = zeroNode_rrd;
        }
        newHead_rrd = zeroNode_rrd;
    }
    
    return newHead_rrd;
}

void displayMenu_rrd() {
    cout << "\n===== Binary Number Operations using Doubly Linked List =====" << endl;
    cout << "1. Enter Binary Numbers" << endl;
    cout << "2. Display Binary Numbers" << endl;
    cout << "3. Calculate 1's Complement" << endl;
    cout << "4. Calculate 2's Complement" << endl;
    cout << "5. Perform Binary Addition" << endl;
    cout << "6. Exit" << endl;
    cout << "==========================================================" << endl;
    cout << "Enter your choice: ";
}

int main() {
    cout << "Welcome to Binary Number Operations System!" << endl;
    
    struct BinaryNode_rrd* binary1_rrd = NULL;
    struct BinaryNode_rrd* binary2_rrd = NULL;
    
    int choice_rrd;
    while (1)
{
        displayMenu_rrd();
        cin >> choice_rrd;
        
        switch (choice_rrd)
{
            
{
                char binaryStr1_rrd[100], binaryStr2_rrd[100];
                
                cout << "Enter first binary number: ";
                cin >> binaryStr1_rrd;
                
                cout << "Enter second binary number: ";
                cin >> binaryStr2_rrd;
                
                freeBinaryNumber_rrd(binary1_rrd);
                freeBinaryNumber_rrd(binary2_rrd);
                
                binary1_rrd = createBinaryNumber_rrd(binaryStr1_rrd);
                binary2_rrd = createBinaryNumber_rrd(binaryStr2_rrd);
                
                if (binary1_rrd != NULL && binary2_rrd != NULL)
{
                    cout << "Binary numbers stored successfully!" << endl;
                }
                break;
            }
            
            
{
                if (binary1_rrd == NULL || binary2_rrd == NULL)
{
                    cout << "Please enter binary numbers first (Option 1)!" << endl;
                    break;
                }
                
                cout << "First binary number: ";
                displayBinary_rrd(binary1_rrd);
                cout << "" << endl;
                
                cout << "Second binary number: ";
                displayBinary_rrd(binary2_rrd);
                cout << "" << endl;
                break;
            }
            
            
{
                if (binary1_rrd == NULL || binary2_rrd == NULL)
{
                    cout << "Please enter binary numbers first (Option 1)!" << endl;
                    break;
                }
                
                cout << "First binary number: ";
                displayBinary_rrd(binary1_rrd);
                cout << "" << endl;
                
                struct BinaryNode_rrd* onesComp1_rrd = onesComplement_rrd(binary1_rrd);
                cout << "1's complement: ";
                displayBinary_rrd(onesComp1_rrd);
                cout << "" << endl;
                
                cout << "\nSecond binary number: ";
                displayBinary_rrd(binary2_rrd);
                cout << "" << endl;
                
                struct BinaryNode_rrd* onesComp2_rrd = onesComplement_rrd(binary2_rrd);
                cout << "1's complement: ";
                displayBinary_rrd(onesComp2_rrd);
                cout << "" << endl;
                
                freeBinaryNumber_rrd(onesComp1_rrd);
                freeBinaryNumber_rrd(onesComp2_rrd);
                break;
            }
            
            
{
                if (binary1_rrd == NULL || binary2_rrd == NULL)
{
                    cout << "Please enter binary numbers first (Option 1)!" << endl;
                    break;
                }
                
                cout << "First binary number: ";
                displayBinary_rrd(binary1_rrd);
                cout << "" << endl;
                
                struct BinaryNode_rrd* twosComp1_rrd = twosComplement_rrd(binary1_rrd);
                cout << "2's complement: ";
                displayBinary_rrd(twosComp1_rrd);
                cout << "" << endl;
                
                cout << "\nSecond binary number: ";
                displayBinary_rrd(binary2_rrd);
                cout << "" << endl;
                
                struct BinaryNode_rrd* twosComp2_rrd = twosComplement_rrd(binary2_rrd);
                cout << "2's complement: ";
                displayBinary_rrd(twosComp2_rrd);
                cout << "" << endl;
                
                freeBinaryNumber_rrd(twosComp1_rrd);
                freeBinaryNumber_rrd(twosComp2_rrd);
                break;
            }
            
            
{
                if (binary1_rrd == NULL || binary2_rrd == NULL)
{
                    cout << "Please enter binary numbers first (Option 1)!" << endl;
                    break;
                }
                
                cout << "First binary number: ";
                displayBinary_rrd(binary1_rrd);
                cout << "" << endl;
                
                cout << "Second binary number: ";
                displayBinary_rrd(binary2_rrd);
                cout << "" << endl;
                
                struct BinaryNode_rrd* sum_rrd = binaryAddition_rrd(binary1_rrd, binary2_rrd);
                cout << "Sum: ";
                displayBinary_rrd(sum_rrd);
                cout << "" << endl;
                
                freeBinaryNumber_rrd(sum_rrd);
                break;
            }
            
            
{
                cout << "Thank you for using Binary Number Operations System!" << endl;
                freeBinaryNumber_rrd(binary1_rrd);
                freeBinaryNumber_rrd(binary2_rrd);
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
Welcome to Binary Number Operations System!

===== Binary Number Operations using Doubly Linked List =====
1. Enter Binary Numbers
2. Display Binary Numbers
3. Calculate 1's Complement
4. Calculate 2's Complement
5. Perform Binary Addition
6. Exit
==========================================================
Enter your choice: 1
Enter first binary number: 1011
Enter second binary number: 1101
Binary numbers stored successfully!

===== Binary Number Operations using Doubly Linked List =====
1. Enter Binary Numbers
2. Display Binary Numbers
3. Calculate 1's Complement
4. Calculate 2's Complement
5. Perform Binary Addition
6. Exit
==========================================================
Enter your choice: 2
First binary number: 1011
Second binary number: 1101

===== Binary Number Operations using Doubly Linked List =====
1. Enter Binary Numbers
2. Display Binary Numbers
3. Calculate 1's Complement
4. Calculate 2's Complement
5. Perform Binary Addition
6. Exit
==========================================================
Enter your choice: 3
First binary number: 1011
1's complement: 0100

Second binary number: 1101
1's complement: 0010

===== Binary Number Operations using Doubly Linked List =====
1. Enter Binary Numbers
2. Display Binary Numbers
3. Calculate 1's Complement
4. Calculate 2's Complement
5. Perform Binary Addition
6. Exit
==========================================================
Enter your choice: 4
First binary number: 1011
2's complement: 0101

Second binary number: 1101
2's complement: 0011

===== Binary Number Operations using Doubly Linked List =====
1. Enter Binary Numbers
2. Display Binary Numbers
3. Calculate 1's Complement
4. Calculate 2's Complement
5. Perform Binary Addition
6. Exit
==========================================================
Enter your choice: 5
First binary number: 1011
Second binary number: 1101
Sum: 11000
```

## Dry Run

1. **Input Binary Numbers**:
   - First number: 1011 (11 in decimal)
   - Second number: 1101 (13 in decimal)
   - Create doubly linked list for each with bits stored from MSB to LSB

2. **1's Complement Calculation**:
   - For 1011:
     * Flip each bit: 1→0, 0→1, 1→0, 1→0
     * Result: 0100
   - For 1101:
     * Flip each bit: 1→0, 1→0, 0→1, 1→0
     * Result: 0010

3. **2's Complement Calculation**:
   - For 1011:
     * Calculate 1's complement: 0100
     * Add 1: 0100 + 1 = 0101
     * Result: 0101
   - For 1101:
     * Calculate 1's complement: 0010
     * Add 1: 0010 + 1 = 0011
     * Result: 0011

4. **Binary Addition**:
   - Add 1011 + 1101:
     * 1 + 1 = 2 (0 with carry 1)
     * 1 + 0 + 1 (carry) = 2 (0 with carry 1)
     * 0 + 1 + 1 (carry) = 2 (0 with carry 1)
     * 1 + 1 + 1 (carry) = 3 (1 with carry 1)
     * 0 + 0 + 1 (carry) = 1 (1 with carry 0)
   - Result: 11000 (24 in decimal, which is 11+13)

## Conclusion

The implementation demonstrates binary number operations using doubly linked lists. Key features include:

1. **Doubly Linked List Structure**: Each node stores one bit with pointers to next and previous nodes
2. **1's Complement**: Simple bit flipping operation
3. **2's Complement**: 1's complement plus 1 addition
4. **Binary Addition**: Full adder implementation with carry propagation

**Time Complexities**:
- Creating binary number: O(n) where n is number of bits
- 1's complement: O(n)
- 2's complement: O(n) for 1's complement + O(n) for addition = O(n)
- Binary addition: O(max(n,m)) where n and m are lengths of the two numbers

The doubly linked list structure is particularly suitable for this application because:
1. **Bidirectional Traversal**: Needed for addition from LSB to MSB
2. **Dynamic Size**: Binary numbers can be of any length
3. **Easy Insertion**: New bits can be easily added at either end
4. **Memory Efficiency**: Only allocates memory for actual bits

The implementation handles edge cases properly:
- Invalid binary input validation
- Carry propagation in addition
- Proper memory management to prevent leaks
- Handling of different length binary numbers

In practical applications, this system could be extended to:
1. Support subtraction using 2's complement
2. Handle signed binary numbers
3. Implement multiplication and division
4. Add support for floating-point binary numbers
5. Optimize for very large binary numbers using more efficient algorithms

The doubly linked list approach provides a clear, educational implementation of binary operations that demonstrates fundamental concepts in computer arithmetic and data structures.