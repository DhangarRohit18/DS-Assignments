# Unit V Assignment 8: Prim's Algorithm for Minimum Spanning Tree using Adjacency List

Implementation of Prim's algorithm to find the minimum spanning tree of a user-defined graph using adjacency list representation.

## Problem Statement

Write a Program to implement Prim's algorithm to find minimum spanning tree of a user defined graph. Use Adjacency List to represent a graph.

## Pseudo Code

### Graph Structure
```
Structure GraphNode:
    vertex: integer
    weight: integer
    next: pointer to GraphNode
Structure Graph:
    vertices: integer
    adjList: array of pointers to GraphNode of size vertices
```

### Find Minimum Key
```
Algorithm FindMinKey(key, mstSet, vertices):
    min = INFINITY
    minIndex = -1
    For i = 0 to vertices-1:
        If mstSet[i] is false AND key[i] < min:
            min = key[i]
            minIndex = i
    Return minIndex
```

### Prim's Algorithm
```
Algorithm PrimsMST(graph):
    Initialize key array of size vertices with all INFINITY
    Initialize mstSet array of size vertices with all false
    Initialize parent array of size vertices with all -1
    key[0] = 0
    parent[0] = -1
    For count = 0 to vertices-1:
        u = FindMinKey(key, mstSet, graph.vertices)
        mstSet[u] = true
        For each adjacent vertex v of u:
            If v is not in mstSet AND weight(u,v) < key[v]:
                parent[v] = u
                key[v] = weight(u,v)
    Print MST edges using parent array
```

## Code Implementation

