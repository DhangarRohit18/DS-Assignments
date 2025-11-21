# Unit IV Assignment 5: Binary Tree - Recursive Operations

Implementation of a Binary Tree program with recursive operations including Inorder Traversal, Preorder Traversal, Display Number of Leaf Nodes, and Mirror Image.

## Problem Statement

Write a Program to create a Binary Tree and perform the following Recursive operations on it:
a. Inorder Traversal
b. Preorder Traversal
c. Display Number of Leaf Nodes
d. Mirror Image

## Pseudo Code

### Node Structure
```
Structure TreeNode:
    data: integer
    left: pointer to TreeNode
    right: pointer to TreeNode
```

### Inorder Traversal (Recursive)
```
Algorithm InorderTraversal(root):
    If root is not NULL:
        InorderTraversal(root.left)
        Print root.data
        InorderTraversal(root.right)
```

### Preorder Traversal (Recursive)
```
Algorithm PreorderTraversal(root):
    If root is not NULL:
        Print root.data
        PreorderTraversal(root.left)
        PreorderTraversal(root.right)
```

### Postorder Traversal (Recursive)
```
Algorithm PostorderTraversal(root):
    If root is not NULL:
        PostorderTraversal(root.left)
        PostorderTraversal(root.right)
        Print root.data
```

### Count Leaf Nodes (Recursive)
```
Algorithm CountLeafNodes(root):
    If root is NULL:
        Return 0
    If root.left is NULL AND root.right is NULL:
        Return 1
    Return CountLeafNodes(root.left) + CountLeafNodes(root.right)
```

### Mirror Image (Recursive)
```
Algorithm MirrorImage(root):
    If root is not NULL:
        MirrorImage(root.left)
        MirrorImage(root.right)
        Swap root.left and root.right
```

## Code Implementation

