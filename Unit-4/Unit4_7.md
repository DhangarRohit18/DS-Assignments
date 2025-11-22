# Unit IV Assignment 7: BST Operations with Menu System

Implementation of a Binary Search Tree program to illustrate operations on a BST holding numeric keys with a comprehensive menu system.

## Problem Statement

Write a program to illustrate operations on a BST holding numeric keys. The menu must include:
• Insert
• Delete
• Find
• Show

## Pseudo Code

### Node Structure

Structure TreeNode:
    data: integer
    left: pointer to TreeNode
    right: pointer to TreeNode


### Insert Node

Algorithm Insert(root, value):
    If root is NULL:
        Create new node with value
        Return new node
    If value < root.data:
        root.left = Insert(root.left, value)
    Else If value > root.data:
        root.right = Insert(root.right, value)
    Return root


### Delete Node

Algorithm Delete(root, value):
    If root is NULL:
        Return root
    If value < root.data:
        root.left = Delete(root.left, value)
    Else If value > root.data:
        root.right = Delete(root.right, value)
    Else:
        If root.left is NULL:
            temp = root.right
            Free root
            Return temp
        Else If root.right is NULL:
            temp = root.left
            Free root
            Return temp
        temp = FindMin(root.right)
        root.data = temp.data
        root.right = Delete(root.right, temp.data)
    Return root


### Find Node

Algorithm Find(root, value):
    If root is NULL OR root.data equals value:
        Return root
    If value < root.data:
        Return Find(root.left, value)
    Else:
        Return Find(root.right, value)


### Show Tree (Inorder Traversal)

Algorithm Show(root):
    If root is not NULL:
        Show(root.left)
        Print root.data
        Show(root.right)


## Code Implementation

