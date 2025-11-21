# Unit II Assignment 7: Polynomial Addition using Singly Linked List

Implementation of polynomial addition using singly linked list to represent and manipulate polynomials efficiently.

## Problem Statement

Write a C program to perform addition of two polynomials using singly linked list representation.

## Pseudo Code

### Polynomial Node Structure
```
Structure PolyNode:
    coeff: integer (coefficient)
    exp: integer (exponent)
    next: pointer to PolyNode
```

### Create Polynomial Node
```
Algorithm CreatePolyNode(coeff, exp):
    Create new node
    node.coeff = coeff
    node.exp = exp
    node.next = NULL
    Return node
```

### Insert Term in Polynomial
```
Algorithm InsertTerm(poly, coeff, exp):
    Create new node with coeff and exp
    If poly is NULL:
        Return new node
    If exp > poly.exp:
        new_node.next = poly
        Return new_node
    current = poly
    While current.next != NULL AND current.next.exp > exp:
        current = current.next
    If current.next != NULL AND current.next.exp == exp:
        current.next.coeff += coeff
        If current.next.coeff == 0:
            Delete current.next
    Else:
        new_node.next = current.next
        current.next = new_node
    Return poly
```

### Add Two Polynomials
```
Algorithm AddPolynomials(poly1, poly2):
    result = NULL
    current1 = poly1
    current2 = poly2
    While current1 != NULL AND current2 != NULL:
        If current1.exp > current2.exp:
            result = InsertTerm(result, current1.coeff, current1.exp)
            current1 = current1.next
        Else If current2.exp > current1.exp:
            result = InsertTerm(result, current2.coeff, current2.exp)
            current2 = current2.next
        Else:
            sum = current1.coeff + current2.coeff
            If sum != 0:
                result = InsertTerm(result, sum, current1.exp)
            current1 = current1.next
            current2 = current2.next
    While current1 != NULL:
        result = InsertTerm(result, current1.coeff, current1.exp)
        current1 = current1.next
    While current2 != NULL:
        result = InsertTerm(result, current2.coeff, current2.exp)
        current2 = current2.next
    Return result
```

### Display Polynomial
```
Algorithm DisplayPolynomial(poly):
    If poly is NULL:
        Print "0"
        Return
    current = poly
    While current != NULL:
        If current != poly AND current.coeff > 0:
            Print " + "
        Else If current.coeff < 0:
            Print " - "
            current.coeff = -current.coeff
        If current.exp == 0:
            Print current.coeff
        Else If current.exp == 1:
            Print current.coeff "x"
        Else:
            Print current.coeff "x^" current.exp
        current = current.next
```

## Code Implementation