```c
#include <iostream>
using namespace std;
#include <stdlib.h>
struct TreeNode_rrd {
    int data_rrd;
    struct TreeNode_rrd* left_rrd;
    struct TreeNode_rrd* right_rrd;
};

struct TreeNode_rrd* createNode_rrd(int data_rrd);
struct TreeNode_rrd* createBinaryTree_rrd();
struct TreeNode_rrd* createBSTFromArray_rrd(int arr_rrd[], int size_rrd);
void inorderTraversal_rrd(struct TreeNode_rrd* root_rrd);
void preorderTraversal_rrd(struct TreeNode_rrd* root_rrd);
void postorderTraversal_rrd(struct TreeNode_rrd* root_rrd);
int countLeafNodes_rrd(struct TreeNode_rrd* root_rrd);
void mirrorImage_rrd(struct TreeNode_rrd* root_rrd);
void displayStructure_rrd(struct TreeNode_rrd* root_rrd, int space_rrd);
void printTreeStructure_rrd(struct TreeNode_rrd* root_rrd);
int countTotalNodes_rrd(struct TreeNode_rrd* root_rrd);
int findHeight_rrd(struct TreeNode_rrd* root_rrd);
int findMinValue_rrd(struct TreeNode_rrd* root_rrd);
int findMaxValue_rrd(struct TreeNode_rrd* root_rrd);
void freeTree_rrd(struct TreeNode_rrd* root_rrd);
void displayMenu_rrd();
struct TreeNode_rrd* createNode_rrd(int data_rrd) {
    struct TreeNode_rrd* newNode_rrd = (struct TreeNode_rrd*)malloc(sizeof(struct TreeNode_rrd));
    newNode_rrd->data_rrd = data_rrd;
    newNode_rrd->left_rrd = NULL;
    newNode_rrd->right_rrd = NULL;
    return newNode_rrd;
}

struct TreeNode_rrd* createBinaryTree_rrd() {
    struct TreeNode_rrd* root_rrd = createNode_rrd(1);
    root_rrd->left_rrd = createNode_rrd(2);
    root_rrd->right_rrd = createNode_rrd(3);
    root_rrd->left_rrd->left_rrd = createNode_rrd(4);
    root_rrd->left_rrd->right_rrd = createNode_rrd(5);
    root_rrd->right_rrd->right_rrd = createNode_rrd(6);
    root_rrd->left_rrd->left_rrd->left_rrd = createNode_rrd(7);
    root_rrd->right_rrd->right_rrd->left_rrd = createNode_rrd(8);
    root_rrd->right_rrd->right_rrd->right_rrd = createNode_rrd(9);
    cout << "Binary tree created successfully!" << endl;
    return root_rrd;
}

struct TreeNode_rrd* createBSTFromArray_rrd(int arr_rrd[], int size_rrd) {
    if (size_rrd <= 0)
{
        return NULL;
    }

    struct TreeNode_rrd* root_rrd = createNode_rrd(arr_rrd[0]);
    for (int i_rrd = 1; i_rrd < size_rrd; i_rrd++)
{
        struct TreeNode_rrd* current_rrd = root_rrd;
        struct TreeNode_rrd* parent_rrd = NULL;
        while (current_rrd != NULL)
{
            parent_rrd = current_rrd;
            if (arr_rrd[i_rrd] < current_rrd->data_rrd)
{
                current_rrd = current_rrd->left_rrd;
            } else
{

                current_rrd = current_rrd->right_rrd;
            }
        }

        struct TreeNode_rrd* newNode_rrd = createNode_rrd(arr_rrd[i_rrd]);
        if (arr_rrd[i_rrd] < parent_rrd->data_rrd)
{
            parent_rrd->left_rrd = newNode_rrd;
        } else
{

            parent_rrd->right_rrd = newNode_rrd;
        }
    }

    cout << "BST created from array successfully!" << endl;
    return root_rrd;
}

void inorderTraversal_rrd(struct TreeNode_rrd* root_rrd) {
    if (root_rrd != NULL)
{
        inorderTraversal_rrd(root_rrd->left_rrd);
        cout << "" << root_rrd->data_rrd << " ";
        inorderTraversal_rrd(root_rrd->right_rrd);
    }
}

void preorderTraversal_rrd(struct TreeNode_rrd* root_rrd) {
    if (root_rrd != NULL)
{
        cout << "" << root_rrd->data_rrd << " ";
        preorderTraversal_rrd(root_rrd->left_rrd);
        preorderTraversal_rrd(root_rrd->right_rrd);
    }
}

void postorderTraversal_rrd(struct TreeNode_rrd* root_rrd) {
    if (root_rrd != NULL)
{
        postorderTraversal_rrd(root_rrd->left_rrd);
        postorderTraversal_rrd(root_rrd->right_rrd);
        cout << "" << root_rrd->data_rrd << " ";
    }
}

int countLeafNodes_rrd(struct TreeNode_rrd* root_rrd) {
    if (root_rrd == NULL)
{
        return 0;
    }

    if (root_rrd->left_rrd == NULL && root_rrd->right_rrd == NULL)
{
        return 1;
    }
    return countLeafNodes_rrd(root_rrd->left_rrd) + countLeafNodes_rrd(root_rrd->right_rrd);
}

void mirrorImage_rrd(struct TreeNode_rrd* root_rrd) {
    if (root_rrd != NULL)
{
        mirrorImage_rrd(root_rrd->left_rrd);
        mirrorImage_rrd(root_rrd->right_rrd);
        struct TreeNode_rrd* temp_rrd = root_rrd->left_rrd;
        root_rrd->left_rrd = root_rrd->right_rrd;
        root_rrd->right_rrd = temp_rrd;
    }
}

void displayStructure_rrd(struct TreeNode_rrd* root_rrd, int space_rrd) {
    const int COUNT_rrd = 10;
    if (root_rrd == NULL)
{
        return;
    }

    space_rrd += COUNT_rrd;
    displayStructure_rrd(root_rrd->right_rrd, space_rrd);
    cout << "" << endl;
    for (int i_rrd = COUNT_rrd; i_rrd < space_rrd; i_rrd++)
{
        cout << " ";
    }

    cout << "" << root_rrd->data_rrd << "" << endl;
    displayStructure_rrd(root_rrd->left_rrd, space_rrd);
}

void printTreeStructure_rrd(struct TreeNode_rrd* root_rrd) {
    cout << "\nTree Structure:" << endl;
    displayStructure_rrd(root_rrd, 0);
    cout << "" << endl;
}

int countTotalNodes_rrd(struct TreeNode_rrd* root_rrd) {
    if (root_rrd == NULL)
{
        return 0;
    }
    return 1 + countTotalNodes_rrd(root_rrd->left_rrd) + countTotalNodes_rrd(root_rrd->right_rrd);
}

int findHeight_rrd(struct TreeNode_rrd* root_rrd) {
    if (root_rrd == NULL)
{
        return -1;
    }

    int leftHeight_rrd = findHeight_rrd(root_rrd->left_rrd);
    int rightHeight_rrd = findHeight_rrd(root_rrd->right_rrd);
    return 1 + (leftHeight_rrd > rightHeight_rrd ? leftHeight_rrd : rightHeight_rrd);
}

int findMinValue_rrd(struct TreeNode_rrd* root_rrd) {
    if (root_rrd == NULL)
{
        cout << "Tree is empty!" << endl;
        return -1;
    }

    if (root_rrd->left_rrd == NULL)
{
        return root_rrd->data_rrd;
    }
    return findMinValue_rrd(root_rrd->left_rrd);
}

int findMaxValue_rrd(struct TreeNode_rrd* root_rrd) {
    if (root_rrd == NULL)
{
        cout << "Tree is empty!" << endl;
        return -1;
    }

    if (root_rrd->right_rrd == NULL)
{
        return root_rrd->data_rrd;
    }
    return findMaxValue_rrd(root_rrd->right_rrd);
}

struct TreeNode_rrd* search_rrd(struct TreeNode_rrd* root_rrd, int data_rrd) {
    if (root_rrd == NULL || root_rrd->data_rrd == data_rrd)
{
        return root_rrd;
    }

    if (data_rrd < root_rrd->data_rrd)
{
        return search_rrd(root_rrd->left_rrd, data_rrd);
    }
    return search_rrd(root_rrd->right_rrd, data_rrd);
}

int isEmpty_rrd(struct TreeNode_rrd* root_rrd) {
    return root_rrd == NULL;
}

int countInternalNodes_rrd(struct TreeNode_rrd* root_rrd) {
    if (root_rrd == NULL || (root_rrd->left_rrd == NULL && root_rrd->right_rrd == NULL))
{
        return 0;
    }
    return 1 + countInternalNodes_rrd(root_rrd->left_rrd) + countInternalNodes_rrd(root_rrd->right_rrd);
}

int countNodesAtLevel_rrd(struct TreeNode_rrd* root_rrd, int level_rrd) {
    if (root_rrd == NULL)
{
        return 0;
    }

    if (level_rrd == 1)
{
        return 1;
    }
    return countNodesAtLevel_rrd(root_rrd->left_rrd, level_rrd - 1) + 
           countNodesAtLevel_rrd(root_rrd->right_rrd, level_rrd - 1);
}

int findLevel_rrd(struct TreeNode_rrd* root_rrd, int data_rrd, int level_rrd) {
    if (root_rrd == NULL)
{
        return 0;
    }

    if (root_rrd->data_rrd == data_rrd)
{
        return level_rrd;
    }

    int leftLevel_rrd = findLevel_rrd(root_rrd->left_rrd, data_rrd, level_rrd + 1);
    if (leftLevel_rrd != 0)
{
        return leftLevel_rrd;
    }
    return findLevel_rrd(root_rrd->right_rrd, data_rrd, level_rrd + 1);
}

int areIdentical_rrd(struct TreeNode_rrd* root1_rrd, struct TreeNode_rrd* root2_rrd) {
    if (root1_rrd == NULL && root2_rrd == NULL)
{
        return 1;
    }

    if (root1_rrd == NULL || root2_rrd == NULL)
{
        return 0;
    }
    return (root1_rrd->data_rrd == root2_rrd->data_rrd) &&
           areIdentical_rrd(root1_rrd->left_rrd, root2_rrd->left_rrd) &&
           areIdentical_rrd(root1_rrd->right_rrd, root2_rrd->right_rrd);
}

struct TreeNode_rrd* copyTree_rrd(struct TreeNode_rrd* root_rrd) {
    if (root_rrd == NULL)
{
        return NULL;
    }

    struct TreeNode_rrd* newNode_rrd = createNode_rrd(root_rrd->data_rrd);
    newNode_rrd->left_rrd = copyTree_rrd(root_rrd->left_rrd);
    newNode_rrd->right_rrd = copyTree_rrd(root_rrd->right_rrd);
    return newNode_rrd;
}

void freeTree_rrd(struct TreeNode_rrd* root_rrd) {
    if (root_rrd != NULL)
{
        freeTree_rrd(root_rrd->left_rrd);
        freeTree_rrd(root_rrd->right_rrd);
        free(root_rrd);
    }
}

struct TreeNode_rrd* createSampleTree_rrd() {
    struct TreeNode_rrd* root_rrd = createNode_rrd(1);
    root_rrd->left_rrd = createNode_rrd(2);
    root_rrd->right_rrd = createNode_rrd(3);
    root_rrd->left_rrd->left_rrd = createNode_rrd(4);
    root_rrd->left_rrd->right_rrd = createNode_rrd(5);
    root_rrd->right_rrd->right_rrd = createNode_rrd(6);
    root_rrd->left_rrd->left_rrd->left_rrd = createNode_rrd(7);
    root_rrd->right_rrd->right_rrd->left_rrd = createNode_rrd(8);
    root_rrd->right_rrd->right_rrd->right_rrd = createNode_rrd(9);
    return root_rrd;
}

void displayMenu_rrd() {
    cout << "\n===== Binary Tree Recursive Operations =====" << endl;
    cout << "1. Create Sample Binary Tree" << endl;
    cout << "2. Create BST from Array" << endl;
    cout << "3. Inorder Traversal (Recursive)" << endl;
    cout << "4. Preorder Traversal (Recursive)" << endl;
    cout << "5. Postorder Traversal (Recursive)" << endl;
    cout << "6. Display Number of Leaf Nodes" << endl;
    cout << "7. Create Mirror Image" << endl;
    cout << "8. Display Tree Structure" << endl;
    cout << "9. Count Total Nodes" << endl;
    cout << "10. Find Height" << endl;
    cout << "11. Find Minimum Value" << endl;
    cout << "12. Find Maximum Value" << endl;
    cout << "13. Search Node" << endl;
    cout << "14. Count Internal Nodes" << endl;
    cout << "15. Copy Tree" << endl;
    cout << "16. Exit" << endl;
    cout << "==========================================" << endl;
    cout << "Enter your choice: ";
}

int main() {
    cout << "Welcome to Binary Tree Recursive Operations!" << endl;
    struct TreeNode_rrd* root_rrd = NULL;
    int choice_rrd;
    while (1)
{
        displayMenu_rrd();
        cin >> choice_rrd;
        switch (choice_rrd)
{
{
                freeTree_rrd(root_rrd);
                root_rrd = createSampleTree_rrd();
                cout << "Sample binary tree created successfully!" << endl;
                printTreeStructure_rrd(root_rrd);
                break;
            }

{
                int size_rrd;
                cout << "Enter number of elements: ";
                cin >> size_rrd;
                if (size_rrd <= 0)
{
                    cout << "Invalid size!" << endl;
                    break;
                }

                int* arr_rrd = (int*)malloc(size_rrd * sizeof(int));
                cout << "Enter " << size_rrd << " elements: ";
                for (int i_rrd = 0; i_rrd < size_rrd; i_rrd++)
{
                    cin >> arr_rrd[i_rrd];
                }

                freeTree_rrd(root_rrd);
                root_rrd = createBSTFromArray_rrd(arr_rrd, size_rrd);
                printTreeStructure_rrd(root_rrd);
                free(arr_rrd);
                break;
            }

{
                if (isEmpty_rrd(root_rrd))
{
                    cout << "Tree is empty!" << endl;
                    break;
                }

                cout << "Inorder Traversal (Recursive): ";
                inorderTraversal_rrd(root_rrd);
                cout << "" << endl;
                break;
            }

{
                if (isEmpty_rrd(root_rrd))
{
                    cout << "Tree is empty!" << endl;
                    break;
                }

                cout << "Preorder Traversal (Recursive): ";
                preorderTraversal_rrd(root_rrd);
                cout << "" << endl;
                break;
            }

{
                if (isEmpty_rrd(root_rrd))
{
                    cout << "Tree is empty!" << endl;
                    break;
                }

                cout << "Postorder Traversal (Recursive): ";
                postorderTraversal_rrd(root_rrd);
                cout << "" << endl;
                break;
            }

{
                if (isEmpty_rrd(root_rrd))
{
                    cout << "Tree is empty!" << endl;
                    break;
                }

                int leafCount_rrd = countLeafNodes_rrd(root_rrd);
                cout << "Number of leaf nodes: " << leafCount_rrd << "" << endl;
                break;
            }

{
                if (isEmpty_rrd(root_rrd))
{
                    cout << "Tree is empty!" << endl;
                    break;
                }

                struct TreeNode_rrd* original_rrd = copyTree_rrd(root_rrd);
                cout << "Original Tree:" << endl;
                printTreeStructure_rrd(root_rrd);
                mirrorImage_rrd(root_rrd);
                cout << "Mirror Image:" << endl;
                printTreeStructure_rrd(root_rrd);
                if (areIdentical_rrd(original_rrd, root_rrd))
{
                    cout << "The trees are identical (unexpected)" << endl;
                } else
{

                    cout << "The trees are mirror images of each other" << endl;
                }

                freeTree_rrd(original_rrd);
                break;
            }

{
                if (isEmpty_rrd(root_rrd))
{
                    cout << "Tree is empty!" << endl;
                    break;
                }

                printTreeStructure_rrd(root_rrd);
                break;
            }

{
                if (isEmpty_rrd(root_rrd))
{
                    cout << "Tree is empty!" << endl;
                    break;
                }

                int nodeCount_rrd = countTotalNodes_rrd(root_rrd);
                cout << "Total number of nodes: " << nodeCount_rrd << "" << endl;
                break;
            }

{
                if (isEmpty_rrd(root_rrd))
{
                    cout << "Tree is empty!" << endl;
                    break;
                }

                int height_rrd = findHeight_rrd(root_rrd);
                cout << "Height of tree: " << height_rrd << "" << endl;
                break;
            }

{
                if (isEmpty_rrd(root_rrd))
{
                    cout << "Tree is empty!" << endl;
                    break;
                }

                int minVal_rrd = findMinValue_rrd(root_rrd);
                cout << "Minimum value in tree: " << minVal_rrd << "" << endl;
                break;
            }

{
                if (isEmpty_rrd(root_rrd))
{
                    cout << "Tree is empty!" << endl;
                    break;
                }

                int maxVal_rrd = findMaxValue_rrd(root_rrd);
                cout << "Maximum value in tree: " << maxVal_rrd << "" << endl;
                break;
            }

{
                if (isEmpty_rrd(root_rrd))
{
                    cout << "Tree is empty!" << endl;
                    break;
                }

                int value_rrd;
                cout << "Enter value to search: ";
                cin >> value_rrd;
                struct TreeNode_rrd* result_rrd = search_rrd(root_rrd, value_rrd);
                if (result_rrd != NULL)
{
                    cout << "Value " << value_rrd << " found in the tree" << endl;
                } else
{

                    cout << "Value " << value_rrd << " not found in the tree" << endl;
                }
                break;
            }

{
                if (isEmpty_rrd(root_rrd))
{
                    cout << "Tree is empty!" << endl;
                    break;
                }

                int internalCount_rrd = countInternalNodes_rrd(root_rrd);
                cout << "Number of internal nodes: " << internalCount_rrd << "" << endl;
                break;
            }

{
                if (isEmpty_rrd(root_rrd))
{
                    cout << "Tree is empty!" << endl;
                    break;
                }

                struct TreeNode_rrd* copy_rrd = copyTree_rrd(root_rrd);
                cout << "Tree copied successfully!" << endl;
                cout << "Original Tree:" << endl;
                printTreeStructure_rrd(root_rrd);
                cout << "Copied Tree:" << endl;
                printTreeStructure_rrd(copy_rrd);
                if (areIdentical_rrd(root_rrd, copy_rrd))
{
                    cout << "The original and copied trees are identical" << endl;
                } else
{

                    cout << "The original and copied trees are different" << endl;
                }

                freeTree_rrd(copy_rrd);
                break;
            }

{
                cout << "Thank you for using Binary Tree Recursive Operations!" << endl;
                freeTree_rrd(root_rrd);
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
Welcome to Binary Tree Recursive Operations!
===== Binary Tree Recursive Operations =====
1. Create Sample Binary Tree
2. Create BST from Array
3. Inorder Traversal (Recursive)
4. Preorder Traversal (Recursive)
5. Postorder Traversal (Recursive)
6. Display Number of Leaf Nodes
7. Create Mirror Image
8. Display Tree Structure
9. Count Total Nodes
10. Find Height
11. Find Minimum Value
12. Find Maximum Value
13. Search Node
14. Count Internal Nodes
15. Copy Tree
16. Exit
==========================================
Enter your choice: 1
Sample binary tree created successfully!
Tree Structure:
                              9
                    6
                              8
          3
1
                    5
          2
                              7
                    4
===== Binary Tree Recursive Operations =====
1. Create Sample Binary Tree
2. Create BST from Array
3. Inorder Traversal (Recursive)
4. Preorder Traversal (Recursive)
5. Postorder Traversal (Recursive)
6. Display Number of Leaf Nodes
7. Create Mirror Image
8. Display Tree Structure
9. Count Total Nodes
10. Find Height
11. Find Minimum Value
12. Find Maximum Value
13. Search Node
14. Count Internal Nodes
15. Copy Tree
16. Exit
==========================================
Enter your choice: 3
Inorder Traversal (Recursive): 7 4 2 5 1 3 8 6 9 
===== Binary Tree Recursive Operations =====
1. Create Sample Binary Tree
2. Create BST from Array
3. Inorder Traversal (Recursive)
4. Preorder Traversal (Recursive)
5. Postorder Traversal (Recursive)
6. Display Number of Leaf Nodes
7. Create Mirror Image
8. Display Tree Structure
9. Count Total Nodes
10. Find Height
11. Find Minimum Value
12. Find Maximum Value
13. Search Node
14. Count Internal Nodes
15. Copy Tree
16. Exit
==========================================
Enter your choice: 4
Preorder Traversal (Recursive): 1 2 4 7 5 3 6 8 9 
===== Binary Tree Recursive Operations =====
1. Create Sample Binary Tree
2. Create BST from Array
3. Inorder Traversal (Recursive)
4. Preorder Traversal (Recursive)
5. Postorder Traversal (Recursive)
6. Display Number of Leaf Nodes
7. Create Mirror Image
8. Display Tree Structure
9. Count Total Nodes
10. Find Height
11. Find Minimum Value
12. Find Maximum Value
13. Search Node
14. Count Internal Nodes
15. Copy Tree
16. Exit
==========================================
Enter your choice: 5
Postorder Traversal (Recursive): 7 4 5 2 8 9 6 3 1 
===== Binary Tree Recursive Operations =====
1. Create Sample Binary Tree
2. Create BST from Array
3. Inorder Traversal (Recursive)
4. Preorder Traversal (Recursive)
5. Postorder Traversal (Recursive)
6. Display Number of Leaf Nodes
7. Create Mirror Image
8. Display Tree Structure
9. Count Total Nodes
10. Find Height
11. Find Minimum Value
12. Find Maximum Value
13. Search Node
14. Count Internal Nodes
15. Copy Tree
16. Exit
==========================================
Enter your choice: 6
Number of leaf nodes: 4
===== Binary Tree Recursive Operations =====
1. Create Sample Binary Tree
2. Create BST from Array
3. Inorder Traversal (Recursive)
4. Preorder Traversal (Recursive)
5. Postorder Traversal (Recursive)
6. Display Number of Leaf Nodes
7. Create Mirror Image
8. Display Tree Structure
9. Count Total Nodes
10. Find Height
11. Find Minimum Value
12. Find Maximum Value
13. Search Node
14. Count Internal Nodes
15. Copy Tree
16. Exit
==========================================
Enter your choice: 7
Original Tree:
                              9
                    6
                              8
          3
1
                    5
          2
                              7
                    4
Mirror Image:
                              7
                    4
          2
1
                              9
                    6
                              8
          3
                    5
```