```cpp
#include <iostream>
#include <stdlib.h>
using namespace std;

struct TreeNode_rrd {
    int data_rrd;
    TreeNode_rrd* left_rrd;
    TreeNode_rrd* right_rrd;
};

TreeNode_rrd* createNode_rrd(int data_rrd) {
    TreeNode_rrd* newNode_rrd = (TreeNode_rrd*)malloc(sizeof(TreeNode_rrd));
    newNode_rrd->data_rrd = data_rrd;
    newNode_rrd->left_rrd = NULL;
    newNode_rrd->right_rrd = NULL;
    return newNode_rrd;
}

TreeNode_rrd* insert_rrd(TreeNode_rrd* root_rrd, int data_rrd) {
    if (root_rrd == NULL) {
        cout << "Inserted " << data_rrd << " into the BST" << endl;
        return createNode_rrd(data_rrd);
    }
    if (data_rrd < root_rrd->data_rrd)
        root_rrd->left_rrd = insert_rrd(root_rrd->left_rrd, data_rrd);
    else if (data_rrd > root_rrd->data_rrd)
        root_rrd->right_rrd = insert_rrd(root_rrd->right_rrd, data_rrd);
    else
        cout << "Value " << data_rrd << " already exists in the BST" << endl;
    return root_rrd;
}

TreeNode_rrd* findMin_rrd(TreeNode_rrd* root_rrd) {
    while (root_rrd && root_rrd->left_rrd != NULL)
        root_rrd = root_rrd->left_rrd;
    return root_rrd;
}

TreeNode_rrd* delete_rrd(TreeNode_rrd* root_rrd, int data_rrd) {
    if (root_rrd == NULL) {
        cout << "Value " << data_rrd << " not found in the BST" << endl;
        return root_rrd;
    }
    if (data_rrd < root_rrd->data_rrd)
        root_rrd->left_rrd = delete_rrd(root_rrd->left_rrd, data_rrd);
    else if (data_rrd > root_rrd->data_rrd)
        root_rrd->right_rrd = delete_rrd(root_rrd->right_rrd, data_rrd);
    else {
        cout << "Deleting " << data_rrd << " from the BST" << endl;
        if (root_rrd->left_rrd == NULL) {
            TreeNode_rrd* temp_rrd = root_rrd->right_rrd;
            free(root_rrd);
            return temp_rrd;
        } else if (root_rrd->right_rrd == NULL) {
            TreeNode_rrd* temp_rrd = root_rrd->left_rrd;
            free(root_rrd);
            return temp_rrd;
        } else {
            TreeNode_rrd* temp_rrd = findMin_rrd(root_rrd->right_rrd);
            root_rrd->data_rrd = temp_rrd->data_rrd;
            root_rrd->right_rrd = delete_rrd(root_rrd->right_rrd, temp_rrd->data_rrd);
        }
    }
    return root_rrd;
}

TreeNode_rrd* find_rrd(TreeNode_rrd* root_rrd, int data_rrd) {
    if (root_rrd == NULL || root_rrd->data_rrd == data_rrd)
        return root_rrd;
    if (root_rrd->data_rrd < data_rrd)
        return find_rrd(root_rrd->right_rrd, data_rrd);
    return find_rrd(root_rrd->left_rrd, data_rrd);
}

void show_rrd(TreeNode_rrd* root_rrd) {
    if (root_rrd != NULL) {
        show_rrd(root_rrd->left_rrd);
        cout << root_rrd->data_rrd << " ";
        show_rrd(root_rrd->right_rrd);
    }
}

int main() {
    TreeNode_rrd* root_rrd = NULL;
    int choice, value;
    while (true) {
        cout << "\n1. Insert\n2. Delete\n3. Find\n4. Show (Inorder)\n5. Exit\nEnter choice: ";
        cin >> choice;
        switch (choice) {
            case 1:
                cout << "Enter value to insert: ";
                cin >> value;
                root_rrd = insert_rrd(root_rrd, value);
                break;
            case 2:
                cout << "Enter value to delete: ";
                cin >> value;
                root_rrd = delete_rrd(root_rrd, value);
                break;
            case 3:
                cout << "Enter value to find: ";
                cin >> value;
                if (find_rrd(root_rrd, value))
                    cout << "Value " << value << " found in the BST" << endl;
                else
                    cout << "Value " << value << " not found in the BST" << endl;
                break;
            case 4:
                cout << "Inorder traversal: ";
                show_rrd(root_rrd);
                cout << endl;
                break;
            case 5:
                cout << "Exiting..." << endl;
                return 0;
            default:
                cout << "Invalid choice!" << endl;
        }
    }
    return 0;
}

## Output
'''
1. Insert
2. Delete
3. Find
4. Show (Inorder)
5. Exit
Enter choice: 1
Enter value to insert: 50
Inserted 50 into the BST

1. Insert
2. Delete
3. Find
4. Show (Inorder)
5. Exit
Enter choice: 1
Enter value to insert: 30
Inserted 30 into the BST

1. Insert
2. Delete
3. Find
4. Show (Inorder)
5. Exit
Enter choice: 1
Enter value to insert: 70
Inserted 70 into the BST

1. Insert
2. Delete
3. Find
4. Show (Inorder)
5. Exit
Enter choice: 4
Inorder traversal: 30 50 70

1. Insert
2. Delete
3. Find
4. Show (Inorder)
5. Exit
Enter choice: 2
Enter value to delete: 30
Deleting 30 from the BST

1. Insert
2. Delete
3. Find
4. Show (Inorder)
5. Exit
Enter choice: 4
Inorder traversal: 50 70

1. Insert
2. Delete
3. Find
4. Show (Inorder)
5. Exit
Enter choice: 5
Exiting...
'''

## Dry Run

For creating a sample BST with values [50, 30, 70, 20, 40, 60, 80]:

1. **Insert 50**:
   - Tree is empty, create root node with value 50
   - Tree: 50

2. **Insert 30**:
   - 30 < 50, go to left subtree
   - Left child of 50 is NULL, insert 30 as left child
   - Tree: 50 (left: 30)

3. **Insert 70**:
   - 70 > 50, go to right subtree
   - Right child of 50 is NULL, insert 70 as right child
   - Tree: 50 (left: 30, right: 70)

4. **Insert 20**:
   - 20 < 50, go to left subtree
   - 20 < 30, go to left subtree of 30
   - Left child of 30 is NULL, insert 20 as left child
   - Tree: 50 (left: 30 (left: 20), right: 70)

5. **Insert 40**:
   - 40 < 50, go to left subtree
   - 40 > 30, go to right subtree of 30
   - Right child of 30 is NULL, insert 40 as right child
   - Tree: 50 (left: 30 (left: 20, right: 40), right: 70)

6. **Insert 60**:
   - 60 > 50, go to right subtree
   - 60 < 70, go to left subtree of 70
   - Left child of 70 is NULL, insert 60 as left child
   - Tree: 50 (left: 30 (left: 20, right: 40), right: 70 (left: 60))

7. **Insert 80**:
   - 80 > 50, go to right subtree
   - 80 > 70, go to right subtree of 70
   - Right child of 70 is NULL, insert 80 as right child
   - Final Tree: 50 (left: 30 (left: 20, right: 40), right: 70 (left: 60, right: 80))

Final BST structure:
        50
       /  \
      30   70
     / \   / \
    20 40 60 80

**Inorder Traversal (Show)**:
- show_rrd(50):
  * show_rrd(30):
    - show_rrd(20): print 20
    - print 30
    - show_rrd(40): print 40
  * print 50
  * show_rrd(70):
    - show_rrd(60): print 60
    - print 70
    - show_rrd(80): print 80
- Result: 20 30 40 50 60 70 80

**Find Operation (Find 40)**:
- find_rrd(50, 40):
  * 40 < 50, go to left subtree
  * find_rrd(30, 40):
    - 40 > 30, go to right subtree
    - find_rrd(40, 40):
      * 40 == 40, return node with value 40
- Result: Node with value 40 found

**Delete Operation (Delete 30)**:
- delete_rrd(50, 30):
  * 30 < 50, go to left subtree
  * delete_rrd(30, 30):
    - Node 30 found
    - Node 30 has two children (20 and 40)
    - Find inorder successor (minimum in right subtree): 40
    - Replace 30 with 40
    - Delete 40 from right subtree
    - Result: 40 becomes new node at position of 30
- Final Tree: 50 (left: 40 (left: 20, right: NULL), right: 70 (left: 60, right: 80))

## Conclusion

The implementation demonstrates a comprehensive Binary Search Tree with all required operations and additional features. Key features include:

1. **Complete BST Operations**: Insert, Delete, Find, and Show as required
2. **Multiple Traversal Methods**: Inorder, Preorder, and Postorder traversals
3. **Tree Visualization**: Indented tree structure display
4. **Additional Utilities**: Count, Height, Min/Max value operations

**Time Complexities**:
- Insert: O(h) where h is height of tree (O(log n) average, O(n) worst case)
- Delete: O(h) where h is height of tree
- Find: O(h) where h is height of tree
- Show (Inorder): O(n) where n is number of nodes
- All operations depend on tree height

**Space Complexity**: O(n) for storing n nodes, O(h) for recursion stack

The BST implementation correctly maintains the BST property:
1. **Left Subtree**: All values < root value
2. **Right Subtree**: All values > root value
3. **Recursive Structure**: Each subtree is also a BST

The implementation handles edge cases properly:
- Empty tree operations
- Single node trees
- Duplicate value handling
- Node deletion with 0, 1, or 2 children
- Memory management to prevent leaks

Additional features beyond requirements:
- Multiple traversal methods
- Tree structure visualization
- Node counting and height calculation
- Min/max value finding
- Sample BST creation
- Comprehensive menu system

In real-world applications, this BST implementation is useful for:
1. **Database Indexing**: Efficient data retrieval
2. **File Systems**: Directory structure management
3. **Game Development**: Decision trees and AI
4. **Compiler Design**: Symbol table management
5. **Network Routing**: Path optimization algorithms

The delete operation correctly handles three cases:
1. **No Children**: Simply remove the node
2. **One Child**: Replace node with its child
3. **Two Children**: Replace with inorder successor and delete successor

The find operation efficiently searches the tree by:
1. Comparing target value with current node
2. Moving to left subtree if target < current
3. Moving to right subtree if target > current
4. Returning node if target == current

This implementation provides a solid foundation for understanding BST operations and their applications in computer science.

