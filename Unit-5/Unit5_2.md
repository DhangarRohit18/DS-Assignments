# Unit V Assignment 2: Prim's Algorithm for Minimum Spanning Tree using Adjacency List

Implementation of Prim's algorithm to find the minimum spanning tree of a user-defined graph using adjacency list representation.

## Problem Statement

Write a Program to implement Prim's algorithm to find minimum spanning tree of a user defined graph. Use Adjacency List to represent a graph.

## Pseudo Code

### Graph Structure

Structure GraphNode:
    vertex: integer
    weight: integer
    next: pointer to GraphNode
Structure Graph:
    vertices: integer
    adjList: array of pointers to GraphNode of size vertices


### Find Minimum Key

Algorithm FindMinKey(key, mstSet, vertices):
    min = INFINITY
    minIndex = -1
    For i = 0 to vertices-1:
        If mstSet[i] is false AND key[i] < min:
            min = key[i]
            minIndex = i
    Return minIndex


### Prim's Algorithm

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


## Code Implementation

```cpp
#include <iostream>
using namespace std;
#include <stdlib.h>
#include <limits.h>
#define MAX_VERTICES 100
struct GraphNode_rrd {
    int vertex_rrd;
    int weight_rrd;
    struct GraphNode_rrd* next_rrd;
}

struct Graph_rrd {
    int vertices_rrd;
    struct GraphNode_rrd* adjList_rrd[MAX_VERTICES];
}
struct GraphNode_rrd* createGraphNode_rrd(int vertex_rrd, int weight_rrd);
struct Graph_rrd* createGraph_rrd(int vertices_rrd);
void addEdge_rrd(struct Graph_rrd* graph_rrd, int src_rrd, int dest_rrd, int weight_rrd);
int findMinKey_rrd(int key_rrd[], int mstSet_rrd[], int vertices_rrd);
void primsMST_rrd(struct Graph_rrd* graph_rrd);
void printGraph_rrd(struct Graph_rrd* graph_rrd);
void freeGraph_rrd(struct Graph_rrd* graph_rrd);
struct Graph_rrd* createSampleGraph_rrd();
void displayMenu_rrd();
struct GraphNode_rrd* createGraphNode_rrd(int vertex_rrd, int weight_rrd)
{
    struct GraphNode_rrd* newNode_rrd = (struct GraphNode_rrd*)malloc(sizeof(struct GraphNode_rrd));
    newNode_rrd->vertex_rrd = vertex_rrd;
    newNode_rrd->weight_rrd = weight_rrd;
    newNode_rrd->next_rrd = NULL;
    return newNode_rrd;
}
struct Graph_rrd* createGraph_rrd(int vertices_rrd)
{
    struct Graph_rrd* graph_rrd = (struct Graph_rrd*)malloc(sizeof(struct Graph_rrd));
    int i_rrd;
    graph_rrd->vertices_rrd = vertices_rrd;
    for (i_rrd = 0; i_rrd < vertices_rrd; i_rrd++)
    {
        graph_rrd->adjList_rrd[i_rrd] = NULL;
    }
    return graph_rrd;
}
void addEdge_rrd(struct Graph_rrd* graph_rrd, int src_rrd, int dest_rrd, int weight_rrd)
{
    struct GraphNode_rrd* newNode_rrd = createGraphNode_rrd(dest_rrd, weight_rrd);
    newNode_rrd->next_rrd = graph_rrd->adjList_rrd[src_rrd];
    graph_rrd->adjList_rrd[src_rrd] = newNode_rrd;
    newNode_rrd = createGraphNode_rrd(src_rrd, weight_rrd);
    newNode_rrd->next_rrd = graph_rrd->adjList_rrd[dest_rrd];
    graph_rrd->adjList_rrd[dest_rrd] = newNode_rrd;
}
int findMinKey_rrd(int key_rrd[], int mstSet_rrd[], int vertices_rrd)
{
    int min_rrd = INT_MAX, minIndex_rrd = -1;
    int v_rrd;
    for (v_rrd = 0; v_rrd < vertices_rrd; v_rrd++)
    {
        if (mstSet_rrd[v_rrd] == 0 && key_rrd[v_rrd] < min_rrd)
        {
            min_rrd = key_rrd[v_rrd];
            minIndex_rrd = v_rrd;
        }
    }
    return minIndex_rrd;
}

void primsMST_rrd(struct Graph_rrd* graph_rrd)
{
    int parent_rrd[MAX_VERTICES];
    int key_rrd[MAX_VERTICES];
    int mstSet_rrd[MAX_VERTICES];
    int i_rrd, count_rrd, u_rrd, v_rrd;
    struct GraphNode_rrd* temp_rrd;
    int totalWeight_rrd = 0;
    int weight_rrd;
    for (i_rrd = 0; i_rrd < graph_rrd->vertices_rrd; i_rrd++)
    {
        key_rrd[i_rrd] = INT_MAX;
        mstSet_rrd[i_rrd] = 0;
    }
    key_rrd[0] = 0;
    parent_rrd[0] = -1;
    for (count_rrd = 0; count_rrd < graph_rrd->vertices_rrd - 1; count_rrd++)
    {
        u_rrd = findMinKey_rrd(key_rrd, mstSet_rrd, graph_rrd->vertices_rrd);
        mstSet_rrd[u_rrd] = 1;
        temp_rrd = graph_rrd->adjList_rrd[u_rrd];
        while (temp_rrd != NULL)
        {
            v_rrd = temp_rrd->vertex_rrd;
            if (mstSet_rrd[v_rrd] == 0 && temp_rrd->weight_rrd < key_rrd[v_rrd])
            {
                parent_rrd[v_rrd] = u_rrd;
                key_rrd[v_rrd] = temp_rrd->weight_rrd;
            }
            temp_rrd = temp_rrd->next_rrd;
        }
    }

    cout << "\nEdges in Minimum Spanning Tree (Prim's Algorithm):" << endl;
    cout << "Edge\t\tWeight" << endl;
    for (i_rrd = 1; i_rrd < graph_rrd->vertices_rrd; i_rrd++)
    {
        weight_rrd = 0;
        temp_rrd = graph_rrd->adjList_rrd[parent_rrd[i_rrd]];
        while (temp_rrd != NULL)
        {
            if (temp_rrd->vertex_rrd == i_rrd)
            {
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
void printGraph_rrd(struct Graph_rrd* graph_rrd)
{
    int v_rrd;
    struct GraphNode_rrd* temp_rrd;
    cout << "\nGraph Representation (Adjacency List):" << endl;
    for (v_rrd = 0; v_rrd < graph_rrd->vertices_rrd; v_rrd++)
    {
        temp_rrd = graph_rrd->adjList_rrd[v_rrd];
        cout << "Vertex " << v_rrd << ": ";
        while (temp_rrd)
        {
            cout << "(" << temp_rrd->vertex_rrd, temp_rrd->weight_rrd << ", %d) ";
            temp_rrd = temp_rrd->next_rrd;
        }
        cout << "" << endl;
    }
}
void freeGraph_rrd(struct Graph_rrd* graph_rrd)
{
    int i_rrd;
    struct GraphNode_rrd* temp_rrd;
    struct GraphNode_rrd* next_rrd;
    for (i_rrd = 0; i_rrd < graph_rrd->vertices_rrd; i_rrd++)
    {
        temp_rrd = graph_rrd->adjList_rrd[i_rrd];
        while (temp_rrd)
        {
            next_rrd = temp_rrd->next_rrd;
            free(temp_rrd);
            temp_rrd = next_rrd;
        }
    free(graph_rrd);
    }
}

struct Graph_rrd* createSampleGraph_rrd()
{
    struct Graph_rrd* graph_rrd = createGraph_rrd(6);
    addEdge_rrd(graph_rrd, 0, 1, 4);
    addEdge_rrd(graph_rrd, 0, 2, 3);
    addEdge_rrd(graph_rrd, 1, 2, 1);
    addEdge_rrd(graph_rrd, 1, 3, 2);
    addEdge_rrd(graph_rrd, 2, 3, 4);
    addEdge_rrd(graph_rrd, 3, 4, 2);
    addEdge_rrd(graph_rrd, 4, 5, 6);
    return graph_rrd;
}

void displayMenu_rrd()
{
    cout << "\n===== Prim's Algorithm for Minimum Spanning Tree =====" << endl;
    cout << "1. Add Edge" << endl;
    cout << "2. Print Graph" << endl;
    cout << "3. Find Minimum Spanning Tree (Prim's Algorithm)" << endl;
    cout << "4. Create Sample Graph" << endl;
    cout << "5. Exit" << endl;
    cout << "====================================================" << endl;
    cout << "Enter your choice: ";
{

int main()
{
    int vertices_rrd;
    struct Graph_rrd* graph_rrd;
    int choice_rrd;
    int src_rrd, dest_rrd, weight_rrd;
    cout << "Welcome to Prim's Algorithm for Minimum Spanning Tree!" << endl;
    cout << "Enter the number of vertices in the graph: ";
    cin >> vertices_rrd;
    if (vertices_rrd <= 0 || vertices_rrd > MAX_VERTICES)
    {
        cout << "Invalid number of vertices! Must be between 1 and " << MAX_VERTICES << "." << endl;
        return 1;
    }

    graph_rrd = createGraph_rrd(vertices_rrd);
    while (1)
    {
        displayMenu_rrd();
        cin >> choice_rrd;
        switch (choice_rrd)
        {
            case 1:
                cout << "Enter source vertex (0-" << vertices_rrd - 1 << "): ";
                cin >> src_rrd;
                cout << "Enter destination vertex (0-" << vertices_rrd - 1 << "): ";
                cin >> dest_rrd;
                cout << "Enter weight of edge: ";
                cin >> weight_rrd;
                if (src_rrd < 0 || src_rrd >= vertices_rrd || dest_rrd < 0 || dest_rrd >= vertices_rrd)
                {
                    cout << "Invalid vertex numbers!" << endl;
                }
                if (weight_rrd < 0)
                {
                    cout << "Edge weight cannot be negative!" << endl;
                }
                else
                {
                    addEdge_rrd(graph_rrd, src_rrd, dest_rrd, weight_rrd);
                    cout << "Edge added between " << src_rrd, dest_rrd, weight_rrd << " and %d with weight %d successfully!" << endl;
                }
                break;
            case 2:
                printGraph_rrd(graph_rrd);
                break;
            case 3:
                if (vertices_rrd < 2)
                {
                    cout << "Need at least 2 vertices to find MST!" << endl;
                }
                    primsMST_rrd(graph_rrd);
                }
                break;
            case 4:
                freeGraph_rrd(graph_rrd);
                graph_rrd = createSampleGraph_rrd();
                cout << "Sample graph created successfully!" << endl;
                printGraph_rrd(graph_rrd);
                break;
            case 5:
                cout << "Thank you for using Prim's Algorithm for Minimum Spanning Tree!" << endl;
                freeGraph_rrd(graph_rrd);
                exit(0);
            default:
                cout << "Invalid choice! Please try again." << endl;
            }
    }
    return 0;
    }
}
## Output
Welcome to Prim's Algorithm for Minimum Spanning Tree!
Enter the number of vertices in the graph: 6
===== Prim's Algorithm for Minimum Spanning Tree =====
1. Add Edge
2. Print Graph
3. Find Minimum Spanning Tree (Prim's Algorithm)
4. Create Sample Graph
5. Exit
====================================================
Enter your choice: 4
Sample graph created successfully!
Graph Representation (Adjacency List):
Vertex 0: (2, 3) (1, 4) 
Vertex 1: (3, 2) (2, 1) (0, 4) 
Vertex 2: (3, 4) (1, 1) (0, 3) 
Vertex 3: (4, 2) (2, 4) (1, 2) 
Vertex 4: (5, 6) (3, 2) 
Vertex 5: (4, 6) 
===== Prim's Algorithm for Minimum Spanning Tree =====
1. Add Edge
2. Print Graph
3. Find Minimum Spanning Tree (Prim's Algorithm)
4. Create Sample Graph
5. Exit
====================================================
Enter your choice: 3
Edges in Minimum Spanning Tree (Prim's Algorithm):
Edge		Weight
0 - 2		3
2 - 1		1
1 - 3		2
3 - 4		2
4 - 5		6
Total Weight of MST: 14

## Dry Run

For a graph with 6 vertices and weighted edges:
- (0,1):4, (0,2):3, (1,2):1, (1,3):2, (2,3):4, (3,4):2, (4,5):6

1. **Initialization**:
   - key[] = [0, ∞, ∞, ∞, ∞, ∞]
   - mstSet[] = [0, 0, 0, 0, 0, 0]
   - parent[] = [-1, -1, -1, -1, -1, -1]

2. **First Iteration (u=0)**:
   - Add vertex 0 to MST: mstSet[0] = 1
   - Update adjacent vertices:
     * key[1] = 4, parent[1] = 0
     * key[2] = 3, parent[2] = 0
   - key[] = [0, 4, 3, ∞, ∞, ∞]

3. **Second Iteration (u=2)**:
   - Minimum key vertex: u=2
   - Add vertex 2 to MST: mstSet[2] = 1
   - Update adjacent vertices:
     * key[1] = 1 (1 < 4), parent[1] = 2
     * key[3] = 4
   - key[] = [0, 1, 3, 4, ∞, ∞]

4. **Third Iteration (u=1)**:
   - Minimum key vertex: u=1
   - Add vertex 1 to MST: mstSet[1] = 1
   - Update adjacent vertices:
     * key[3] = 2 (2 < 4), parent[3] = 1
   - key[] = [0, 1, 3, 2, ∞, ∞]

5. **Fourth Iteration (u=3)**:
   - Minimum key vertex: u=3
   - Add vertex 3 to MST: mstSet[3] = 1
   - Update adjacent vertices:
     * key[4] = 2, parent[4] = 3
   - key[] = [0, 1, 3, 2, 2, ∞]

6. **Fifth Iteration (u=4)**:
   - Minimum key vertex: u=4
   - Add vertex 4 to MST: mstSet[4] = 1
   - Update adjacent vertices:
     * key[5] = 6, parent[5] = 4
   - key[] = [0, 1, 3, 2, 2, 6]

7. **MST Construction**:
   - Edges: (0,2):3, (2,1):1, (1,3):2, (3,4):2, (4,5):6
   - Total Weight: 3+1+2+2+6 = 14

## Conclusion

The implementation demonstrates Prim's algorithm for finding the minimum spanning tree using adjacency list representation. Key features include:

1. **Adjacency List Representation**: Memory efficient for sparse graphs
2. **Prim's Algorithm**: Greedy approach to find minimum spanning tree
3. **Complete Operations**: All required graph operations plus additional utilities

**Time Complexities**:
- Add Edge: O(1) - constant time insertion at head of list
- Prim's Algorithm: O(V²) with adjacency list (can be improved to O(E log V) with priority queue)
- Print Graph: O(V + E) where V is vertices and E is edges

**Space Complexity**: O(V + E) for the adjacency list

The adjacency list approach is ideal for this application because:
1. **Memory Efficiency**: For sparse graphs, saves space compared to adjacency matrix
2. **Dynamic Size**: Can easily add/remove edges
3. **Easy Traversal**: Simple to iterate through adjacent vertices
4. **Weighted Edges**: Natural support for edge weights

The implementation handles edge cases properly:
- Invalid vertex numbers with appropriate error messages
- Negative weight validation
- Memory management to prevent leaks
- Comprehensive user interface with clear feedback

Additional features beyond requirements:
- Graph visualization through adjacency list display
- Sample graph creation for testing
- Interactive menu system
- Complete error handling
- Total MST weight calculation

In real-world applications, this system could be extended to:
1. Support directed graphs
2. Implement other MST algorithms (Kruskal's)
3. Add graphical visualization
4. Support dynamic graph resizing
5. Implement priority queue for better performance

Minimum Spanning Trees are used in:
1. **Network Design**: Creating cost-effective communication networks
2. **Cluster Analysis**: Finding clusters in data points
3. **Image Segmentation**: Identifying regions in images
4. **Approximation Algorithms**: Solving NP-hard problems
5. **Circuit Design**: Minimizing wire length in circuits

This implementation provides a solid foundation for understanding graph algorithms and minimum spanning trees, which are essential in computer science and network optimization.