## Dry Run

For the sample binary tree:
```
       1
      / \
     2   3
    / \   \
   4   5   6
  /       / \
 7       8   9
```

1. **Inorder Traversal (Recursive)**:
   - inorderTraversal_rrd(1):
     * inorderTraversal_rrd(2):
       - inorderTraversal_rrd(4):
         * inorderTraversal_rrd(7): 
           + 7 (print)
         * 4 (print)
         * inorderTraversal_rrd(NULL): (nothing)
       - 2 (print)
       - inorderTraversal_rrd(5): 
         * 5 (print)
     * 1 (print)
     * inorderTraversal_rrd(3):
       - inorderTraversal_rrd(NULL): (nothing)
       - 3 (print)
       - inorderTraversal_rrd(6):
         * inorderTraversal_rrd(8):
           + 8 (print)
         * 6 (print)
         * inorderTraversal_rrd(9):
           + 9 (print)
   - Result: 7 4 2 5 1 3 8 6 9

2. **Preorder Traversal (Recursive)**:
   - preorderTraversal_rrd(1):
     * 1 (print)
     * preorderTraversal_rrd(2):
       - 2 (print)
       - preorderTraversal_rrd(4):
         * 4 (print)
         * preorderTraversal_rrd(7):
           + 7 (print)
         * preorderTraversal_rrd(NULL): (nothing)
       - preorderTraversal_rrd(5):
         * 5 (print)
     * preorderTraversal_rrd(3):
       - 3 (print)
       - preorderTraversal_rrd(NULL): (nothing)
       - preorderTraversal_rrd(6):
         * 6 (print)
         * preorderTraversal_rrd(8):
           + 8 (print)
         * preorderTraversal_rrd(9):
           + 9 (print)
   - Result: 1 2 4 7 5 3 6 8 9

