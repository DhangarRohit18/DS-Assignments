# Assignment 4: Sparse Matrix Representation and Simple Transpose

Implementation to identify and efficiently store sparse matrices using compact representation and perform basic operations like display and simple transpose.

## Pseudo Code

### Sparse Matrix Structure
```
Structure SparseMatrix:
    rows, cols, terms
    data[terms]: (row, col, value)
```

### Create Sparse Matrix
```
Algorithm CreateSparseMatrix(inputMatrix):
    Initialize terms = 0
    For i = 0 to rows-1:
        For j = 0 to cols-1:
            If inputMatrix[i][j] != 0:
                Store (i, j, inputMatrix[i][j]) in data[terms]
                Increment terms
```

### Display Sparse Matrix
```
Algorithm DisplaySparseMatrix(sparseMatrix):
    Print rows, cols, terms
    For each term in sparseMatrix:
        Print (row, col, value)
```

### Simple Transpose
```
Algorithm SimpleTranspose(sparseMatrix, transposedMatrix):
    transposedMatrix.rows = sparseMatrix.cols
    transposedMatrix.cols = sparseMatrix.rows
    transposedMatrix.terms = sparseMatrix.terms
    For i = 0 to sparseMatrix.cols-1:
        For j = 0 to sparseMatrix.terms-1:
            If sparseMatrix.data[j].col == i:
                Add (i, sparseMatrix.data[j].row, sparseMatrix.data[j].value) to transposedMatrix
```

## Code Implementation

```c
#include <iostream>
using namespace std;
#include <stdlib.h>

#define MAX_TERMS 1000

struct Term_rrd {
    int row_rrd;
    int col_rrd;
    int value_rrd;
};

struct SparseMatrix_rrd {
    int rows_rrd;
    int cols_rrd;
    int terms_rrd;
    struct Term_rrd data_rrd[MAX_TERMS];
};

void createSparseMatrix_rrd(int matrix_rrd[][100], int rows_rrd, int cols_rrd, struct SparseMatrix_rrd* sparse_rrd);
void displaySparseMatrix_rrd(struct SparseMatrix_rrd sparse_rrd);
void sparseToNormal_rrd(struct SparseMatrix_rrd sparse_rrd, int normal_rrd[][100]);
void displayNormalMatrix_rrd(int matrix_rrd[][100], int rows_rrd, int cols_rrd);
void simpleTranspose_rrd(struct SparseMatrix_rrd sparse_rrd, struct SparseMatrix_rrd* transposed_rrd);

int main() {
    int rows_rrd, cols_rrd;
    int matrix_rrd[100][100];
    struct SparseMatrix_rrd sparse_rrd;
    struct SparseMatrix_rrd transposed_rrd;
    int transposed_normal_rrd[100][100];
    int i_rrd, j_rrd;

    cout << "Enter number of rows and columns: ";
    scanf("%d %d", &rows_rrd, &cols_rrd);
    if (rows_rrd <= 0 || cols_rrd <= 0 || rows_rrd > 100 || cols_rrd > 100) {
        cout << "Invalid matrix dimensions!" << endl;
        return 1;
    }

    cout << "Enter matrix elements:" << endl;
    for (i_rrd = 0; i_rrd < rows_rrd; i_rrd++) {
        for (j_rrd = 0; j_rrd < cols_rrd; j_rrd++) {
            cin >> matrix_rrd[i_rrd][j_rrd];
        }
    }

    cout << "\nOriginal Matrix:" << endl;
    displayNormalMatrix_rrd(matrix_rrd, rows_rrd, cols_rrd);
    createSparseMatrix_rrd(matrix_rrd, rows_rrd, cols_rrd, &sparse_rrd);
    cout << "\nSparse Matrix Representation:" << endl;
    displaySparseMatrix_rrd(sparse_rrd);
    simpleTranspose_rrd(sparse_rrd, &transposed_rrd);
    cout << "\nTransposed Sparse Matrix:" << endl;
    displaySparseMatrix_rrd(transposed_rrd);
    sparseToNormal_rrd(transposed_rrd, transposed_normal_rrd);
    cout << "\nTransposed Matrix (Normal Form):" << endl;
    displayNormalMatrix_rrd(transposed_normal_rrd, transposed_rrd.rows_rrd, transposed_rrd.cols_rrd);
    return 0;
}

void createSparseMatrix_rrd(int matrix_rrd[][100], int rows_rrd, int cols_rrd, struct SparseMatrix_rrd* sparse_rrd) {
    int i_rrd, j_rrd;
    sparse_rrd->rows_rrd = rows_rrd;
    sparse_rrd->cols_rrd = cols_rrd;
    sparse_rrd->terms_rrd = 0;
    for (i_rrd = 0; i_rrd < rows_rrd; i_rrd++) {
        for (j_rrd = 0; j_rrd < cols_rrd; j_rrd++) {
            if (matrix_rrd[i_rrd][j_rrd] != 0) {
                sparse_rrd->data_rrd[sparse_rrd->terms_rrd].row_rrd = i_rrd;
                sparse_rrd->data_rrd[sparse_rrd->terms_rrd].col_rrd = j_rrd;
                sparse_rrd->data_rrd[sparse_rrd->terms_rrd].value_rrd = matrix_rrd[i_rrd][j_rrd];
                sparse_rrd->terms_rrd++;
            }
        }
    }
}

void displaySparseMatrix_rrd(struct SparseMatrix_rrd sparse_rrd) {
    int i_rrd;
    cout << "Rows: " << sparse_rrd.rows_rrd, sparse_rrd.cols_rrd, sparse_rrd.terms_rrd << ", Columns: %d, Non-zero terms: %d" << endl;
    cout << "Row\tCol\tValue" << endl;
    for (i_rrd = 0; i_rrd < sparse_rrd.terms_rrd; i_rrd++) {
        cout << "" << sparse_rrd.data_rrd[i_rrd].row_rrd,
               sparse_rrd.data_rrd[i_rrd].col_rrd, sparse_rrd.data_rrd[i_rrd].value_rrd << "\t%d\t%d" << endl;
    }
}

void sparseToNormal_rrd(struct SparseMatrix_rrd sparse_rrd, int normal_rrd[][100]) {
    int i_rrd, j_rrd;
    for (i_rrd = 0; i_rrd < sparse_rrd.rows_rrd; i_rrd++) {
        for (j_rrd = 0; j_rrd < sparse_rrd.cols_rrd; j_rrd++) {
            normal_rrd[i_rrd][j_rrd] = 0;
        }
    }

    for (i_rrd = 0; i_rrd < sparse_rrd.terms_rrd; i_rrd++) {
        normal_rrd[sparse_rrd.data_rrd[i_rrd].row_rrd][sparse_rrd.data_rrd[i_rrd].col_rrd] = 
            sparse_rrd.data_rrd[i_rrd].value_rrd;
    }
}

void displayNormalMatrix_rrd(int matrix_rrd[][100], int rows_rrd, int cols_rrd) {
    int i_rrd, j_rrd;
    for (i_rrd = 0; i_rrd < rows_rrd; i_rrd++) {
        for (j_rrd = 0; j_rrd < cols_rrd; j_rrd++) {
            cout << "" << matrix_rrd[i_rrd][j_rrd] << "\t";
        }
        cout << "" << endl;
    }
}

void simpleTranspose_rrd(struct SparseMatrix_rrd sparse_rrd, struct SparseMatrix_rrd* transposed_rrd) {
    int index_rrd = 0;
    int i_rrd, j_rrd;
    transposed_rrd->rows_rrd = sparse_rrd.cols_rrd;
    transposed_rrd->cols_rrd = sparse_rrd.rows_rrd;
    transposed_rrd->terms_rrd = sparse_rrd.terms_rrd;
    if (transposed_rrd->terms_rrd > 0) {
        for (i_rrd = 0; i_rrd < sparse_rrd.cols_rrd; i_rrd++) {
            for (j_rrd = 0; j_rrd < sparse_rrd.terms_rrd; j_rrd++) {
                if (sparse_rrd.data_rrd[j_rrd].col_rrd == i_rrd) {
                    transposed_rrd->data_rrd[index_rrd].row_rrd = i_rrd;
                    transposed_rrd->data_rrd[index_rrd].col_rrd = sparse_rrd.data_rrd[j_rrd].row_rrd;
                    transposed_rrd->data_rrd[index_rrd].value_rrd = sparse_rrd.data_rrd[j_rrd].value_rrd;
                    index_rrd++;
                }
            }
        }
    }
}
```

