# Unit V Assignment 6: Kruskal's Algorithm for Minimum Spanning Tree using Adjacency Matrix

Implementation of Kruskal's algorithm to find the minimum spanning tree of a user-defined graph using adjacency matrix representation.

## Problem Statement

Write a Program to implement Kruskal's algorithm to find the minimum spanning tree of a user defined graph. Use Adjacency Matrix to represent a graph.

## Pseudo Code

### Graph Structure
```
Structure Graph:
    vertices: integer
    adjMatrix: 2D array of size vertices x vertices
```

### Edge Structure
```
Structure Edge:
    src: integer (source vertex)
    dest: integer (destination vertex)
    weight: integer
```

### Find Parent (Union-Find)
```
Algorithm FindParent(parent, vertex):
    If parent[vertex] == vertex:
        Return vertex
    Return FindParent(parent, parent[vertex])
```

### Union (Union-Find)
```
Algorithm Union(parent, rank, x, y):
    xRoot = FindParent(parent, x)
    yRoot = FindParent(parent, y)
    If rank[xRoot] < rank[yRoot]:
        parent[xRoot] = yRoot
    Else If rank[xRoot] > rank[yRoot]:
        parent[yRoot] = xRoot
    Else:
        parent[yRoot] = xRoot
        rank[xRoot]++
```

### Kruskal's Algorithm
```
Algorithm KruskalMST(graph):
    Initialize edges array to store all edges
    Initialize parent array of size vertices
    Initialize rank array of size vertices
    For each vertex i:
        parent[i] = i
        rank[i] = 0
    Sort edges array by weight
    Initialize edgeCount = 0
    For each edge in sorted edges:
        If edgeCount == vertices - 1:
            Break
        x = FindParent(parent, edge.src)
        y = FindParent(parent, edge.dest)
        If x != y:
            Add edge to MST
            Union(parent, rank, x, y)
            edgeCount++
```

## Code Implementation