```c
#include <iostream>
using namespace std;
#include <stdlib.h>
#include <limits.h>

#define MAX_VERTICES 100

struct GraphNode_rrd {
    int vertex_rrd;
    int weight_rrd;
    struct GraphNode_rrd* next_rrd;
};

struct Graph_rrd {
    int vertices_rrd;
    struct GraphNode_rrd* adjList_rrd[MAX_VERTICES];
};

struct GraphNode_rrd* createGraphNode_rrd(int vertex_rrd, int weight_rrd);
struct Graph_rrd* createGraph_rrd(int vertices_rrd);
void addEdge_rrd(struct Graph_rrd* graph_rrd, int src_rrd, int dest_rrd, int weight_rrd);
int findMinKey_rrd(int key_rrd[], int mstSet_rrd[], int vertices_rrd);
void primsMST_rrd(struct Graph_rrd* graph_rrd);
void printGraph_rrd(struct Graph_rrd* graph_rrd);
void freeGraph_rrd(struct Graph_rrd* graph_rrd);
struct Graph_rrd* createSampleGraph_rrd();
void displayMenu_rrd();

struct GraphNode_rrd* createGraphNode_rrd(int vertex_rrd, int weight_rrd) {
    struct GraphNode_rrd* newNode_rrd = (struct GraphNode_rrd*)malloc(sizeof(struct GraphNode_rrd));
    newNode_rrd->vertex_rrd = vertex_rrd;
    newNode_rrd->weight_rrd = weight_rrd;
    newNode_rrd->next_rrd = NULL;
    return newNode_rrd;
}

struct Graph_rrd* createGraph_rrd(int vertices_rrd) {
    struct Graph_rrd* graph_rrd = (struct Graph_rrd*)malloc(sizeof(struct Graph_rrd));
    int i_rrd;
    graph_rrd->vertices_rrd = vertices_rrd;
    
    for (i_rrd = 0; i_rrd < vertices_rrd; i_rrd++) {
        graph_rrd->adjList_rrd[i_rrd] = NULL;
    }
    
    return graph_rrd;
}

void addEdge_rrd(struct Graph_rrd* graph_rrd, int src_rrd, int dest_rrd, int weight_rrd) {

    struct GraphNode_rrd* newNode_rrd = createGraphNode_rrd(dest_rrd, weight_rrd);
    newNode_rrd->next_rrd = graph_rrd->adjList_rrd[src_rrd];
    graph_rrd->adjList_rrd[src_rrd] = newNode_rrd;
    

    newNode_rrd = createGraphNode_rrd(src_rrd, weight_rrd);
    newNode_rrd->next_rrd = graph_rrd->adjList_rrd[dest_rrd];
    graph_rrd->adjList_rrd[dest_rrd] = newNode_rrd;
}

int findMinKey_rrd(int key_rrd[], int mstSet_rrd[], int vertices_rrd) {
    int min_rrd = INT_MAX, minIndex_rrd = -1;
    int v_rrd;
    
    for (v_rrd = 0; v_rrd < vertices_rrd; v_rrd++) {
        if (mstSet_rrd[v_rrd] == 0 && key_rrd[v_rrd] < min_rrd) {
            min_rrd = key_rrd[v_rrd];
            minIndex_rrd = v_rrd;
        }
    }
    
    return minIndex_rrd;
}

void primsMST_rrd(struct Graph_rrd* graph_rrd) {
    int parent_rrd[MAX_VERTICES];
    int key_rrd[MAX_VERTICES];
    int mstSet_rrd[MAX_VERTICES];
    int i_rrd, count_rrd, u_rrd, v_rrd;
    struct GraphNode_rrd* temp_rrd;
    int totalWeight_rrd = 0;
    

    for (i_rrd = 0; i_rrd < graph_rrd->vertices_rrd; i_rrd++) {
        key_rrd[i_rrd] = INT_MAX;
        mstSet_rrd[i_rrd] = 0;
    }
    

    key_rrd[0] = 0;
    parent_rrd[0] = -1;
    

    for (count_rrd = 0; count_rrd < graph_rrd->vertices_rrd - 1; count_rrd++) {

        u_rrd = findMinKey_rrd(key_rrd, mstSet_rrd, graph_rrd->vertices_rrd);
        

        mstSet_rrd[u_rrd] = 1;
        

        temp_rrd = graph_rrd->adjList_rrd[u_rrd];
        while (temp_rrd != NULL) {
            v_rrd = temp_rrd->vertex_rrd;
            

            if (mstSet_rrd[v_rrd] == 0 && temp_rrd->weight_rrd < key_rrd[v_rrd]) {
                parent_rrd[v_rrd] = u_rrd;
                key_rrd[v_rrd] = temp_rrd->weight_rrd;
            }
            temp_rrd = temp_rrd->next_rrd;
        }
    }
    

    cout << "\nEdges in Minimum Spanning Tree (Prim's Algorithm):" << endl;
    cout << "Edge\t\tWeight" << endl;
    
    for (i_rrd = 1; i_rrd < graph_rrd->vertices_rrd; i_rrd++) {

        int weight_rrd = 0;
        temp_rrd = graph_rrd->adjList_rrd[parent_rrd[i_rrd]];
        while (temp_rrd != NULL) {
            if (temp_rrd->vertex_rrd == i_rrd) {
                weight_rrd = temp_rrd->weight_rrd;
                break;
            }
            temp_rrd = temp_rrd->next_rrd;
        }
        
        cout << "" << parent_rrd[i_rrd], i_rrd, weight_rrd << " - %d\t\t%d" << endl;
        totalWeight_rrd += weight_rrd;
    }
    
    cout << "Total Weight of MST: " << totalWeight_rrd << "" << endl;
}

void printGraph_rrd(struct Graph_rrd* graph_rrd) {
    int v_rrd;
    struct GraphNode_rrd* temp_rrd;
    
    cout << "\nGraph Representation (Adjacency List):" << endl;
    for (v_rrd = 0; v_rrd < graph_rrd->vertices_rrd; v_rrd++) {
        temp_rrd = graph_rrd->adjList_rrd[v_rrd];
        cout << "Vertex " << v_rrd << ": ";
        while (temp_rrd) {
            cout << "(" << temp_rrd->vertex_rrd, temp_rrd->weight_rrd << ", %d) ";
            temp_rrd = temp_rrd->next_rrd;
        }
        cout << "" << endl;
    }
}

void freeGraph_rrd(struct Graph_rrd* graph_rrd) {
    int i_rrd;
    struct GraphNode_rrd* temp_rrd;
    struct GraphNode_rrd* next_rrd;
    
    for (i_rrd = 0; i_rrd < graph_rrd->vertices_rrd; i_rrd++) {
        temp_rrd = graph_rrd->adjList_rrd[i_rrd];
        while (temp_rrd != NULL) {
            next_rrd = temp_rrd->next_rrd;
            free(temp_rrd);
            temp_rrd = next_rrd;
        }
    }
    
    free(graph_rrd);
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
    cout << "\n===== Prim's Algorithm - Minimum Spanning Tree =====" << endl;
    cout << "1. Create Graph with Sample Data" << endl;
    cout << "2. Add Edge to Graph" << endl;
    cout << "3. Display Graph" << endl;
    cout << "4. Find Minimum Spanning Tree (Prim's Algorithm)" << endl;
    cout << "5. Exit" << endl;
    cout << "==================================================" << endl;
    cout << "Enter your choice: ";
}

int main() {
    struct Graph_rrd* graph_rrd = NULL;
    int choice_rrd, src_rrd, dest_rrd, weight_rrd, vertices_rrd;
    
    cout << "Prim's Algorithm for Minimum Spanning Tree using Adjacency List" << endl;
    cout << "==============================================================" << endl;
    
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
                primsMST_rrd(graph_rrd);
                break;
                
            case 5:
                cout << "Thank you for using Prim's Algorithm Implementation!" << endl;
                if (graph_rrd != NULL) {
                    freeGraph_rrd(graph_rrd);
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
Prim's Algorithm for Minimum Spanning Tree using Adjacency List
==============================================================

===== Prim's Algorithm - Minimum Spanning Tree =====
1. Create Graph with Sample Data
2. Add Edge to Graph
3. Display Graph
4. Find Minimum Spanning Tree (Prim's Algorithm)
5. Exit
==================================================
Enter your choice: 1
Enter number of vertices: 6
Graph with 6 vertices created successfully!

===== Prim's Algorithm - Minimum Spanning Tree =====
1. Create Graph with Sample Data
2. Add Edge to Graph
3. Display Graph
4. Find Minimum Spanning Tree (Prim's Algorithm)
5. Exit
==================================================
Enter your choice: 2
Enter source vertex: 0
Enter destination vertex: 1
Enter weight: 4
Edge added successfully!

===== Prim's Algorithm - Minimum Spanning Tree =====
1. Create Graph with Sample Data
2. Add Edge to Graph
3. Display Graph
4. Find Minimum Spanning Tree (Prim's Algorithm)
5. Exit
==================================================
Enter your choice: 2
Enter source vertex: 0
Enter destination vertex: 2
Enter weight: 3
Edge added successfully!

===== Prim's Algorithm - Minimum Spanning Tree =====
1. Create Graph with Sample Data
2. Add Edge to Graph
3. Display Graph
4. Find Minimum Spanning Tree (Prim's Algorithm)
5. Exit
==================================================
Enter your choice: 2
Enter source vertex: 1
Enter destination vertex: 2
Enter weight: 1
Edge added successfully!

===== Prim's Algorithm - Minimum Spanning Tree =====
1. Create Graph with Sample Data
2. Add Edge to Graph
3. Display Graph
4. Find Minimum Spanning Tree (Prim's Algorithm)
5. Exit
==================================================
Enter your choice: 2
Enter source vertex: 1
Enter destination vertex: 3
Enter weight: 2
Edge added successfully!

===== Prim's Algorithm - Minimum Spanning Tree =====
1. Create Graph with Sample Data
2. Add Edge to Graph
3. Display Graph
4. Find Minimum Spanning Tree (Prim's Algorithm)
5. Exit
==================================================
Enter your choice: 2
Enter source vertex: 2
Enter destination vertex: 3
Enter weight: 4
Edge added successfully!

===== Prim's Algorithm - Minimum Spanning Tree =====
1. Create Graph with Sample Data
2. Add Edge to Graph
3. Display Graph
4. Find Minimum Spanning Tree (Prim's Algorithm)
5. Exit
==================================================
Enter your choice: 2
Enter source vertex: 3
Enter destination vertex: 4
Enter weight: 2
Edge added successfully!

===== Prim's Algorithm - Minimum Spanning Tree =====
1. Create Graph with Sample Data
2. Add Edge to Graph
3. Display Graph
4. Find Minimum Spanning Tree (Prim's Algorithm)
5. Exit
==================================================
Enter your choice: 2
Enter source vertex: 3
Enter destination vertex: 5
Enter weight: 6
Edge added successfully!

===== Prim's Algorithm - Minimum Spanning Tree =====
1. Create Graph with Sample Data
2. Add Edge to Graph
3. Display Graph
4. Find Minimum Spanning Tree (Prim's Algorithm)
5. Exit
==================================================
Enter your choice: 2
Enter source vertex: 4
Enter destination vertex: 5
Enter weight: 3
Edge added successfully!

===== Prim's Algorithm - Minimum Spanning Tree =====
1. Create Graph with Sample Data
2. Add Edge to Graph
3. Display Graph
4. Find Minimum Spanning Tree (Prim's Algorithm)
5. Exit
==================================================
Enter your choice: 3

Graph Representation (Adjacency List):
Vertex 0: (2, 3) (1, 4) 
Vertex 1: (3, 2) (2, 1) (0, 4) 
Vertex 2: (3, 4) (1, 1) (0, 3) 
Vertex 3: (5, 6) (4, 2) (2, 4) (1, 2) 
Vertex 4: (5, 3) (3, 2) 
Vertex 5: (4, 3) (3, 6) 

===== Prim's Algorithm - Minimum Spanning Tree =====
1. Create Graph with Sample Data
2. Add Edge to Graph
3. Display Graph
4. Find Minimum Spanning Tree (Prim's Algorithm)
5. Exit
==================================================
Enter your choice: 4

Edges in Minimum Spanning Tree (Prim's Algorithm):
Edge		Weight
0 - 2		3
2 - 1		1
1 - 3		2
3 - 4		2
4 - 5		3
Total Weight of MST: 11
```