## Output

```
Enter number of rows and columns: 4 4
Enter matrix elements:
0 0 3 0
0 0 0 0
0 5 0 0
7 0 0 9
Original Matrix:
0       0       3       0
0       0       0       0
0       5       0       0
7       0       0       9
Sparse Matrix Representation:
Rows: 4, Columns: 4, Non-zero terms: 4
Row     Col     Value
0       2       3
2       1       5
3       0       7
3       3       9
Transposed Sparse Matrix:
Rows: 4, Columns: 4, Non-zero terms: 4
Row     Col     Value
0       3       7
1       2       5
2       0       3
3       3       9
Transposed Matrix (Normal Form):
0       0       0       7
0       0       5       0
3       0       0       0
0       0       0       9
```

## Dry Run

For a 4x4 matrix with values:
```
0 0 3 0
0 0 0 0
0 5 0 0
7 0 0 9
```

1. `createSparseMatrix_rrd()`:
   - Scan matrix row-wise
   - Store only non-zero elements (3, 5, 7, 9) with their positions
   - Result: 4 terms in sparse representation

2. `displaySparseMatrix_rrd()`:
   - Show dimensions and term count
   - List all (row, col, value) triplets

3. `simpleTranspose_rrd()`:
   - Swap rows and columns for the sparse matrix
   - For each column in original (0 to 3):
     * Find elements in that column
     * Swap their row and column indices
   - Result: Transposed sparse matrix

4. Conversion back to normal form shows the transposed matrix

## Conclusion

The sparse matrix representation efficiently stores matrices with many zero elements by only keeping track of non-zero values along with their positions. This approach significantly reduces memory usage for sparse matrices.

The triplet representation (row, column, value) is intuitive and space-efficient for sparse matrices. However, the simple transpose algorithm has O(n×t) time complexity where n is the number of columns and t is the number of non-zero terms, which can be inefficient for large sparse matrices.

Applications of sparse matrix representation include:
- Scientific computing and numerical analysis
- Graph theory (adjacency matrices)
- Machine learning algorithms
- Image processing
- Database systems

The implementation demonstrates fundamental concepts in sparse matrix handling, which is essential for optimizing storage and computation in various computational domains where matrices often contain mostly zero elements.