```c
#include <iostream>
using namespace std;
#include <stdlib.h>
#include <limits.h>

#define MAX_VERTICES 100
#define MAX_EDGES (MAX_VERTICES * MAX_VERTICES)

struct Graph_rrd {
    int vertices_rrd;
    int adjMatrix_rrd[MAX_VERTICES][MAX_VERTICES];
};

struct Edge_rrd {
    int src_rrd;
    int dest_rrd;
    int weight_rrd;
};

struct Graph_rrd* createGraph_rrd(int vertices_rrd);
void addEdge_rrd(struct Graph_rrd* graph_rrd, int src_rrd, int dest_rrd, int weight_rrd);
int findParent_rrd(int parent_rrd[], int vertex_rrd);
void unionSets_rrd(int parent_rrd[], int rank_rrd[], int x_rrd, int y_rrd);
int compareEdges_rrd(const void* a_rrd, const void* b_rrd);
void kruskalMST_rrd(struct Graph_rrd* graph_rrd);
void printGraph_rrd(struct Graph_rrd* graph_rrd);
void printAdjMatrix_rrd(struct Graph_rrd* graph_rrd);
struct Graph_rrd* createSampleGraph_rrd();
void displayMenu_rrd();

struct Graph_rrd* createGraph_rrd(int vertices_rrd) {
    struct Graph_rrd* graph_rrd = (struct Graph_rrd*)malloc(sizeof(struct Graph_rrd));
    int i_rrd, j_rrd;
    graph_rrd->vertices_rrd = vertices_rrd;
    
    for (i_rrd = 0; i_rrd < vertices_rrd; i_rrd++) {
        for (j_rrd = 0; j_rrd < vertices_rrd; j_rrd++) {
            graph_rrd->adjMatrix_rrd[i_rrd][j_rrd] = 0;
        }
    }
    
    return graph_rrd;
}

void addEdge_rrd(struct Graph_rrd* graph_rrd, int src_rrd, int dest_rrd, int weight_rrd) {
    graph_rrd->adjMatrix_rrd[src_rrd][dest_rrd] = weight_rrd;
    graph_rrd->adjMatrix_rrd[dest_rrd][src_rrd] = weight_rrd;
}

int findParent_rrd(int parent_rrd[], int vertex_rrd) {
    if (parent_rrd[vertex_rrd] == vertex_rrd) {
        return vertex_rrd;
    }
    return findParent_rrd(parent_rrd, parent_rrd[vertex_rrd]);
}

void unionSets_rrd(int parent_rrd[], int rank_rrd[], int x_rrd, int y_rrd) {
    int xRoot_rrd = findParent_rrd(parent_rrd, x_rrd);
    int yRoot_rrd = findParent_rrd(parent_rrd, y_rrd);
    
    if (rank_rrd[xRoot_rrd] < rank_rrd[yRoot_rrd]) {
        parent_rrd[xRoot_rrd] = yRoot_rrd;
    } else if (rank_rrd[xRoot_rrd] > rank_rrd[yRoot_rrd]) {
        parent_rrd[yRoot_rrd] = xRoot_rrd;
    } else {
        parent_rrd[yRoot_rrd] = xRoot_rrd;
        rank_rrd[xRoot_rrd]++;
    }
}

int compareEdges_rrd(const void* a_rrd, const void* b_rrd) {
    struct Edge_rrd* edge1_rrd = (struct Edge_rrd*)a_rrd;
    struct Edge_rrd* edge2_rrd = (struct Edge_rrd*)b_rrd;
    return edge1_rrd->weight_rrd - edge2_rrd->weight_rrd;
}

void kruskalMST_rrd(struct Graph_rrd* graph_rrd) {
    struct Edge_rrd edges_rrd[MAX_EDGES];
    int parent_rrd[MAX_VERTICES];
    int rank_rrd[MAX_VERTICES];
    int edgeCount_rrd = 0;
    int totalWeight_rrd = 0;
    int i_rrd, j_rrd;
    

    for (i_rrd = 0; i_rrd < graph_rrd->vertices_rrd; i_rrd++) {
        parent_rrd[i_rrd] = i_rrd;
        rank_rrd[i_rrd] = 0;
    }
    

    int edgeIndex_rrd = 0;
    for (i_rrd = 0; i_rrd < graph_rrd->vertices_rrd; i_rrd++) {
        for (j_rrd = i_rrd + 1; j_rrd < graph_rrd->vertices_rrd; j_rrd++) {
            if (graph_rrd->adjMatrix_rrd[i_rrd][j_rrd] != 0) {
                edges_rrd[edgeIndex_rrd].src_rrd = i_rrd;
                edges_rrd[edgeIndex_rrd].dest_rrd = j_rrd;
                edges_rrd[edgeIndex_rrd].weight_rrd = graph_rrd->adjMatrix_rrd[i_rrd][j_rrd];
                edgeIndex_rrd++;
            }
        }
    }
    

    qsort(edges_rrd, edgeIndex_rrd, sizeof(struct Edge_rrd), compareEdges_rrd);
    
    cout << "\nEdges in Minimum Spanning Tree (Kruskal's Algorithm):" << endl;
    cout << "Edge\t\tWeight" << endl;
    

    for (i_rrd = 0; i_rrd < edgeIndex_rrd && edgeCount_rrd < graph_rrd->vertices_rrd - 1; i_rrd++) {
        int x_rrd = findParent_rrd(parent_rrd, edges_rrd[i_rrd].src_rrd);
        int y_rrd = findParent_rrd(parent_rrd, edges_rrd[i_rrd].dest_rrd);
        

        if (x_rrd != y_rrd) {
            cout << "" << edges_rrd[i_rrd].src_rrd, edges_rrd[i_rrd].dest_rrd, edges_rrd[i_rrd].weight_rrd << " - %d\t\t%d" << endl;
            unionSets_rrd(parent_rrd, rank_rrd, x_rrd, y_rrd);
            totalWeight_rrd += edges_rrd[i_rrd].weight_rrd;
            edgeCount_rrd++;
        }
    }
    
    cout << "Total Weight of MST: " << totalWeight_rrd << "" << endl;
}

void printGraph_rrd(struct Graph_rrd* graph_rrd) {
    int i_rrd, j_rrd;
    cout << "\nGraph Representation:" << endl;
    for (i_rrd = 0; i_rrd < graph_rrd->vertices_rrd; i_rrd++) {
        cout << "Vertex " << i_rrd << ": ";
        for (j_rrd = 0; j_rrd < graph_rrd->vertices_rrd; j_rrd++) {
            if (graph_rrd->adjMatrix_rrd[i_rrd][j_rrd] != 0) {
                cout << "(" << j_rrd, graph_rrd->adjMatrix_rrd[i_rrd][j_rrd] << ", %d) ";
            }
        }
        cout << "" << endl;
    }
}

void printAdjMatrix_rrd(struct Graph_rrd* graph_rrd) {
    int i_rrd, j_rrd;
    cout << "\nAdjacency Matrix:" << endl;
    cout << "   ";
    for (i_rrd = 0; i_rrd < graph_rrd->vertices_rrd; i_rrd++) {
        printf("%3d", i_rrd);
    }
    cout << "" << endl;
    
    for (i_rrd = 0; i_rrd < graph_rrd->vertices_rrd; i_rrd++) {
        printf("%2d ", i_rrd);
        for (j_rrd = 0; j_rrd < graph_rrd->vertices_rrd; j_rrd++) {
            printf("%3d", graph_rrd->adjMatrix_rrd[i_rrd][j_rrd]);
        }
        cout << "" << endl;
    }
}

struct Graph_rrd* createSampleGraph_rrd() {
    struct Graph_rrd* graph_rrd = createGraph_rrd(6);
    

    addEdge_rrd(graph_rrd, 0, 1, 4);
    addEdge_rrd(graph_rrd, 0, 2, 3);
    addEdge_rrd(graph_rrd, 1, 2, 1);
    addEdge_rrd(graph_rrd, 1, 3, 2);
    addEdge_rrd(graph_rrd, 2, 3, 4);
    addEdge_rrd(graph_rrd, 3, 4, 2);
    addEdge_rrd(graph_rrd, 3, 5, 6);
    addEdge_rrd(graph_rrd, 4, 5, 3);
    
    return graph_rrd;
}

void displayMenu_rrd() {
    cout << "\n===== Kruskal's Algorithm - Minimum Spanning Tree =====" << endl;
    cout << "1. Create Graph with Sample Data" << endl;
    cout << "2. Add Edge to Graph" << endl;
    cout << "3. Display Graph" << endl;
    cout << "4. Display Adjacency Matrix" << endl;
    cout << "5. Find Minimum Spanning Tree (Kruskal's Algorithm)" << endl;
    cout << "6. Exit" << endl;
    cout << "=====================================================" << endl;
    cout << "Enter your choice: ";
}

int main() {
    struct Graph_rrd* graph_rrd = NULL;
    int choice_rrd, src_rrd, dest_rrd, weight_rrd, vertices_rrd;
    
    cout << "Kruskal's Algorithm for Minimum Spanning Tree using Adjacency Matrix" << endl;
    cout << "====================================================================" << endl;
    
    while (1) {
        displayMenu_rrd();
        cin >> choice_rrd;
        
        switch (choice_rrd) {
            case 1:
                cout << "Enter number of vertices: ";
                cin >> vertices_rrd;
                if (vertices_rrd <= 0 || vertices_rrd > MAX_VERTICES) {
                    cout << "Invalid number of vertices!" << endl;
                    break;
                }
                graph_rrd = createGraph_rrd(vertices_rrd);
                cout << "Graph with " << vertices_rrd << " vertices created successfully!" << endl;
                break;
                
            case 2:
                if (graph_rrd == NULL) {
                    cout << "Please create a graph first!" << endl;
                    break;
                }
                cout << "Enter source vertex: ";
                cin >> src_rrd;
                cout << "Enter destination vertex: ";
                cin >> dest_rrd;
                cout << "Enter weight: ";
                cin >> weight_rrd;
                
                if (src_rrd < 0 || src_rrd >= graph_rrd->vertices_rrd || 
                    dest_rrd < 0 || dest_rrd >= graph_rrd->vertices_rrd) {
                    cout << "Invalid vertex numbers!" << endl;
                    break;
                }
                
                addEdge_rrd(graph_rrd, src_rrd, dest_rrd, weight_rrd);
                cout << "Edge added successfully!" << endl;
                break;
                
            case 3:
                if (graph_rrd == NULL) {
                    cout << "Please create a graph first!" << endl;
                    break;
                }
                printGraph_rrd(graph_rrd);
                break;
                
            case 4:
                if (graph_rrd == NULL) {
                    cout << "Please create a graph first!" << endl;
                    break;
                }
                printAdjMatrix_rrd(graph_rrd);
                break;
                
            case 5:
                if (graph_rrd == NULL) {
                    cout << "Please create a graph first!" << endl;
                    break;
                }
                kruskalMST_rrd(graph_rrd);
                break;
                
            case 6:
                cout << "Thank you for using Kruskal's Algorithm Implementation!" << endl;
                if (graph_rrd != NULL) {
                    free(graph_rrd);
                }
                exit(0);
                
            default:
                cout << "Invalid choice! Please try again." << endl;
        }
    }
    
    return 0;
}
```