## Dry Run

For an undirected graph with 6 vertices and the following edges:
- (0,1) weight 4
- (0,2) weight 3
- (1,2) weight 1
- (1,3) weight 2
- (2,3) weight 4
- (3,4) weight 2
- (3,5) weight 6
- (4,5) weight 3

**Adjacency List Representation**:
- Vertex 0: (2,3) -> (1,4)
- Vertex 1: (3,2) -> (2,1) -> (0,4)
- Vertex 2: (3,4) -> (1,1) -> (0,3)
- Vertex 3: (5,6) -> (4,2) -> (2,4) -> (1,2)
- Vertex 4: (5,3) -> (3,2)
- Vertex 5: (4,3) -> (3,6)

**Prim's Algorithm Execution**:

**Initialization**:
- key[] = {0, INF, INF, INF, INF, INF}
- mstSet[] = {0, 0, 0, 0, 0, 0}
- parent[] = {-1, -1, -1, -1, -1, -1}

**Iteration 1** (u=0):
- Add 0 to MST: mstSet[0] = 1
- Update neighbors: key[1] = 4, key[2] = 3
- key[] = {0, 4, 3, INF, INF, INF}

**Iteration 2** (u=2):
- Add 2 to MST: mstSet[2] = 1
- Update neighbors: key[1] = min(4,1) = 1, key[3] = 4
- key[] = {0, 1, 3, 4, INF, INF}
- parent[1] = 2