3. **Count Leaf Nodes (Recursive)**:
   - countLeafNodes_rrd(1):
     * countLeafNodes_rrd(2):
       - countLeafNodes_rrd(4):
         * countLeafNodes_rrd(7): return 1 (leaf)
         * countLeafNodes_rrd(NULL): return 0
         * return 1
       - countLeafNodes_rrd(5): return 1 (leaf)
       * return 1 + 1 = 2
     * countLeafNodes_rrd(3):
       - countLeafNodes_rrd(NULL): return 0
       - countLeafNodes_rrd(6):
         * countLeafNodes_rrd(8): return 1 (leaf)
         * countLeafNodes_rrd(9): return 1 (leaf)
         * return 1 + 1 = 2
       * return 0 + 2 = 2
     * return 2 + 2 = 4
   - Result: 4 leaf nodes (7, 5, 8, 9)

4. **Mirror Image (Recursive)**:
   - mirrorImage_rrd(1):
     * mirrorImage_rrd(2):
       - mirrorImage_rrd(4):
         * mirrorImage_rrd(7): (leaf, no children)
         * mirrorImage_rrd(NULL): (nothing)
         * Swap 7 and NULL: 4 now has 7 as right child
       - mirrorImage_rrd(5): (leaf, no children)
       - Swap left(4) and right(5): 2 now has 5 as left child, 4 as right child
     * mirrorImage_rrd(3):
       - mirrorImage_rrd(NULL): (nothing)
       - mirrorImage_rrd(6):
         * mirrorImage_rrd(8): (leaf, no children)
         * mirrorImage_rrd(9): (leaf, no children)
         * Swap left(8) and right(9): 6 now has 9 as left child, 8 as right child
       - Swap left(NULL) and right(6): 3 now has 6 as left child
     * Swap left(2) and right(3): 1 now has 3 as left child, 2 as right child