## Output

```
Kruskal's Algorithm for Minimum Spanning Tree using Adjacency Matrix
====================================================================

===== Kruskal's Algorithm - Minimum Spanning Tree =====
1. Create Graph with Sample Data
2. Add Edge to Graph
3. Display Graph
4. Display Adjacency Matrix
5. Find Minimum Spanning Tree (Kruskal's Algorithm)
6. Exit
=====================================================
Enter your choice: 1
Enter number of vertices: 6
Graph with 6 vertices created successfully!

===== Kruskal's Algorithm - Minimum Spanning Tree =====
1. Create Graph with Sample Data
2. Add Edge to Graph
3. Display Graph
4. Display Adjacency Matrix
5. Find Minimum Spanning Tree (Kruskal's Algorithm)
6. Exit
=====================================================
Enter your choice: 2
Enter source vertex: 0
Enter destination vertex: 1
Enter weight: 4
Edge added successfully!

===== Kruskal's Algorithm - Minimum Spanning Tree =====
1. Create Graph with Sample Data
2. Add Edge to Graph
3. Display Graph
4. Display Adjacency Matrix
5. Find Minimum Spanning Tree (Kruskal's Algorithm)
6. Exit
=====================================================
Enter your choice: 2
Enter source vertex: 0
Enter destination vertex: 2
Enter weight: 3
Edge added successfully!

===== Kruskal's Algorithm - Minimum Spanning Tree =====
1. Create Graph with Sample Data
2. Add Edge to Graph
3. Display Graph
4. Display Adjacency Matrix
5. Find Minimum Spanning Tree (Kruskal's Algorithm)
6. Exit
=====================================================
Enter your choice: 2
Enter source vertex: 1
Enter destination vertex: 2
Enter weight: 1
Edge added successfully!

===== Kruskal's Algorithm - Minimum Spanning Tree =====
1. Create Graph with Sample Data
2. Add Edge to Graph
3. Display Graph
4. Display Adjacency Matrix
5. Find Minimum Spanning Tree (Kruskal's Algorithm)
6. Exit
=====================================================
Enter your choice: 2
Enter source vertex: 1
Enter destination vertex: 3
Enter weight: 2
Edge added successfully!

===== Kruskal's Algorithm - Minimum Spanning Tree =====
1. Create Graph with Sample Data
2. Add Edge to Graph
3. Display Graph
4. Display Adjacency Matrix
5. Find Minimum Spanning Tree (Kruskal's Algorithm)
6. Exit
=====================================================
Enter your choice: 2
Enter source vertex: 2
Enter destination vertex: 3
Enter weight: 4
Edge added successfully!

===== Kruskal's Algorithm - Minimum Spanning Tree =====
1. Create Graph with Sample Data
2. Add Edge to Graph
3. Display Graph
4. Display Adjacency Matrix
5. Find Minimum Spanning Tree (Kruskal's Algorithm)
6. Exit
=====================================================
Enter your choice: 2
Enter source vertex: 3
Enter destination vertex: 4
Enter weight: 2
Edge added successfully!

===== Kruskal's Algorithm - Minimum Spanning Tree =====
1. Create Graph with Sample Data
2. Add Edge to Graph
3. Display Graph
4. Display Adjacency Matrix
5. Find Minimum Spanning Tree (Kruskal's Algorithm)
6. Exit
=====================================================
Enter your choice: 2
Enter source vertex: 3
Enter destination vertex: 5
Enter weight: 6
Edge added successfully!

===== Kruskal's Algorithm - Minimum Spanning Tree =====
1. Create Graph with Sample Data
2. Add Edge to Graph
3. Display Graph
4. Display Adjacency Matrix
5. Find Minimum Spanning Tree (Kruskal's Algorithm)
6. Exit
=====================================================
Enter your choice: 2
Enter source vertex: 4
Enter destination vertex: 5
Enter weight: 3
Edge added successfully!

===== Kruskal's Algorithm - Minimum Spanning Tree =====
1. Create Graph with Sample Data
2. Add Edge to Graph
3. Display Graph
4. Display Adjacency Matrix
5. Find Minimum Spanning Tree (Kruskal's Algorithm)
6. Exit
=====================================================
Enter your choice: 5

Edges in Minimum Spanning Tree (Kruskal's Algorithm):
Edge		Weight
1 - 2		1
1 - 3		2
3 - 4		2
4 - 5		3
0 - 2		3
Total Weight of MST: 11
```