```c
#include <iostream>
using namespace std;
#include <stdlib.h>

struct PolyNode_rrd {
    int coeff_rrd;
    int exp_rrd;
    struct PolyNode_rrd* next_rrd;
};

struct PolyNode_rrd* createPolyNode_rrd(int coeff_rrd, int exp_rrd);
struct PolyNode_rrd* insertTerm_rrd(struct PolyNode_rrd* poly_rrd, int coeff_rrd, int exp_rrd);
struct PolyNode_rrd* addPolynomials_rrd(struct PolyNode_rrd* poly1_rrd, struct PolyNode_rrd* poly2_rrd);
void displayPolynomial_rrd(struct PolyNode_rrd* poly_rrd);
struct PolyNode_rrd* inputPolynomial_rrd();
void freePolynomial_rrd(struct PolyNode_rrd* poly_rrd);

int main() {
    struct PolyNode_rrd* poly1_rrd = NULL;
    struct PolyNode_rrd* poly2_rrd = NULL;
    struct PolyNode_rrd* result_rrd = NULL;
    
    cout << "Polynomial Addition using Singly Linked List" << endl;
    cout << "===========================================" << endl;
    
    cout << "Enter first polynomial:" << endl;
    poly1_rrd = inputPolynomial_rrd();
    
    cout << "\nEnter second polynomial:" << endl;
    poly2_rrd = inputPolynomial_rrd();
    
    cout << "\nFirst polynomial: ";
    displayPolynomial_rrd(poly1_rrd);
    cout << "" << endl;
    
    cout << "Second polynomial: ";
    displayPolynomial_rrd(poly2_rrd);
    cout << "" << endl;
    
    result_rrd = addPolynomials_rrd(poly1_rrd, poly2_rrd);
    
    cout << "Sum of polynomials: ";
    displayPolynomial_rrd(result_rrd);
    cout << "" << endl;
    

    freePolynomial_rrd(poly1_rrd);
    freePolynomial_rrd(poly2_rrd);
    freePolynomial_rrd(result_rrd);
    
    return 0;
}

struct PolyNode_rrd* createPolyNode_rrd(int coeff_rrd, int exp_rrd) {
    struct PolyNode_rrd* newNode_rrd = (struct PolyNode_rrd*)malloc(sizeof(struct PolyNode_rrd));
    newNode_rrd->coeff_rrd = coeff_rrd;
    newNode_rrd->exp_rrd = exp_rrd;
    newNode_rrd->next_rrd = NULL;
    return newNode_rrd;
}

struct PolyNode_rrd* insertTerm_rrd(struct PolyNode_rrd* poly_rrd, int coeff_rrd, int exp_rrd) {

    if (coeff_rrd == 0) {
        return poly_rrd;
    }
    

    struct PolyNode_rrd* newNode_rrd = createPolyNode_rrd(coeff_rrd, exp_rrd);
    

    if (poly_rrd == NULL || exp_rrd > poly_rrd->exp_rrd) {
        newNode_rrd->next_rrd = poly_rrd;
        return newNode_rrd;
    }
    

    if (exp_rrd == poly_rrd->exp_rrd) {
        poly_rrd->coeff_rrd += coeff_rrd;
        if (poly_rrd->coeff_rrd == 0) {
            struct PolyNode_rrd* temp_rrd = poly_rrd;
            poly_rrd = poly_rrd->next_rrd;
            free(temp_rrd);
        }
        free(newNode_rrd);
        return poly_rrd;
    }
    

    struct PolyNode_rrd* current_rrd = poly_rrd;
    while (current_rrd->next_rrd != NULL && current_rrd->next_rrd->exp_rrd > exp_rrd) {
        current_rrd = current_rrd->next_rrd;
    }
    

    if (current_rrd->next_rrd != NULL && current_rrd->next_rrd->exp_rrd == exp_rrd) {
        current_rrd->next_rrd->coeff_rrd += coeff_rrd;
        if (current_rrd->next_rrd->coeff_rrd == 0) {
            struct PolyNode_rrd* temp_rrd = current_rrd->next_rrd;
            current_rrd->next_rrd = temp_rrd->next_rrd;
            free(temp_rrd);
        }
        free(newNode_rrd);
    } else {

        newNode_rrd->next_rrd = current_rrd->next_rrd;
        current_rrd->next_rrd = newNode_rrd;
    }
    
    return poly_rrd;
}

struct PolyNode_rrd* addPolynomials_rrd(struct PolyNode_rrd* poly1_rrd, struct PolyNode_rrd* poly2_rrd) {
    struct PolyNode_rrd* result_rrd = NULL;
    struct PolyNode_rrd* current1_rrd = poly1_rrd;
    struct PolyNode_rrd* current2_rrd = poly2_rrd;
    

    while (current1_rrd != NULL && current2_rrd != NULL) {
        if (current1_rrd->exp_rrd > current2_rrd->exp_rrd) {

            result_rrd = insertTerm_rrd(result_rrd, current1_rrd->coeff_rrd, current1_rrd->exp_rrd);
            current1_rrd = current1_rrd->next_rrd;
        } else if (current2_rrd->exp_rrd > current1_rrd->exp_rrd) {

            result_rrd = insertTerm_rrd(result_rrd, current2_rrd->coeff_rrd, current2_rrd->exp_rrd);
            current2_rrd = current2_rrd->next_rrd;
        } else {

            int sumCoeff_rrd = current1_rrd->coeff_rrd + current2_rrd->coeff_rrd;
            if (sumCoeff_rrd != 0) {
                result_rrd = insertTerm_rrd(result_rrd, sumCoeff_rrd, current1_rrd->exp_rrd);
            }
            current1_rrd = current1_rrd->next_rrd;
            current2_rrd = current2_rrd->next_rrd;
        }
    }
    

    while (current1_rrd != NULL) {
        result_rrd = insertTerm_rrd(result_rrd, current1_rrd->coeff_rrd, current1_rrd->exp_rrd);
        current1_rrd = current1_rrd->next_rrd;
    }
    

    while (current2_rrd != NULL) {
        result_rrd = insertTerm_rrd(result_rrd, current2_rrd->coeff_rrd, current2_rrd->exp_rrd);
        current2_rrd = current2_rrd->next_rrd;
    }
    
    return result_rrd;
}

void displayPolynomial_rrd(struct PolyNode_rrd* poly_rrd) {
    if (poly_rrd == NULL) {
        cout << "0";
        return;
    }
    
    struct PolyNode_rrd* current_rrd = poly_rrd;
    int first_rrd = 1;
    
    while (current_rrd != NULL) {
        if (!first_rrd) {
            if (current_rrd->coeff_rrd > 0) {
                cout << " + ";
            } else {
                cout << " - ";
                current_rrd->coeff_rrd = -current_rrd->coeff_rrd;
            }
        } else {
            if (current_rrd->coeff_rrd < 0) {
                cout << "-";
                current_rrd->coeff_rrd = -current_rrd->coeff_rrd;
            }
            first_rrd = 0;
        }
        
        if (current_rrd->exp_rrd == 0) {
            cout << "" << current_rrd->coeff_rrd << "";
        } else if (current_rrd->exp_rrd == 1) {
            if (current_rrd->coeff_rrd == 1) {
                cout << "x";
            } else {
                cout << "" << current_rrd->coeff_rrd << "x";
            }
        } else {
            if (current_rrd->coeff_rrd == 1) {
                cout << "x^" << current_rrd->exp_rrd << "";
            } else {
                cout << "" << current_rrd->coeff_rrd, current_rrd->exp_rrd << "x^%d";
            }
        }
        
        current_rrd = current_rrd->next_rrd;
    }
}

struct PolyNode_rrd* inputPolynomial_rrd() {
    struct PolyNode_rrd* poly_rrd = NULL;
    int n_rrd, coeff_rrd, exp_rrd, i_rrd;
    
    cout << "Enter number of terms: ";
    cin >> n_rrd;
    
    for (i_rrd = 0; i_rrd < n_rrd; i_rrd++) {
        cout << "Enter coefficient and exponent for term " << i_rrd + 1 << ": ";
        scanf("%d %d", &coeff_rrd, &exp_rrd);
        poly_rrd = insertTerm_rrd(poly_rrd, coeff_rrd, exp_rrd);
    }
    
    return poly_rrd;
}

void freePolynomial_rrd(struct PolyNode_rrd* poly_rrd) {
    struct PolyNode_rrd* temp_rrd;
    while (poly_rrd != NULL) {
        temp_rrd = poly_rrd;
        poly_rrd = poly_rrd->next_rrd;
        free(temp_rrd);
    }
}
```