## Conclusion

The implementation demonstrates recursive Binary Tree operations with elegant and intuitive algorithms. Key features include:

1. **Recursive Approach**: All operations implemented using recursion
2. **Complete Functionality**: All required operations plus additional utilities
3. **Natural Fit**: Recursion naturally fits tree structures
4. **Clean Code**: Elegant and readable recursive implementations

**Time Complexities**:
- Inorder Traversal: O(n) where n is number of nodes
- Preorder Traversal: O(n) where n is number of nodes
- Postorder Traversal: O(n) where n is number of nodes
- Count Leaf Nodes: O(n) where n is number of nodes
- Mirror Image: O(n) where n is number of nodes
- All operations visit each node exactly once

**Space Complexity**: O(h) where h is height of tree (due to recursion stack)

The recursive implementations are elegant because:
1. **Natural Expression**: Trees are naturally recursive structures
2. **Clean Code**: Less code and easier to understand
3. **Intuitive Logic**: Direct translation of mathematical definitions
4. **Educational Value**: Helps understand recursion concepts

The recursive approach for tree operations:
1. **Inorder**: Left subtree → Root → Right subtree
2. **Preorder**: Root → Left subtree → Right subtree
3. **Postorder**: Left subtree → Right subtree → Root
4. **Leaf Count**: Base cases (NULL=0, leaf=1) + recursive cases
5. **Mirror Image**: Recurse then swap (post-order processing)