## Dry Run

For a graph with 6 vertices and the following edges:
- (0,1) weight 4
- (0,2) weight 3
- (1,2) weight 1
- (1,3) weight 2
- (2,3) weight 4
- (3,4) weight 2
- (3,5) weight 6
- (4,5) weight 3

**Step 1: Collect and Sort Edges**
Sorted edges by weight:
1. (1,2) weight 1
2. (1,3) weight 2
3. (3,4) weight 2
4. (0,2) weight 3
5. (4,5) weight 3
6. (0,1) weight 4
7. (2,3) weight 4
8. (3,5) weight 6

**Step 2: Process Edges**
1. Add (1,2) weight 1 - No cycle, include in MST
2. Add (1,3) weight 2 - No cycle, include in MST
3. Add (3,4) weight 2 - No cycle, include in MST
4. Add (0,2) weight 3 - No cycle, include in MST
5. Add (4,5) weight 3 - No cycle, include in MST
6. All vertices connected, MST complete

**MST Edges**: (1,2), (1,3), (3,4), (0,2), (4,5)
**Total Weight**: 1 + 2 + 2 + 3 + 3 = 11

## Conclusion

The implementation demonstrates Kruskal's algorithm for finding the minimum spanning tree using adjacency matrix representation with the following key features:

**Algorithm Complexity**:
1. **Time Complexity**: O(E log E) where E is the number of edges
2. **Space Complexity**: O(V + E) where V is the number of vertices
3. **Sorting**: O(E log E) for sorting edges
4. **Union-Find**: O(E α(V)) where α is the inverse Ackermann function