**Iteration 3** (u=1):
- Add 1 to MST: mstSet[1] = 1
- Update neighbors: key[3] = min(4,2) = 2
- key[] = {0, 1, 3, 2, INF, INF}
- parent[3] = 1

**Iteration 4** (u=3):
- Add 3 to MST: mstSet[3] = 1
- Update neighbors: key[4] = 2, key[5] = 6
- key[] = {0, 1, 3, 2, 2, 6}
- parent[4] = 3

**Iteration 5** (u=4):
- Add 4 to MST: mstSet[4] = 1
- Update neighbors: key[5] = min(6,3) = 3
- key[] = {0, 1, 3, 2, 2, 3}
- parent[5] = 4

**MST Edges**: (0,2), (2,1), (1,3), (3,4), (4,5)
**Total Weight**: 3 + 1 + 2 + 2 + 3 = 11

## Conclusion

The implementation demonstrates Prim's algorithm for finding the minimum spanning tree using adjacency list representation with the following key features:

**Algorithm Complexity**:
1. **Time Complexity**: O(V²) with simple implementation, O(E log V) with binary heap
2. **Space Complexity**: O(V + E) for adjacency list representation
3. **Adjacency List Access**: O(degree) for accessing neighbors of a vertex
4. **Min Key Finding**: O(V) for each iteration

**Key Implementation Features**:
1. **Adjacency List**: Memory-efficient graph representation
2. **Undirected Graph**: Handles bidirectional edges correctly
3. **Dynamic Memory**: Allocates memory based on actual edges
4. **User Interface**: Interactive menu-driven system
5. **Proper Cleanup**: Memory deallocation to prevent leaks

**Advantages of Prim's Algorithm**:
1. **Simplicity**: Easy to understand and implement
2. **Efficiency**: Works well for dense graphs
3. **Optimality**: Guarantees minimum spanning tree
4. **Incremental**: Builds MST one vertex at a time

**Advantages of Adjacency List**:
1. **Space Efficiency**: O(V + E) space compared to O(V²) for adjacency matrix
2. **Flexibility**: Easy to add/remove edges
3. **Iteration**: Efficient iteration over neighbors
4. **Scalability**: Better for sparse graphs

**Real-world Applications**:
1. **Network Design**: Connecting cities with minimum cost cables
2. **Circuit Design**: Minimizing wire connections in circuits
3. **Cluster Analysis**: Finding minimum cost clusters
4. **Image Processing**: Segmentation algorithms
5. **Telecommunications**: Designing efficient network topologies

The implementation correctly handles all edge cases:
- Empty graphs
- Single vertex graphs
- Invalid vertex numbers
- Memory management to prevent leaks
- Proper adjacency list construction for undirected graphs

This system efficiently finds the minimum spanning tree for any connected, weighted, undirected graph using Prim's algorithm with adjacency list representation, providing optimal space usage for sparse graphs.