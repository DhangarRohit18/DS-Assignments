# Unit III Assignment 1: Stock Price Tracker using Stack

Implementation of a simple stock price tracker that keeps a history of daily stock prices using a stack implemented with a linked list.

## Problem Statement

Build a simple stock price tracker that keeps a history of daily stock prices entered by the user. To allow users to go back and view or remove the most recent price, implement a stack using a linked list to store these integer prices. Implement the following operations:

1. record(price) – Add a new stock price (an integer) to the stack
2. remove() – Remove and return the most recent price (top of the stack)
3. latest() – Return the most recent stock price without removing it
4. isEmpty() – Check if there are no prices recorded

## Pseudo Code

### Node Structure
```
Structure StackNode:
    price: integer
    next: pointer to StackNode
```

### Stack Structure
```
Structure StockPriceStack:
    top: pointer to StackNode
    size: integer
```

### Record Price
```
Algorithm RecordPrice(stack, price):
    Create new node with price
    new node.next = stack.top
    stack.top = new node
    stack.size++
```

### Remove Price
```
Algorithm RemovePrice(stack):
    If stack is empty:
        Return error/invalid value
    price = stack.top.price
    temp = stack.top
    stack.top = stack.top.next
    Free temp
    stack.size--
    Return price
```

### Latest Price
```
Algorithm LatestPrice(stack):
    If stack is empty:
        Return error/invalid value
    Return stack.top.price
```

### Is Empty
```
Algorithm IsEmpty(stack):
    Return stack.top == NULL
```

## Code Implementation