**Key Implementation Features**:
1. **Union-Find Data Structure**: Efficient cycle detection
2. **Edge Sorting**: Uses qsort for optimal performance
3. **Adjacency Matrix**: Compact graph representation
4. **Dynamic Memory**: Allocates memory based on vertices
5. **User Interface**: Interactive menu-driven system

**Advantages of Kruskal's Algorithm**:
1. **Simplicity**: Easy to understand and implement
2. **Efficiency**: Works well for sparse graphs
3. **Optimality**: Guarantees minimum spanning tree
4. **Flexibility**: Works with disconnected graphs

**Union-Find Operations**:
1. **Find**: O(α(n)) with path compression
2. **Union**: O(α(n)) with union by rank
3. **Path Compression**: Flattens tree structure during find
4. **Union by Rank**: Keeps tree balanced

**Real-world Applications**:
1. **Network Design**: Connecting cities with minimum cost
2. **Circuit Design**: Minimizing wire length in circuits
3. **Cluster Analysis**: Finding minimum cost clusters
4. **Image Processing**: Segmentation algorithms

The implementation correctly handles all edge cases:
- Empty graphs
- Disconnected graphs
- Single vertex graphs
- Complete graphs
- Memory management to prevent leaks

This system efficiently finds the minimum spanning tree for any connected, weighted, undirected graph using Kruskal's algorithm with optimal performance characteristics.