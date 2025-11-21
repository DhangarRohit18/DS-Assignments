# Unit II Assignment 6: Set Implementation using Generalized Linked List

Implementation of a Set using a Generalized Linked List (GLL) to store complex nested structures and display elements in correct set notation format.

## Problem Statement

Implement a Set using a Generalized Linked List (GLL) to store the structure:
S = { p, q, {r, s, t, {}, {u, v}, w, x, {y, z}, a1, b1} }

Store this structure using a Generalized Linked List and display the elements in correct set notation format.

## Pseudo Code

### GLL Node Structure
```
Structure GLLNode:
    tag: integer (0 for atom, 1 for list)
    data: union
        atom: character or string
        list: pointer to GLLNode
    next: pointer to GLLNode
```

### Create Atom Node
```
Algorithm CreateAtomNode(data):
    Create new node
    node.tag = 0
    node.data.atom = data
    node.next = NULL
    Return node
```

### Create List Node
```
Algorithm CreateListNode(list):
    Create new node
    node.tag = 1
    node.data.list = list
    node.next = NULL
    Return node
```

### Display GLL
```
Algorithm DisplayGLL(node):
    If node is NULL:
        Print "{}"
        Return
    Print "{"
    While node is not NULL:
        If node.tag == 0:
            Print node.data.atom
        Else:
            DisplayGLL(node.data.list)
        If node.next is not NULL:
            Print ", "
        node = node.next
    Print "}"
```

## Code Implementation

```c
#include <iostream>
using namespace std;
#include <stdlib.h>
#include <string.h>

struct GLLNode_rrd {
    int tag_rrd;
    union {
        char atom_rrd[20];
        struct GLLNode_rrd* list_rrd;
    } data_rrd;
    struct GLLNode_rrd* next_rrd;
};

struct GLLNode_rrd* createAtomNode_rrd(char* atom_rrd);
struct GLLNode_rrd* createListNode_rrd(struct GLLNode_rrd* list_rrd);
void displayGLL_rrd(struct GLLNode_rrd* node_rrd);
struct GLLNode_rrd* createSetExample_rrd();
void freeGLL_rrd(struct GLLNode_rrd* node_rrd);

int main() {
    struct GLLNode_rrd* set_rrd;
    
    cout << "Generalized Linked List Implementation of Set" << endl;
    cout << "============================================" << endl;
    

    set_rrd = createSetExample_rrd();
    
    cout << "Set S = ";
    displayGLL_rrd(set_rrd);
    cout << "" << endl;
    

    freeGLL_rrd(set_rrd);
    
    return 0;
}

struct GLLNode_rrd* createAtomNode_rrd(char* atom_rrd) {
    struct GLLNode_rrd* newNode_rrd = (struct GLLNode_rrd*)malloc(sizeof(struct GLLNode_rrd));
    newNode_rrd->tag_rrd = 0;
    strcpy(newNode_rrd->data_rrd.atom_rrd, atom_rrd);
    newNode_rrd->next_rrd = NULL;
    return newNode_rrd;
}

struct GLLNode_rrd* createListNode_rrd(struct GLLNode_rrd* list_rrd) {
    struct GLLNode_rrd* newNode_rrd = (struct GLLNode_rrd*)malloc(sizeof(struct GLLNode_rrd));
    newNode_rrd->tag_rrd = 1;
    newNode_rrd->data_rrd.list_rrd = list_rrd;
    newNode_rrd->next_rrd = NULL;
    return newNode_rrd;
}

void displayGLL_rrd(struct GLLNode_rrd* node_rrd) {
    if (node_rrd == NULL) {
        cout << "{}";
        return;
    }
    
    cout << "{";
    while (node_rrd != NULL) {
        if (node_rrd->tag_rrd == 0) {
            cout << "" << node_rrd->data_rrd.atom_rrd << "";
        } else {
            displayGLL_rrd(node_rrd->data_rrd.list_rrd);
        }
        
        if (node_rrd->next_rrd != NULL) {
            cout << ", ";
        }
        node_rrd = node_rrd->next_rrd;
    }
    cout << "}";
}

struct GLLNode_rrd* createSetExample_rrd() {

    struct GLLNode_rrd* innermostList_rrd = createAtomNode_rrd("y");
    innermostList_rrd->next_rrd = createAtomNode_rrd("z");
    

    struct GLLNode_rrd* uvList_rrd = createAtomNode_rrd("u");
    uvList_rrd->next_rrd = createAtomNode_rrd("v");
    

    struct GLLNode_rrd* nestedList_rrd = createAtomNode_rrd("r");
    struct GLLNode_rrd* current_rrd = nestedList_rrd;
    

    current_rrd->next_rrd = createAtomNode_rrd("s");
    current_rrd = current_rrd->next_rrd;
    

    current_rrd->next_rrd = createAtomNode_rrd("t");
    current_rrd = current_rrd->next_rrd;
    

    current_rrd->next_rrd = createListNode_rrd(NULL);
    current_rrd = current_rrd->next_rrd;
    

    current_rrd->next_rrd = createListNode_rrd(uvList_rrd);
    current_rrd = current_rrd->next_rrd;
    

    current_rrd->next_rrd = createAtomNode_rrd("w");
    current_rrd = current_rrd->next_rrd;
    

    current_rrd->next_rrd = createAtomNode_rrd("x");
    current_rrd = current_rrd->next_rrd;
    

    current_rrd->next_rrd = createListNode_rrd(innermostList_rrd);
    current_rrd = current_rrd->next_rrd;
    

    current_rrd->next_rrd = createAtomNode_rrd("a1");
    current_rrd = current_rrd->next_rrd;
    

    current_rrd->next_rrd = createAtomNode_rrd("b1");
    

    struct GLLNode_rrd* mainSet_rrd = createAtomNode_rrd("p");
    current_rrd = mainSet_rrd;
    

    current_rrd->next_rrd = createAtomNode_rrd("q");
    current_rrd = current_rrd->next_rrd;
    

    current_rrd->next_rrd = createListNode_rrd(nestedList_rrd);
    
    return mainSet_rrd;
}

void freeGLL_rrd(struct GLLNode_rrd* node_rrd) {
    struct GLLNode_rrd* temp_rrd;
    while (node_rrd != NULL) {
        temp_rrd = node_rrd;
        node_rrd = node_rrd->next_rrd;
        
        if (temp_rrd->tag_rrd == 1 && temp_rrd->data_rrd.list_rrd != NULL) {
            freeGLL_rrd(temp_rrd->data_rrd.list_rrd);
        }
        
        free(temp_rrd);
    }
}
```

