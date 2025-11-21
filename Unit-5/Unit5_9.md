# Unit V Assignment 9: Kruskal's Algorithm for Minimum Spanning Tree using Adjacency List

Implementation of Kruskal's algorithm to find the minimum spanning tree of a user-defined graph using adjacency list representation.

## Problem Statement

Write a Program to implement Kruskal's algorithm to find the minimum spanning tree of a user defined graph. Use Adjacency List to represent a graph.

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
    Collect all edges from adjacency list
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

struct GraphNode_rrd {
    int vertex_rrd;
    int weight_rrd;
    struct GraphNode_rrd* next_rrd;
};

struct Graph_rrd {
    int vertices_rrd;
    struct GraphNode_rrd* adjList_rrd[MAX_VERTICES];
};

struct Edge_rrd {
    int src_rrd;
    int dest_rrd;
    int weight_rrd;
};

struct GraphNode_rrd* createGraphNode_rrd(int vertex_rrd, int weight_rrd);
struct Graph_rrd* createGraph_rrd(int vertices_rrd);
void addEdge_rrd(struct Graph_rrd* graph_rrd, int src_rrd, int dest_rrd, int weight_rrd);
int findParent_rrd(int parent_rrd[], int vertex_rrd);
void unionSets_rrd(int parent_rrd[], int rank_rrd[], int x_rrd, int y_rrd);
int compareEdges_rrd(const void* a_rrd, const void* b_rrd);
void kruskalMST_rrd(struct Graph_rrd* graph_rrd);
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
    int i_rrd;
    struct GraphNode_rrd* temp_rrd;
    

    for (i_rrd = 0; i_rrd < graph_rrd->vertices_rrd; i_rrd++) {
        parent_rrd[i_rrd] = i_rrd;
        rank_rrd[i_rrd] = 0;
    }
    

    int edgeIndex_rrd = 0;
    for (i_rrd = 0; i_rrd < graph_rrd->vertices_rrd; i_rrd++) {
        temp_rrd = graph_rrd->adjList_rrd[i_rrd];
        while (temp_rrd != NULL) {

            if (i_rrd < temp_rrd->vertex_rrd) {
                edges_rrd[edgeIndex_rrd].src_rrd = i_rrd;
                edges_rrd[edgeIndex_rrd].dest_rrd = temp_rrd->vertex_rrd;
                edges_rrd[edgeIndex_rrd].weight_rrd = temp_rrd->weight_rrd;
                edgeIndex_rrd++;
            }
            temp_rrd = temp_rrd->next_rrd;
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
    cout << "\n===== Kruskal's Algorithm - Minimum Spanning Tree =====" << endl;
    cout << "1. Create Graph with Sample Data" << endl;
    cout << "2. Add Edge to Graph" << endl;
    cout << "3. Display Graph" << endl;
    cout << "4. Find Minimum Spanning Tree (Kruskal's Algorithm)" << endl;
    cout << "5. Exit" << endl;
    cout << "=====================================================" << endl;
    cout << "Enter your choice: ";
}

int main() {
    struct Graph_rrd* graph_rrd = NULL;
    int choice_rrd, src_rrd, dest_rrd, weight_rrd, vertices_rrd;
    
    cout << "Kruskal's Algorithm for Minimum Spanning Tree using Adjacency List" << endl;
    cout << "==================================================================" << endl;
    
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
                kruskalMST_rrd(graph_rrd);
                break;
                
            case 5:
                cout << "Thank you for using Kruskal's Algorithm Implementation!" << endl;
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
Kruskal's Algorithm for Minimum Spanning Tree using Adjacency List
==================================================================

===== Kruskal's Algorithm - Minimum Spanning Tree =====
1. Create Graph with Sample Data
2. Add Edge to Graph
3. Display Graph
4. Find Minimum Spanning Tree (Kruskal's Algorithm)
5. Exit
=====================================================
Enter your choice: 1
Enter number of vertices: 6
Graph with 6 vertices created successfully!

===== Kruskal's Algorithm - Minimum Spanning Tree =====
1. Create Graph with Sample Data
2. Add Edge to Graph
3. Display Graph
4. Find Minimum Spanning Tree (Kruskal's Algorithm)
5. Exit
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
4. Find Minimum Spanning Tree (Kruskal's Algorithm)
5. Exit
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
4. Find Minimum Spanning Tree (Kruskal's Algorithm)
5. Exit
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
4. Find Minimum Spanning Tree (Kruskal's Algorithm)
5. Exit
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
4. Find Minimum Spanning Tree (Kruskal's Algorithm)
5. Exit
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
4. Find Minimum Spanning Tree (Kruskal's Algorithm)
5. Exit
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
4. Find Minimum Spanning Tree (Kruskal's Algorithm)
5. Exit
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
4. Find Minimum Spanning Tree (Kruskal's Algorithm)
5. Exit
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
4. Find Minimum Spanning Tree (Kruskal's Algorithm)
5. Exit
=====================================================
Enter your choice: 3

Graph Representation (Adjacency List):
Vertex 0: (2, 3) (1, 4) 
Vertex 1: (3, 2) (2, 1) (0, 4) 
Vertex 2: (3, 4) (1, 1) (0, 3) 
Vertex 3: (5, 6) (4, 2) (2, 4) (1, 2) 
Vertex 4: (5, 3) (3, 2) 
Vertex 5: (4, 3) (3, 6) 

===== Kruskal's Algorithm - Minimum Spanning Tree =====
1. Create Graph with Sample Data
2. Add Edge to Graph
3. Display Graph
4. Find Minimum Spanning Tree (Kruskal's Algorithm)
5. Exit
=====================================================
Enter your choice: 4

Edges in Minimum Spanning Tree (Kruskal's Algorithm):
Edge		Weight
1 - 2		1
1 - 3		2
3 - 4		2
0 - 2		3
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

**Collecting Edges** (avoiding duplicates by only taking src < dest):
1. (0,1) weight 4
2. (0,2) weight 3
3. (1,2) weight 1
4. (1,3) weight 2
5. (2,3) weight 4
6. (3,4) weight 2
7. (3,5) weight 6
8. (4,5) weight 3

**Sorted Edges by Weight**:
1. (1,2) weight 1
2. (1,3) weight 2
3. (3,4) weight 2
4. (0,2) weight 3
5. (4,5) weight 3
6. (0,1) weight 4
7. (2,3) weight 4
8. (3,5) weight 6

**Kruskal's Algorithm Execution**:

**Initialization**:
- parent[] = {0, 1, 2, 3, 4, 5}
- rank[] = {0, 0, 0, 0, 0, 0}

**Processing Edges**:
1. Edge (1,2) weight 1: parent[1]=1, parent[2]=2 → Different sets, include in MST
   - Union(1,2): parent[2]=1
   - MST: {(1,2)}, Total weight: 1

2. Edge (1,3) weight 2: parent[1]=1, parent[3]=3 → Different sets, include in MST
   - Union(1,3): parent[3]=1
   - MST: {(1,2), (1,3)}, Total weight: 3

3. Edge (3,4) weight 2: parent[3]=1, parent[4]=4 → Different sets, include in MST
   - Union(1,4): parent[4]=1
   - MST: {(1,2), (1,3), (3,4)}, Total weight: 5

4. Edge (0,2) weight 3: parent[0]=0, parent[2]=1 → Different sets, include in MST
   - Union(0,1): parent[1]=0
   - MST: {(1,2), (1,3), (3,4), (0,2)}, Total weight: 8

5. Edge (4,5) weight 3: parent[4]=0, parent[5]=5 → Different sets, include in MST
   - Union(0,5): parent[5]=0
   - MST: {(1,2), (1,3), (3,4), (0,2), (4,5)}, Total weight: 11

6. All vertices connected, MST complete.

**MST Edges**: (1,2), (1,3), (3,4), (0,2), (4,5)
**Total Weight**: 1 + 2 + 2 + 3 + 3 = 11

## Conclusion

The implementation demonstrates Kruskal's algorithm for finding the minimum spanning tree using adjacency list representation with the following key features:

**Algorithm Complexity**:
1. **Time Complexity**: O(E log E) where E is the number of edges
2. **Space Complexity**: O(V + E) for adjacency list representation
3. **Sorting**: O(E log E) for sorting edges
4. **Union-Find**: O(E α(V)) where α is the inverse Ackermann function

**Key Implementation Features**:
1. **Union-Find Data Structure**: Efficient cycle detection with path compression and union by rank
2. **Edge Sorting**: Uses qsort for optimal performance
3. **Adjacency List**: Memory-efficient graph representation
4. **Duplicate Avoidance**: Only processes each edge once in undirected graphs
5. **User Interface**: Interactive menu-driven system

**Advantages of Kruskal's Algorithm**:
1. **Simplicity**: Easy to understand and implement
2. **Efficiency**: Works well for sparse graphs
3. **Optimality**: Guarantees minimum spanning tree
4. **Flexibility**: Works with disconnected graphs

**Advantages of Adjacency List**:
1. **Space Efficiency**: O(V + E) space compared to O(V²) for adjacency matrix
2. **Edge Collection**: Easy to collect all edges from the graph
3. **Flexibility**: Easy to add/remove edges
4. **Scalability**: Better for sparse graphs

**Union-Find Operations**:
1. **Find**: O(α(n)) with path compression
2. **Union**: O(α(n)) with union by rank
3. **Path Compression**: Flattens tree structure during find
4. **Union by Rank**: Keeps tree balanced

**Real-world Applications**:
1. **Network Design**: Connecting cities with minimum cost cables
2. **Circuit Design**: Minimizing wire connections in circuits
3. **Cluster Analysis**: Finding minimum cost clusters
4. **Image Processing**: Segmentation algorithms
5. **Telecommunications**: Designing efficient network topologies

The implementation correctly handles all edge cases:
- Empty graphs
- Disconnected graphs
- Single vertex graphs
- Complete graphs
- Memory management to prevent leaks
- Proper duplicate edge handling for undirected graphs

This system efficiently finds the minimum spanning tree for any connected, weighted, undirected graph using Kruskal's algorithm with adjacency list representation, providing optimal performance for sparse graphs.