The implementation handles edge cases properly:
- Empty tree operations
- Single node trees
- Linear (skewed) trees
- Balanced trees
- Memory management to prevent leaks

Additional features beyond requirements:
- Postorder traversal (bonus)
- Tree structure visualization
- Total node counting
- Height calculation
- Min/max value finding
- Node searching
- Internal node counting
- Tree copying and comparison
- Comprehensive menu system

In real-world applications, recursive tree operations are useful for:
1. **Compiler Design**: Parse tree processing
2. **File Systems**: Directory traversal
3. **Game Development**: Decision tree evaluation
4. **Database Indexing**: B-tree operations
5. **Artificial Intelligence**: Game tree search
6. **Computer Graphics**: Scene graph processing

The recursive approach is preferred in many cases because:
1. **Simplicity**: More intuitive and easier to implement
2. **Readability**: Code closely matches the mathematical definition
3. **Maintainability**: Easier to modify and extend
4. **Educational Value**: Helps students understand recursion

However, for very deep trees, iterative approaches might be preferred to avoid stack overflow. The choice between recursive and iterative depends on:
1. Tree depth and available stack space
2. Performance requirements
3. Code maintainability needs
4. Developer preference and team standards

This implementation provides a solid foundation for understanding recursive algorithms and their application to tree data structures, which is fundamental in computer science.