## Output

```
Generalized Linked List Implementation of Set
============================================
Set S = {p, q, {r, s, t, {}, {u, v}, w, x, {y, z}, a1, b1}}
```

## Dry Run

1. **Create Atom Nodes**:
   - Create nodes for simple elements: p, q, r, s, t, u, v, w, x, y, z, a1, b1
   - Each node has tag=0 and stores the atom value in data.atom

2. **Create List Nodes**:
   - Create innermost list {y, z} by linking y and z atom nodes
   - Create list {u, v} by linking u and v atom nodes
   - Create nested list {r, s, t, {}, {u, v}, w, x, {y, z}, a1, b1} by linking all elements
   - For empty set {}, create a list node with NULL list pointer
   - For {u, v} and {y, z}, create list nodes pointing to their respective lists

3. **Create Main Set**:
   - Create main set {p, q, nested_list} by linking p, q, and the nested list
   - p and q are atom nodes, nested_list is a list node

4. **Display Process**:
   - Start with main set node
   - Print opening brace "{"
   - Process each node:
     * For atom nodes (p, q): print the atom value
     * For list nodes: recursively call display function
   - Print closing brace "}"

## Conclusion

The implementation demonstrates a Generalized Linked List (GLL) for representing complex nested set structures. Key features include:

1. **Flexible Structure**: GLL can represent both atomic elements and nested lists using a union data structure
2. **Memory Efficiency**: Only allocates memory for actual elements, not fixed-size arrays
3. **Recursive Nature**: Natural fit for nested structures with recursive display and memory management
4. **Tag System**: Uses tags to distinguish between atoms and lists at each node

**Time Complexities**:
- Node Creation: O(1) for each node
- Display: O(n) where n is the total number of elements (atoms and lists)
- Memory Deallocation: O(n) with recursive traversal

The GLL structure is particularly well-suited for this application because:
1. It can represent arbitrary nesting levels
2. It handles heterogeneous data (atoms and lists) in a uniform way
3. It allows efficient memory usage without predefining maximum sizes
4. The recursive structure naturally matches the recursive nature of nested sets

This implementation correctly displays the set in proper mathematical notation, showing how GLL can be used to represent complex data structures that would be difficult to model with simple linear data structures.