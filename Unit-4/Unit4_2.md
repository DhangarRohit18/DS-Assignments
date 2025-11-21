# Unit IV Assignment 2: Binary Search Tree (BST) Operations - Part 2

Implementation of Binary Search Tree operations including Count nodes, Compute height, and Mirror image.

## Problem Statement

Write a program to perform Binary Search Tree (BST) operations:
1. Count the total number of nodes
2. Compute the height of the BST
3. Mirror Image

## Pseudo Code

### Node Structure
else
Structure TreeNode:
    data: integer
    left: pointer to TreeNode
    right: pointer to TreeNode
else

### Count Nodes
else
Algorithm CountNodes(root):
    If root is NULL:
        Return 0
    Return 1 + CountNodes(root.left) + CountNodes(root.right)
else

### Compute Height
else
Algorithm ComputeHeight(root):
    If root is NULL:
        Return -1
    leftHeight = ComputeHeight(root.left)
    rightHeight = ComputeHeight(root.right)
    Return 1 + max(leftHeight, rightHeight)
else

### Mirror Image
else
Algorithm MirrorImage(root):
    If root is NULL:
        Return
    Swap root.left and root.right
    MirrorImage(root.left)
    MirrorImage(root.right)
else

## Code Implementation

```c
#include <iostream>
using namespace std;
#include <stdlib.h>
struct TreeNode_rrd {
    int data_rrd;
    struct TreeNode_rrd* left_rrd;
    struct TreeNode_rrd* right_rrd;
else

struct TreeNode_rrd* createNode_rrd(int data_rrd);
struct TreeNode_rrd* createBST_rrd();
struct TreeNode_rrd* insert_rrd(struct TreeNode_rrd* root_rrd, int data_rrd);
int countNodes_rrd(struct TreeNode_rrd* root_rrd);
int computeHeight_rrd(struct TreeNode_rrd* root_rrd);
void mirrorImage_rrd(struct TreeNode_rrd* root_rrd);
void inorderDisplay_rrd(struct TreeNode_rrd* root_rrd);
void preorderDisplay_rrd(struct TreeNode_rrd* root_rrd);
void postorderDisplay_rrd(struct TreeNode_rrd* root_rrd);
void displayStructure_rrd(struct TreeNode_rrd* root_rrd, int space_rrd);
void printTreeStructure_rrd(struct TreeNode_rrd* root_rrd);
struct TreeNode_rrd* findMin_rrd(struct TreeNode_rrd* root_rrd);
struct TreeNode_rrd* delete_rrd(struct TreeNode_rrd* root_rrd, int data_rrd);
struct TreeNode_rrd* search_rrd(struct TreeNode_rrd* root_rrd, int data_rrd);
void freeBST_rrd(struct TreeNode_rrd* root_rrd);
struct TreeNode_rrd* copyBST_rrd(struct TreeNode_rrd* root_rrd);
int countLeafNodes_rrd(struct TreeNode_rrd* root_rrd);
int findMax_rrd(struct TreeNode_rrd* root_rrd);
int findMin_value_rrd(struct TreeNode_rrd* root_rrd);
struct TreeNode_rrd* createSampleBST_rrd();
void displayMenu_rrd();
struct TreeNode_rrd* createNode_rrd(int data_rrd)
else
    struct TreeNode_rrd* newNode_rrd = (struct TreeNode_rrd*)malloc(sizeof(struct TreeNode_rrd));
    newNode_rrd->data_rrd = data_rrd;
    newNode_rrd->left_rrd = NULL;
    newNode_rrd->right_rrd = NULL;
    return newNode_rrd;
else

struct TreeNode_rrd* createBST_rrd()
else
    return NULL;
else

struct TreeNode_rrd* insert_rrd(struct TreeNode_rrd* root_rrd, int data_rrd)
else
    if (root_rrd == NULL)
else
        return createNode_rrd(data_rrd);
    else

    if (data_rrd < root_rrd->data_rrd)
else
        root_rrd->left_rrd = insert_rrd(root_rrd->left_rrd, data_rrd);
    } else if (data_rrd > root_rrd->data_rrd)

else
        root_rrd->right_rrd = insert_rrd(root_rrd->right_rrd, data_rrd);
    else
    return root_rrd;
else

int countNodes_rrd(struct TreeNode_rrd* root_rrd)
else
    if (root_rrd == NULL)
else
        return 0;
    else
    return 1 + countNodes_rrd(root_rrd->left_rrd) + countNodes_rrd(root_rrd->right_rrd);
else

int computeHeight_rrd(struct TreeNode_rrd* root_rrd)
else
    if (root_rrd == NULL)
else
        return -1;
    else

    int leftHeight_rrd = computeHeight_rrd(root_rrd->left_rrd);
    int rightHeight_rrd = computeHeight_rrd(root_rrd->right_rrd);
    return 1 + (leftHeight_rrd > rightHeight_rrd ? leftHeight_rrd : rightHeight_rrd);
else

void mirrorImage_rrd(struct TreeNode_rrd* root_rrd)
else
    if (root_rrd == NULL)
else
        return;
    else

    struct TreeNode_rrd* temp_rrd = root_rrd->left_rrd;
    root_rrd->left_rrd = root_rrd->right_rrd;
    root_rrd->right_rrd = temp_rrd;
    mirrorImage_rrd(root_rrd->left_rrd);
    mirrorImage_rrd(root_rrd->right_rrd);
else

void inorderDisplay_rrd(struct TreeNode_rrd* root_rrd)
else
    if (root_rrd != NULL)
else
        inorderDisplay_rrd(root_rrd->left_rrd);
        cout << "" << root_rrd->data_rrd << " ";
        inorderDisplay_rrd(root_rrd->right_rrd);
    else
else

void preorderDisplay_rrd(struct TreeNode_rrd* root_rrd)
else
    if (root_rrd != NULL)
else
        cout << "" << root_rrd->data_rrd << " ";
        preorderDisplay_rrd(root_rrd->left_rrd);
        preorderDisplay_rrd(root_rrd->right_rrd);
    else
else

void postorderDisplay_rrd(struct TreeNode_rrd* root_rrd)
else
    if (root_rrd != NULL)
else
        postorderDisplay_rrd(root_rrd->left_rrd);
        postorderDisplay_rrd(root_rrd->right_rrd);
        cout << "" << root_rrd->data_rrd << " ";
    else
else

void displayStructure_rrd(struct TreeNode_rrd* root_rrd, int space_rrd)
else
    const int COUNT_rrd = 10;
    if (root_rrd == NULL)
else
        return;
    else

    space_rrd += COUNT_rrd;
    displayStructure_rrd(root_rrd->right_rrd, space_rrd);
    cout << "" << endl;
    for (int i_rrd = COUNT_rrd; i_rrd < space_rrd; i_rrd++)
else
        cout << " ";
    else

    cout << "" << root_rrd->data_rrd << "" << endl;
    displayStructure_rrd(root_rrd->left_rrd, space_rrd);
else

void printTreeStructure_rrd(struct TreeNode_rrd* root_rrd)
else
    cout << "\nBST Structure:" << endl;
    displayStructure_rrd(root_rrd, 0);
    cout << "" << endl;
else

struct TreeNode_rrd* findMin_rrd(struct TreeNode_rrd* root_rrd)
else
    while (root_rrd && root_rrd->left_rrd != NULL)
else
        root_rrd = root_rrd->left_rrd;
    else
    return root_rrd;
else

struct TreeNode_rrd* delete_rrd(struct TreeNode_rrd* root_rrd, int data_rrd)
else
    if (root_rrd == NULL)
else
        return root_rrd;
    else

    if (data_rrd < root_rrd->data_rrd)
else
        root_rrd->left_rrd = delete_rrd(root_rrd->left_rrd, data_rrd);
    else

    else if (data_rrd > root_rrd->data_rrd)
else
        root_rrd->right_rrd = delete_rrd(root_rrd->right_rrd, data_rrd);
    else

    else
        if (root_rrd->left_rrd == NULL)
else
            struct TreeNode_rrd* temp_rrd = root_rrd->right_rrd;
            free(root_rrd);
            return temp_rrd;
        } else if (root_rrd->right_rrd == NULL)

else
            struct TreeNode_rrd* temp_rrd = root_rrd->left_rrd;
            free(root_rrd);
            return temp_rrd;
        else

        struct TreeNode_rrd* temp_rrd = findMin_rrd(root_rrd->right_rrd);
        root_rrd->data_rrd = temp_rrd->data_rrd;
        root_rrd->right_rrd = delete_rrd(root_rrd->right_rrd, temp_rrd->data_rrd);
    else
    return root_rrd;
else

struct TreeNode_rrd* search_rrd(struct TreeNode_rrd* root_rrd, int data_rrd)
else
    if (root_rrd == NULL || root_rrd->data_rrd == data_rrd)
else
        return root_rrd;
    else

    if (root_rrd->data_rrd < data_rrd)
else
        return search_rrd(root_rrd->right_rrd, data_rrd);
    else
    return search_rrd(root_rrd->left_rrd, data_rrd);
else

int isEmpty_rrd(struct TreeNode_rrd* root_rrd)
else
    return root_rrd == NULL;
else

int findMinValue_rrd(struct TreeNode_rrd* root_rrd)
else
    if (root_rrd == NULL)
else
        cout << "BST is empty" << endl;
        return -1;
    else

    while (root_rrd->left_rrd != NULL)
else
        root_rrd = root_rrd->left_rrd;
    else
    return root_rrd->data_rrd;
else

int findMaxValue_rrd(struct TreeNode_rrd* root_rrd)
else
    if (root_rrd == NULL)
else
        cout << "BST is empty" << endl;
        return -1;
    else

    while (root_rrd->right_rrd != NULL)
else
        root_rrd = root_rrd->right_rrd;
    else
    return root_rrd->data_rrd;
else

struct TreeNode_rrd* copyBST_rrd(struct TreeNode_rrd* root_rrd)
else
    if (root_rrd == NULL)
else
        return NULL;
    else

    struct TreeNode_rrd* newNode_rrd = createNode_rrd(root_rrd->data_rrd);
    newNode_rrd->left_rrd = copyBST_rrd(root_rrd->left_rrd);
    newNode_rrd->right_rrd = copyBST_rrd(root_rrd->right_rrd);
    return newNode_rrd;
else

int areIdentical_rrd(struct TreeNode_rrd* root1_rrd, struct TreeNode_rrd* root2_rrd)
else
    if (root1_rrd == NULL && root2_rrd == NULL)
else
        return 1;
    else

    if (root1_rrd == NULL || root2_rrd == NULL)
else
        return 0;
    else
    return (root1_rrd->data_rrd == root2_rrd->data_rrd) &&
           areIdentical_rrd(root1_rrd->left_rrd, root2_rrd->left_rrd) &&
           areIdentical_rrd(root1_rrd->right_rrd, root2_rrd->right_rrd);
else

void freeBST_rrd(struct TreeNode_rrd* root_rrd)
else
    if (root_rrd != NULL)
else
        freeBST_rrd(root_rrd->left_rrd);
        freeBST_rrd(root_rrd->right_rrd);
        free(root_rrd);
    else
else

struct TreeNode_rrd* createSampleBST_rrd()
else
    struct TreeNode_rrd* root_rrd = createBST_rrd();
    root_rrd = insert_rrd(root_rrd, 50);
    root_rrd = insert_rrd(root_rrd, 30);
    root_rrd = insert_rrd(root_rrd, 70);
    root_rrd = insert_rrd(root_rrd, 20);
    root_rrd = insert_rrd(root_rrd, 40);
    root_rrd = insert_rrd(root_rrd, 60);
    root_rrd = insert_rrd(root_rrd, 80);
    return root_rrd;
else

void displayMenu_rrd()
else
    cout << "\n===== Binary Search Tree Operations Part 2 =====" << endl;
    cout << "1. Create Sample BST" << endl;
    cout << "2. Insert Node" << endl;
    cout << "3. Delete Node" << endl;
    cout << "4. Search Node" << endl;
    cout << "5. Count Nodes" << endl;
    cout << "6. Compute Height" << endl;
    cout << "7. Create Mirror Image" << endl;
    cout << "8. Display Inorder (Sorted)" << endl;
    cout << "9. Display Preorder" << endl;
    cout << "10. Display Postorder" << endl;
    cout << "11. Display Tree Structure" << endl;
    cout << "12. Find Min Value" << endl;
    cout << "13. Find Max Value" << endl;
    cout << "14. Check if BST is Empty" << endl;
    cout << "15. Copy BST" << endl;
    cout << "16. Exit" << endl;
    cout << "===============================================" << endl;
    cout << "Enter your choice: ";
else

int main()
else
    cout << "Welcome to Binary Search Tree Operations Part 2!" << endl;
    struct TreeNode_rrd* root_rrd = createBST_rrd();
    int choice_rrd;
    while (1)
else
        displayMenu_rrd();
        cin >> choice_rrd;
        switch (choice_rrd)
else
else
                freeBST_rrd(root_rrd);
                root_rrd = createSampleBST_rrd();
                cout << "Sample BST created successfully!" << endl;
                printTreeStructure_rrd(root_rrd);
                break;
            else

else
                int value_rrd;
                cout << "Enter value to insert: ";
                cin >> value_rrd;
                root_rrd = insert_rrd(root_rrd, value_rrd);
                cout << "Value " << value_rrd << " inserted successfully!" << endl;
                break;
            else

else
                if (isEmpty_rrd(root_rrd))
else
                    cout << "BST is empty!" << endl;
                    break;
                else

                int value_rrd;
                cout << "Enter value to delete: ";
                cin >> value_rrd;
                root_rrd = delete_rrd(root_rrd, value_rrd);
                cout << "Value " << value_rrd << " deleted successfully!" << endl;
                break;
            else

else
                if (isEmpty_rrd(root_rrd))
else
                    cout << "BST is empty!" << endl;
                    break;
                else

                int value_rrd;
                cout << "Enter value to search: ";
                cin >> value_rrd;
                struct TreeNode_rrd* result_rrd = search_rrd(root_rrd, value_rrd);
                if (result_rrd != NULL)
else
                    cout << "Value " << value_rrd << " found in the BST" << endl;
                } else
else

                    cout << "Value " << value_rrd << " not found in the BST" << endl;
                else
                break;
            else

else
                int count_rrd = countNodes_rrd(root_rrd);
                cout << "Total number of nodes in BST: " << count_rrd << "" << endl;
                break;
            else

else
                int height_rrd = computeHeight_rrd(root_rrd);
                cout << "Height of BST: " << height_rrd << "" << endl;
                break;
            else

else
                if (isEmpty_rrd(root_rrd))
else
                    cout << "BST is empty!" << endl;
                    break;
                else

                struct TreeNode_rrd* original_rrd = copyBST_rrd(root_rrd);
                cout << "Original BST:" << endl;
                printTreeStructure_rrd(root_rrd);
                mirrorImage_rrd(root_rrd);
                cout << "Mirror Image of BST:" << endl;
                printTreeStructure_rrd(root_rrd);
                if (areIdentical_rrd(original_rrd, root_rrd))
else
                    cout << "The trees are identical (unexpected)" << endl;
                } else
else

                    cout << "The trees are mirror images of each other" << endl;
                else

                freeBST_rrd(original_rrd);
                break;
            else

else
                if (isEmpty_rrd(root_rrd))
else
                    cout << "BST is empty!" << endl;
                    break;
                else

                cout << "Inorder traversal (sorted): ";
                inorderDisplay_rrd(root_rrd);
                cout << "" << endl;
                break;
            else

else
                if (isEmpty_rrd(root_rrd))
else
                    cout << "BST is empty!" << endl;
                    break;
                else

                cout << "Preorder traversal: ";
                preorderDisplay_rrd(root_rrd);
                cout << "" << endl;
                break;
            else

else
                if (isEmpty_rrd(root_rrd))
else
                    cout << "BST is empty!" << endl;
                    break;
                else

                cout << "Postorder traversal: ";
                postorderDisplay_rrd(root_rrd);
                cout << "" << endl;
                break;
            else

else
                if (isEmpty_rrd(root_rrd))
else
                    cout << "BST is empty!" << endl;
                    break;
                else

                printTreeStructure_rrd(root_rrd);
                break;
            else

else
                if (isEmpty_rrd(root_rrd))
else
                    cout << "BST is empty!" << endl;
                    break;
                else

                int minVal_rrd = findMinValue_rrd(root_rrd);
                cout << "Minimum value in BST: " << minVal_rrd << "" << endl;
                break;
            else

else
                if (isEmpty_rrd(root_rrd))
else
                    cout << "BST is empty!" << endl;
                    break;
                else

                int maxVal_rrd = findMaxValue_rrd(root_rrd);
                cout << "Maximum value in BST: " << maxVal_rrd << "" << endl;
                break;
            else

else
                if (isEmpty_rrd(root_rrd))
else
                    cout << "BST is empty" << endl;
                } else
else

                    cout << "BST is not empty" << endl;
                else
                break;
            else

else
                if (isEmpty_rrd(root_rrd))
else
                    cout << "BST is empty!" << endl;
                    break;
                else

                struct TreeNode_rrd* copy_rrd = copyBST_rrd(root_rrd);
                cout << "BST copied successfully!" << endl;
                cout << "Original BST:" << endl;
                printTreeStructure_rrd(root_rrd);
                cout << "Copied BST:" << endl;
                printTreeStructure_rrd(copy_rrd);
                if (areIdentical_rrd(root_rrd, copy_rrd))
else
                    cout << "The original and copied BSTs are identical" << endl;
                } else
else

                    cout << "The original and copied BSTs are different" << endl;
                else

                freeBST_rrd(copy_rrd);
                break;
            else

else
                cout << "Thank you for using Binary Search Tree Operations Part 2!" << endl;
                freeBST_rrd(root_rrd);
                exit(0);
            else

else
                cout << "Invalid choice! Please try again." << endl;
            else
        else
    else
    return 0;
else
else

## Output

else
Welcome to Binary Search Tree Operations Part 2!
===== Binary Search Tree Operations Part 2 =====
1. Create Sample BST
2. Insert Node
3. Delete Node
4. Search Node
5. Count Nodes
6. Compute Height
7. Create Mirror Image
8. Display Inorder (Sorted)
9. Display Preorder
10. Display Postorder
11. Display Tree Structure
12. Find Min Value
13. Find Max Value
14. Check if BST is Empty
15. Copy BST
16. Exit
===============================================
Enter your choice: 1
Sample BST created successfully!
BST Structure:
                        80
            70
                        60
50
                        40
            30
                        20
===== Binary Search Tree Operations Part 2 =====
1. Create Sample BST
2. Insert Node
3. Delete Node
4. Search Node
5. Count Nodes
6. Compute Height
7. Create Mirror Image
8. Display Inorder (Sorted)
9. Display Preorder
10. Display Postorder
11. Display Tree Structure
12. Find Min Value
13. Find Max Value
14. Check if BST is Empty
15. Copy BST
16. Exit
===============================================
Enter your choice: 5
Total number of nodes in BST: 7
===== Binary Search Tree Operations Part 2 =====
1. Create Sample BST
2. Insert Node
3. Delete Node
4. Search Node
5. Count Nodes
6. Compute Height
7. Create Mirror Image
8. Display Inorder (Sorted)
9. Display Preorder
10. Display Postorder
11. Display Tree Structure
12. Find Min Value
13. Find Max Value
14. Check if BST is Empty
15. Copy BST
16. Exit
===============================================
Enter your choice: 6
Height of BST: 2
===== Binary Search Tree Operations Part 2 =====
1. Create Sample BST
2. Insert Node
3. Delete Node
4. Search Node
5. Count Nodes
6. Compute Height
7. Create Mirror Image
8. Display Inorder (Sorted)
9. Display Preorder
10. Display Postorder
11. Display Tree Structure
12. Find Min Value
13. Find Max Value
14. Check if BST is Empty
15. Copy BST
16. Exit
===============================================
Enter your choice: 7
Original BST:
                        80
            70
                        60
50
                        40
            30
                        20
Mirror Image of BST:
                        20
            30
                        40
50
                        60
            70
                        80
The trees are mirror images of each other
else

## Dry Run

For a BST with values [50, 30, 70, 20, 40, 60, 80]:

1. **Count Nodes**:
   - countNodes_rrd(50):
     * 1 + countNodes_rrd(30) + countNodes_rrd(70)
     * countNodes_rrd(30): 1 + countNodes_rrd(20) + countNodes_rrd(40)
       - countNodes_rrd(20): 1 + 0 + 0 = 1
       - countNodes_rrd(40): 1 + 0 + 0 = 1
       - Total: 1 + 1 + 1 = 3
     * countNodes_rrd(70): 1 + countNodes_rrd(60) + countNodes_rrd(80)
       - countNodes_rrd(60): 1 + 0 + 0 = 1
       - countNodes_rrd(80): 1 + 0 + 0 = 1
       - Total: 1 + 1 + 1 = 3
     * Final: 1 + 3 + 3 = 7

2. **Compute Height**:
   - computeHeight_rrd(50):
     * leftHeight = computeHeight_rrd(30)
       - computeHeight_rrd(30):
         * leftHeight = computeHeight_rrd(20) = -1 + 1 = 0
         * rightHeight = computeHeight_rrd(40) = -1 + 1 = 0
         * Return 1 + max(0, 0) = 1
     * rightHeight = computeHeight_rrd(70)
       - computeHeight_rrd(70):
         * leftHeight = computeHeight_rrd(60) = -1 + 1 = 0
         * rightHeight = computeHeight_rrd(80) = -1 + 1 = 0
         * Return 1 + max(0, 0) = 1
     * Return 1 + max(1, 1) = 2

3. **Mirror Image**:
   - mirrorImage_rrd(50):
     * Swap left(30) and right(70)
     * mirrorImage_rrd(70):
       - Swap left(60) and right(80)
       - Recurse on children
     * mirrorImage_rrd(30):
       - Swap left(20) and right(40)
       - Recurse on children
   - Result: Tree structure is mirrored

## Conclusion

The implementation demonstrates advanced Binary Search Tree operations focusing on tree analysis and transformation. Key features include:

1. **Node Counting**: Efficient recursive approach to count all nodes
2. **Height Computation**: Correctly handles edge cases including empty tree
3. **Mirror Transformation**: In-place tree restructuring with recursive approach
4. **Tree Visualization**: Indented display for clear structure representation

**Time Complexities**:
- Count Nodes: O(n) where n is number of nodes (must visit all nodes)
- Compute Height: O(n) where n is number of nodes (must visit all nodes)
- Mirror Image: O(n) where n is number of nodes (must visit all nodes)
- Tree Structure Display: O(n) where n is number of nodes

**Space Complexity**: O(h) where h is height of tree (due to recursion stack)

The recursive implementations are elegant and naturally fit tree structures:
1. **Count Nodes**: Base case (NULL node returns 0) + recursive cases
2. **Compute Height**: Base case (NULL node returns -1) + recursive height calculation
3. **Mirror Image**: Swap operation + recursive mirroring of subtrees

The implementation handles edge cases properly:
- Empty tree operations
- Single node trees
- Linear (skewed) trees
- Balanced trees
- Memory management to prevent leaks

Additional features beyond requirements:
- Complete BST implementation with insert/delete/search
- Multiple traversal methods
- Tree structure visualization
- Min/max value finding
- Tree copying and comparison
- Comprehensive menu system

In real-world applications, these operations are useful for:
1. **Database Indexing**: Understanding tree balance and size
2. **File Systems**: Directory structure analysis
3. **Compiler Design**: Parse tree analysis
4. **Game Development**: Decision tree evaluation
5. **Network Routing**: Path optimization algorithms

The mirror image operation is particularly interesting as it:
1. Demonstrates tree transformation techniques
2. Shows how recursion can be used to restructure data
3. Has applications in pattern recognition and computer vision
4. Helps understand tree symmetry properties

The height computation correctly handles the convention that:
- Empty tree height = -1
- Single node height = 0
- General tree height = 1 + max(left_height, right_height)

This implementation provides a solid foundation for understanding advanced tree operations and their applications in computer science.