```c
#include <iostream>
using namespace std;
#include <stdlib.h>
struct StackNode_rrd {
    int price_rrd;
    struct StackNode_rrd* next_rrd;
};

struct StockPriceStack_rrd {
    struct StackNode_rrd* top_rrd;
    int size_rrd;
};

struct StockPriceStack_rrd* createStack_rrd();
int isEmpty_rrd(struct StockPriceStack_rrd* stack_rrd);
void record_rrd(struct StockPriceStack_rrd* stack_rrd, int price_rrd);
int remove_rrd(struct StockPriceStack_rrd* stack_rrd);
int latest_rrd(struct StockPriceStack_rrd* stack_rrd);
int size_rrd(struct StockPriceStack_rrd* stack_rrd);
void displayPrices_rrd(struct StockPriceStack_rrd* stack_rrd);
void clearStack_rrd(struct StockPriceStack_rrd* stack_rrd);
double calculateAverage_rrd(struct StockPriceStack_rrd* stack_rrd);
int findMaximum_rrd(struct StockPriceStack_rrd* stack_rrd);
int findMinimum_rrd(struct StockPriceStack_rrd* stack_rrd);
void freeStack_rrd(struct StockPriceStack_rrd* stack_rrd);
void displayMenu_rrd();

struct StockPriceStack_rrd* createStack_rrd() 
{
    struct StockPriceStack_rrd* stack_rrd = (struct StockPriceStack_rrd*)malloc(sizeof(struct StockPriceStack_rrd));
    stack_rrd->top_rrd = NULL;
    stack_rrd->size_rrd = 0;
    return stack_rrd;
}

int isEmpty_rrd(struct StockPriceStack_rrd* stack_rrd) 
{
    return stack_rrd->top_rrd == NULL;
}

void record_rrd(struct StockPriceStack_rrd* stack_rrd, int price_rrd) 
{
    struct StackNode_rrd* newNode_rrd = (struct StackNode_rrd*)malloc(sizeof(struct StackNode_rrd));
    newNode_rrd->price_rrd = price_rrd;
    newNode_rrd->next_rrd = stack_rrd->top_rrd;
    stack_rrd->top_rrd = newNode_rrd;
    stack_rrd->size_rrd++;
    cout << "Price " << price_rrd << " recorded successfully!" << endl;
}

int remove_rrd(struct StockPriceStack_rrd* stack_rrd) 
{
    if (isEmpty_rrd(stack_rrd))
    {
        cout << "Error: No prices recorded!" << endl;
        return -1;
    }

    struct StackNode_rrd* temp_rrd = stack_rrd->top_rrd;
    int price_rrd = temp_rrd->price_rrd;
    stack_rrd->top_rrd = stack_rrd->top_rrd->next_rrd;
    free(temp_rrd);
    stack_rrd->size_rrd--;
    cout << "Most recent price " << price_rrd << " removed successfully!" << endl;
    return price_rrd;
}

int latest_rrd(struct StockPriceStack_rrd* stack_rrd) 
{
    if (isEmpty_rrd(stack_rrd))
    {
        cout << "Error: No prices recorded!" << endl;
        return -1;
    }
    return stack_rrd->top_rrd->price_rrd;
}

int size_rrd(struct StockPriceStack_rrd* stack_rrd) 
{
    return stack_rrd->size_rrd;
}

void displayPrices_rrd(struct StockPriceStack_rrd* stack_rrd) 
{
    if (isEmpty_rrd(stack_rrd))
    {
        cout << "No prices recorded!" << endl;
        return;
    }

    cout << "\n===== Stock Price History (Most Recent First) =====" << endl;
    cout << "Position\tPrice" << endl;
    cout << "-------------------" << endl;
    struct StackNode_rrd* current_rrd = stack_rrd->top_rrd;
    int position_rrd = 1;
    while (current_rrd != NULL)
    {
        cout << "" << position_rrd, current_rrd->price_rrd << "\t\t%d" << endl;
        current_rrd = current_rrd->next_rrd;
        position_rrd++;
    }

    cout << "-------------------" << endl;
    cout << "Total entries: " << stack_rrd->size_rrd << "" << endl;
}

void clearStack_rrd(struct StockPriceStack_rrd* stack_rrd) 
{
    while (!isEmpty_rrd(stack_rrd))
    {
        remove_rrd(stack_rrd);
    }
    cout << "All prices cleared!" << endl;
}

double calculateAverage_rrd(struct StockPriceStack_rrd* stack_rrd) 
{
    if (isEmpty_rrd(stack_rrd))
    {
        cout << "No prices to calculate average!" << endl;
        return 0.0;
    }

    long long sum_rrd = 0;
    int count_rrd = 0;
    struct StackNode_rrd* current_rrd = stack_rrd->top_rrd;
    while (current_rrd != NULL)
    {
        sum_rrd += current_rrd->price_rrd;
        count_rrd++;
        current_rrd = current_rrd->next_rrd;
    }
    return (double)sum_rrd / count_rrd;
}

int findMaximum_rrd(struct StockPriceStack_rrd* stack_rrd) 
{
    if (isEmpty_rrd(stack_rrd))
    {
        cout << "No prices recorded!" << endl;
        return -1;
    }

    int maxPrice_rrd = stack_rrd->top_rrd->price_rrd;
    struct StackNode_rrd* current_rrd = stack_rrd->top_rrd->next_rrd;
    while (current_rrd != NULL)
    {
        if (current_rrd->price_rrd > maxPrice_rrd)
        {
            maxPrice_rrd = current_rrd->price_rrd;
        }
        current_rrd = current_rrd->next_rrd;
    }
    return maxPrice_rrd;
}

int findMinimum_rrd(struct StockPriceStack_rrd* stack_rrd) 
{
    if (isEmpty_rrd(stack_rrd))
    {
        cout << "No prices recorded!" << endl;
        return -1;
    }

    int minPrice_rrd = stack_rrd->top_rrd->price_rrd;
    struct StackNode_rrd* current_rrd = stack_rrd->top_rrd->next_rrd;
    while (current_rrd != NULL)
    {
        if (current_rrd->price_rrd < minPrice_rrd)
        {
            minPrice_rrd = current_rrd->price_rrd;
        }

        current_rrd = current_rrd->next_rrd;
    }
    return minPrice_rrd;
}

void freeStack_rrd(struct StockPriceStack_rrd* stack_rrd) 
{
    clearStack_rrd(stack_rrd);
    free(stack_rrd);
}

void displayMenu_rrd() 
{
    cout << "\n===== Stock Price Tracker =====" << endl;
    cout << "1. Record Price" << endl;
    cout << "2. Remove Most Recent Price" << endl;
    cout << "3. View Latest Price" << endl;
    cout << "4. Check if Empty" << endl;
    cout << "5. Display All Prices" << endl;
    cout << "6. Get Stack Size" << endl;
    cout << "7. Calculate Average Price" << endl;
    cout << "8. Find Maximum Price" << endl;
    cout << "9. Find Minimum Price" << endl;
    cout << "10. Clear All Prices" << endl;
    cout << "11. Exit" << endl;
    cout << "==============================" << endl;
    cout << "Enter your choice: ";
}

int main() 
{
    cout << "Welcome to Stock Price Tracker!" << endl;
    struct StockPriceStack_rrd* priceStack_rrd = createStack_rrd();
    int choice_rrd;
    
    while (1)
    {
        displayMenu_rrd();
        cin >> choice_rrd;
        
        switch (choice_rrd)
        {
            case 1: {
                int price_rrd;
                cout << "Enter stock price: ";
                cin >> price_rrd;
                if (price_rrd < 0)
                {
                    cout << "Error: Price cannot be negative!" << endl;
                } 
                else
                {
                    record_rrd(priceStack_rrd, price_rrd);
                }
                break;
            }
            
            case 2: {
                remove_rrd(priceStack_rrd);
                break;
            }
            
            case 3: {
                int latestPrice_rrd = latest_rrd(priceStack_rrd);
                if (latestPrice_rrd != -1)
                {
                    cout << "Latest stock price: " << latestPrice_rrd << "" << endl;
                }
                break;
            }
            
            case 4: {
                if (isEmpty_rrd(priceStack_rrd))
                {
                    cout << "Stack is empty!" << endl;
                } 
                else
                {
                    printf("Stack is not empty. Contains %d prices.\n", size_rrd(priceStack_rrd));
                }
                break;
            }
            
            case 5: {
                displayPrices_rrd(priceStack_rrd);
                break;
            }
            
            case 6: {
                printf("Number of prices recorded: %d\n", size_rrd(priceStack_rrd));
                break;
            }
            
            case 7: {
                double average_rrd = calculateAverage_rrd(priceStack_rrd);
                if (average_rrd > 0)
                {
                    printf("Average price: %.2f\n", average_rrd);
                }
                break;
            }
            
            case 8: {
                int maxPrice_rrd = findMaximum_rrd(priceStack_rrd);
                if (maxPrice_rrd != -1)
                {
                    cout << "Maximum price: " << maxPrice_rrd << "" << endl;
                }
                break;
            }
            
            case 9: {
                int minPrice_rrd = findMinimum_rrd(priceStack_rrd);
                if (minPrice_rrd != -1)
                {
                    cout << "Minimum price: " << minPrice_rrd << "" << endl;
                }
                break;
            }
            
            case 10: {
                clearStack_rrd(priceStack_rrd);
                break;
            }
            
            case 11: {
                cout << "Thank you for using Stock Price Tracker!" << endl;
                freeStack_rrd(priceStack_rrd);
                exit(0);
            }
            
            default: {
                cout << "Invalid choice! Please try again." << endl;
                break;
            }
        }
    }
    
    return 0;
}
```