## Output

```
Polynomial Addition using Singly Linked List
===========================================
Enter first polynomial:
Enter number of terms: 3
Enter coefficient and exponent for term 1: 3 2
Enter coefficient and exponent for term 2: 2 1
Enter coefficient and exponent for term 3: 1 0

Enter second polynomial:
Enter number of terms: 3
Enter coefficient and exponent for term 1: 2 2
Enter coefficient and exponent for term 2: -3 1
Enter coefficient and exponent for term 3: 4 0

First polynomial: 3x^2 + 2x + 1
Second polynomial: 2x^2 - 3x + 4
Sum of polynomials: 5x^2 - x + 5
```

## Dry Run

1. **Input First Polynomial (3x² + 2x + 1)**:
   - Insert term 3x²: List becomes [3,2]
   - Insert term 2x: List becomes [3,2] -> [2,1]
   - Insert term 1: List becomes [3,2] -> [2,1] -> [1,0]

2. **Input Second Polynomial (2x² - 3x + 4)**:
   - Insert term 2x²: List becomes [2,2]
   - Insert term -3x: List becomes [2,2] -> [-3,1]
   - Insert term 4: List becomes [2,2] -> [-3,1] -> [4,0]

3. **Addition Process**:
   - Compare exponents of first terms: 2 == 2
   - Add coefficients: 3 + 2 = 5, create term 5x²
   - Move to next terms: 2x and -3x
   - Compare exponents: 1 == 1
   - Add coefficients: 2 + (-3) = -1, create term -x
   - Move to next terms: 1 and 4
   - Compare exponents: 0 == 0
   - Add coefficients: 1 + 4 = 5, create term 5
   - No more terms in either polynomial
   - Result: 5x² - x + 5

## Conclusion

The implementation demonstrates polynomial addition using singly linked lists with the following key features:

1. **Efficient Representation**: Only stores non-zero terms, saving memory
2. **Sorted Order**: Terms are maintained in descending order of exponents
3. **Dynamic Memory**: Allocates memory only for existing terms
4. **Automatic Simplification**: Combines like terms during insertion

**Time Complexities**:
- Term Insertion: O(n) where n is the number of terms
- Polynomial Addition: O(m + n) where m and n are terms in the two polynomials
- Display: O(n) where n is the number of terms

**Space Complexity**: O(m + n) for storing the two input polynomials and result

The linked list approach is particularly advantageous for polynomials because:
1. It efficiently handles sparse polynomials (many zero coefficients)
2. It dynamically adjusts to the number of terms
3. It maintains terms in sorted order for efficient operations
4. It naturally handles polynomials of any degree

The implementation correctly handles edge cases such as:
- Zero coefficients (terms are not stored)
- Like term combination (coefficients are added)
- Negative coefficients (properly displayed with minus signs)
- Empty polynomials (represented as zero)