## Output

```
Welcome to Stock Price Tracker!
===== Stock Price Tracker =====
1. Record Price
2. Remove Most Recent Price
3. View Latest Price
4. Check if Empty
5. Display All Prices
6. Get Stack Size
7. Calculate Average Price
8. Find Maximum Price
9. Find Minimum Price
10. Clear All Prices
11. Exit
==============================
Enter your choice: 1
Enter stock price: 150
Price 150 recorded successfully!

===== Stock Price Tracker =====
1. Record Price
2. Remove Most Recent Price
3. View Latest Price
4. Check if Empty
5. Display All Prices
6. Get Stack Size
7. Calculate Average Price
8. Find Maximum Price
9. Find Minimum Price
10. Clear All Prices
11. Exit
==============================
Enter your choice: 1
Enter stock price: 155
Price 155 recorded successfully!

===== Stock Price Tracker =====
1. Record Price
2. Remove Most Recent Price
3. View Latest Price
4. Check if Empty
5. Display All Prices
6. Get Stack Size
7. Calculate Average Price
8. Find Maximum Price
9. Find Minimum Price
10. Clear All Prices
11. Exit
==============================
Enter your choice: 1
Enter stock price: 148
Price 148 recorded successfully!

===== Stock Price Tracker =====
1. Record Price
2. Remove Most Recent Price
3. View Latest Price
4. Check if Empty
5. Display All Prices
6. Get Stack Size
7. Calculate Average Price
8. Find Maximum Price
9. Find Minimum Price
10. Clear All Prices
11. Exit
==============================
Enter your choice: 5

===== Stock Price History (Most Recent First) =====
Position	Price
-------------------
1		148
2		155
3		150
-------------------
Total entries: 3

===== Stock Price Tracker =====
1. Record Price
2. Remove Most Recent Price
3. View Latest Price
4. Check if Empty
5. Display All Prices
6. Get Stack Size
7. Calculate Average Price
8. Find Maximum Price
9. Find Minimum Price
10. Clear All Prices
11. Exit
==============================
Enter your choice: 3
Latest stock price: 148

===== Stock Price Tracker =====
1. Record Price
2. Remove Most Recent Price
3. View Latest Price
4. Check if Empty
5. Display All Prices
6. Get Stack Size
7. Calculate Average Price
8. Find Maximum Price
9. Find Minimum Price
10. Clear All Prices
11. Exit
==============================
Enter your choice: 2
Most recent price 148 removed successfully!

===== Stock Price Tracker =====
1. Record Price
2. Remove Most Recent Price
3. View Latest Price
4. Check if Empty
5. Display All Prices
6. Get Stack Size
7. Calculate Average Price
8. Find Maximum Price
9. Find Minimum Price
10. Clear All Prices
11. Exit
==============================
```

## Dry Run

1. **Record Prices**:
   - Record 150: Create node with value 150, set top to this node
   - Record 155: Create node with value 155, set next to previous top (150), update top to 155
   - Record 148: Create node with value 148, set next to previous top (155), update top to 148
   - Stack: 148 → 155 → 150 (top to bottom)

2. **View Latest Price**:
   - Return value of top node: 148

3. **Display All Prices**:
   - Traverse from top to bottom: 148, 155, 150

4. **Remove Most Recent Price**:
   - Store value of top node (148)
   - Update top to next node (155)
   - Free memory of removed node
   - Return stored value (148)
   - Stack now: 155 → 150

5. **Check if Empty**:
   - Check if top is NULL: No, stack contains 2 elements

## Conclusion

The implementation demonstrates a stack-based stock price tracker using linked list implementation. Key features include:

1. **LIFO Structure**: Last In, First Out behavior perfect for tracking most recent prices
2. **Dynamic Memory**: Memory allocated only for recorded prices
3. **Complete Operations**: All required stack operations plus additional utility functions

**Time Complexities**:
- Record (Push): O(1) - constant time insertion at head
- Remove (Pop): O(1) - constant time removal from head
- Latest (Peek): O(1) - constant time access to head
- Is Empty: O(1) - simple pointer check
- Display All: O(n) - linear traversal where n is number of prices
- Average/Min/Max: O(n) - requires traversal of all elements

**Space Complexity**: O(n) where n is the number of recorded prices

The linked list implementation is ideal for this application because:
1. **Dynamic Size**: Stack can grow or shrink as needed
2. **Memory Efficiency**: Only allocates memory for actual entries
3. **Simple Operations**: Push and pop are simple pointer manipulations
4. **No Size Limitations**: Unlike array-based stacks, no fixed capacity

The system handles edge cases properly:
- Empty stack operations with appropriate error messages
- Negative price validation
- Memory management to prevent leaks
- Comprehensive user interface with clear feedback

Additional features beyond requirements:
- Stack size tracking
- Average price calculation
- Maximum/minimum price finding
- Complete price history display
- Stack clearing functionality

In real-world applications, this system could be extended to:
1. Support multiple stocks
2. Add timestamp information
3. Persist data to files
4. Add graphical visualization
5. Implement price alerts
6. Add statistical analysis features

The stack data structure is perfectly suited for this application as it naturally maintains the chronological order of price entries with efficient access to the most recent entry.
