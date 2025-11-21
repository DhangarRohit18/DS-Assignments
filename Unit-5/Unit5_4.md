# Unit V Assignment 4: Dijkstra's Algorithm for Shortest Path using Adjacency List

Implementation of Dijkstra's algorithm to find the shortest distance between two nodes of a user-defined graph using adjacency list representation.

## Problem Statement

Write a Program to implement Dijkstra's algorithm to find shortest distance between two nodes of a user defined graph. Use Adjacency List to represent a graph.

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

### Min Heap Structure
```
Structure MinHeapNode:
    vertex: integer
    distance: integer
Structure MinHeap:
    size: integer
    capacity: integer
    pos: array to track position of vertices
    array: array of MinHeapNode
```

### Dijkstra's Algorithm
```
Algorithm Dijkstra(graph, src):
    Initialize distance array of size vertices with all INFINITY
    Initialize minHeap with capacity vertices
    distance[src] = 0
    Insert src into minHeap with distance 0
    While minHeap is not empty:
        minHeapNode = ExtractMin from minHeap
        u = minHeapNode.vertex
        For each adjacent vertex v of u:
            If distance[u] + weight(u,v) < distance[v]:
                distance[v] = distance[u] + weight(u,v)
                DecreaseKey of v in minHeap to new distance
    Print distance array
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

struct MinHeapNode_rrd {
    int vertex_rrd;
    int distance_rrd;
};

struct MinHeap_rrd {
    int size_rrd;
    int capacity_rrd;
    int* pos_rrd;
    struct MinHeapNode_rrd** array_rrd;
};

struct GraphNode_rrd* createGraphNode_rrd(int vertex_rrd, int weight_rrd);
struct Graph_rrd* createGraph_rrd(int vertices_rrd);
void addEdge_rrd(struct Graph_rrd* graph_rrd, int src_rrd, int dest_rrd, int weight_rrd);
struct MinHeapNode_rrd* createMinHeapNode_rrd(int vertex_rrd, int distance_rrd);
struct MinHeap_rrd* createMinHeap_rrd(int capacity_rrd);
void swapMinHeapNode_rrd(struct MinHeapNode_rrd** a_rrd, struct MinHeapNode_rrd** b_rrd);
void minHeapify_rrd(struct MinHeap_rrd* minHeap_rrd, int index_rrd);
int isEmpty_rrd(struct MinHeap_rrd* minHeap_rrd);
struct MinHeapNode_rrd* extractMin_rrd(struct MinHeap_rrd* minHeap_rrd);
void decreaseKey_rrd(struct MinHeap_rrd* minHeap_rrd, int vertex_rrd, int distance_rrd);
int isInMinHeap_rrd(struct MinHeap_rrd* minHeap_rrd, int vertex_rrd);
void printDistance_rrd(int distance_rrd[], int vertices_rrd, int src_rrd);
void dijkstra_rrd(struct Graph_rrd* graph_rrd, int src_rrd);
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
    graph_rrd->vertices_rrd = vertices_rrd;
    for (int i_rrd = 0; i_rrd < vertices_rrd; i_rrd++)
{
        graph_rrd->adjList_rrd[i_rrd] = NULL;
    }
    return graph_rrd;
}

void addEdge_rrd(struct Graph_rrd* graph_rrd, int src_rrd, int dest_rrd, int weight_rrd) {
    struct GraphNode_rrd* newNode_rrd = createGraphNode_rrd(dest_rrd, weight_rrd);
    newNode_rrd->next_rrd = graph_rrd->adjList_rrd[src_rrd];
    graph_rrd->adjList_rrd[src_rrd] = newNode_rrd;
}

struct MinHeapNode_rrd* createMinHeapNode_rrd(int vertex_rrd, int distance_rrd) {
    struct MinHeapNode_rrd* minHeapNode_rrd = (struct MinHeapNode_rrd*)malloc(sizeof(struct MinHeapNode_rrd));
    minHeapNode_rrd->vertex_rrd = vertex_rrd;
    minHeapNode_rrd->distance_rrd = distance_rrd;
    return minHeapNode_rrd;
}

struct MinHeap_rrd* createMinHeap_rrd(int capacity_rrd) {
    struct MinHeap_rrd* minHeap_rrd = (struct MinHeap_rrd*)malloc(sizeof(struct MinHeap_rrd));
    minHeap_rrd->pos_rrd = (int*)malloc(capacity_rrd * sizeof(int));
    minHeap_rrd->size_rrd = 0;
    minHeap_rrd->capacity_rrd = capacity_rrd;
    minHeap_rrd->array_rrd = (struct MinHeapNode_rrd**)malloc(capacity_rrd * sizeof(struct MinHeapNode_rrd*));
    return minHeap_rrd;
}

void swapMinHeapNode_rrd(struct MinHeapNode_rrd** a_rrd, struct MinHeapNode_rrd** b_rrd) {
    struct MinHeapNode_rrd* t_rrd = *a_rrd;
    *a_rrd = *b_rrd;
    *b_rrd = t_rrd;
}

void minHeapify_rrd(struct MinHeap_rrd* minHeap_rrd, int index_rrd) {
    int smallest_rrd, left_rrd, right_rrd;
    smallest_rrd = index_rrd;
    left_rrd = 2 * index_rrd + 1;
    right_rrd = 2 * index_rrd + 2;
    if (left_rrd < minHeap_rrd->size_rrd && 
    {
        minHeap_rrd->array_rrd[left_rrd]->distance_rrd < minHeap_rrd->array_rrd[smallest_rrd]->distance_rrd)
{
        smallest_rrd = left_rrd;
    }

    if (right_rrd < minHeap_rrd->size_rrd && 
    {
        minHeap_rrd->array_rrd[right_rrd]->distance_rrd < minHeap_rrd->array_rrd[smallest_rrd]->distance_rrd)
{
        smallest_rrd = right_rrd;
    }

    if (smallest_rrd != index_rrd)
{
        struct MinHeapNode_rrd* smallestNode_rrd = minHeap_rrd->array_rrd[smallest_rrd];
        struct MinHeapNode_rrd* indexNode_rrd = minHeap_rrd->array_rrd[index_rrd];
        minHeap_rrd->pos_rrd[smallestNode_rrd->vertex_rrd] = index_rrd;
        minHeap_rrd->pos_rrd[indexNode_rrd->vertex_rrd] = smallest_rrd;
        swapMinHeapNode_rrd(&minHeap_rrd->array_rrd[smallest_rrd], &minHeap_rrd->array_rrd[index_rrd]);
        minHeapify_rrd(minHeap_rrd, smallest_rrd);
    }
}

int isEmpty_rrd(struct MinHeap_rrd* minHeap_rrd) {
    return minHeap_rrd->size_rrd == 0;
}

struct MinHeapNode_rrd* extractMin_rrd(struct MinHeap_rrd* minHeap_rrd) {
    if (isEmpty_rrd(minHeap_rrd))
{
        return NULL;
    }

    struct MinHeapNode_rrd* root_rrd = minHeap_rrd->array_rrd[0];
    struct MinHeapNode_rrd* lastNode_rrd = minHeap_rrd->array_rrd[minHeap_rrd->size_rrd - 1];
    minHeap_rrd->array_rrd[0] = lastNode_rrd;
    minHeap_rrd->pos_rrd[root_rrd->vertex_rrd] = minHeap_rrd->size_rrd - 1;
    minHeap_rrd->pos_rrd[lastNode_rrd->vertex_rrd] = 0;
    --minHeap_rrd->size_rrd;
    minHeapify_rrd(minHeap_rrd, 0);
    return root_rrd;
}

void decreaseKey_rrd(struct MinHeap_rrd* minHeap_rrd, int vertex_rrd, int distance_rrd) {
    int i_rrd = minHeap_rrd->pos_rrd[vertex_rrd];
    minHeap_rrd->array_rrd[i_rrd]->distance_rrd = distance_rrd;
    while (i_rrd && minHeap_rrd->array_rrd[i_rrd]->distance_rrd < minHeap_rrd->array_rrd[(i_rrd - 1) / 2]->distance_rrd)
{
        minHeap_rrd->pos_rrd[minHeap_rrd->array_rrd[i_rrd]->vertex_rrd] = (i_rrd - 1) / 2;
        minHeap_rrd->pos_rrd[minHeap_rrd->array_rrd[(i_rrd - 1) / 2]->vertex_rrd] = i_rrd;
        swapMinHeapNode_rrd(&minHeap_rrd->array_rrd[i_rrd], &minHeap_rrd->array_rrd[(i_rrd - 1) / 2]);
        i_rrd = (i_rrd - 1) / 2;
    }
}

int isInMinHeap_rrd(struct MinHeap_rrd* minHeap_rrd, int vertex_rrd) {
    if (minHeap_rrd->pos_rrd[vertex_rrd] < minHeap_rrd->size_rrd)
{
        return 1;
    }
    return 0;
}

void printDistance_rrd(int distance_rrd[], int vertices_rrd, int src_rrd) {
    cout << "\nVertex Distance from Source (" << src_rrd << "):" << endl;
    cout << "Vertex\tDistance" << endl;
    for (int i_rrd = 0; i_rrd < vertices_rrd; i_rrd++)
{
        if (distance_rrd[i_rrd] == INT_MAX)
{
            cout << "" << i_rrd << "\tINF" << endl;
        } else
{

            cout << "" << i_rrd, distance_rrd[i_rrd] << "\t%d" << endl;
        }
    }
}

void dijkstra_rrd(struct Graph_rrd* graph_rrd, int src_rrd) {
    int vertices_rrd = graph_rrd->vertices_rrd;
    int* distance_rrd = (int*)malloc(vertices_rrd * sizeof(int));
    struct MinHeap_rrd* minHeap_rrd = createMinHeap_rrd(vertices_rrd);
    for (int v_rrd = 0; v_rrd < vertices_rrd; v_rrd++)
{
        distance_rrd[v_rrd] = INT_MAX;
        minHeap_rrd->array_rrd[v_rrd] = createMinHeapNode_rrd(v_rrd, distance_rrd[v_rrd]);
        minHeap_rrd->pos_rrd[v_rrd] = v_rrd;
    }

    minHeap_rrd->array_rrd[src_rrd] = createMinHeapNode_rrd(src_rrd, 0);
    minHeap_rrd->pos_rrd[src_rrd] = src_rrd;
    distance_rrd[src_rrd] = 0;
    decreaseKey_rrd(minHeap_rrd, src_rrd, 0);
    minHeap_rrd->size_rrd = vertices_rrd;
    while (!isEmpty_rrd(minHeap_rrd))
{
        struct MinHeapNode_rrd* minHeapNode_rrd = extractMin_rrd(minHeap_rrd);
        int u_rrd = minHeapNode_rrd->vertex_rrd;
        struct GraphNode_rrd* temp_rrd = graph_rrd->adjList_rrd[u_rrd];
        while (temp_rrd != NULL)
{
            int v_rrd = temp_rrd->vertex_rrd;
            if (isInMinHeap_rrd(minHeap_rrd, v_rrd) && 
            {
                distance_rrd[u_rrd] != INT_MAX && 
                distance_rrd[u_rrd] + temp_rrd->weight_rrd < distance_rrd[v_rrd])
{
                distance_rrd[v_rrd] = distance_rrd[u_rrd] + temp_rrd->weight_rrd;
                decreaseKey_rrd(minHeap_rrd, v_rrd, distance_rrd[v_rrd]);
            }

            temp_rrd = temp_rrd->next_rrd;
        }
    }

    printDistance_rrd(distance_rrd, vertices_rrd, src_rrd);
    for (int i_rrd = 0; i_rrd < vertices_rrd; i_rrd++)
{
        free(minHeap_rrd->array_rrd[i_rrd]);
    }

    free(minHeap_rrd->array_rrd);
    free(minHeap_rrd->pos_rrd);
    free(minHeap_rrd);
    free(distance_rrd);
}

void printGraph_rrd(struct Graph_rrd* graph_rrd) {
    cout << "\nGraph Representation (Adjacency List):" << endl;
    for (int v_rrd = 0; v_rrd < graph_rrd->vertices_rrd; v_rrd++)
{
        struct GraphNode_rrd* temp_rrd = graph_rrd->adjList_rrd[v_rrd];
        cout << "Vertex " << v_rrd << ": ";
        while (temp_rrd)
{
            cout << "(" << temp_rrd->vertex_rrd, temp_rrd->weight_rrd << ", %d) ";
            temp_rrd = temp_rrd->next_rrd;
        }

        cout << "" << endl;
    }
}

void freeGraph_rrd(struct Graph_rrd* graph_rrd) {
    for (int i_rrd = 0; i_rrd < graph_rrd->vertices_rrd; i_rrd++)
{
        struct GraphNode_rrd* temp_rrd = graph_rrd->adjList_rrd[i_rrd];
        while (temp_rrd)
{
            struct GraphNode_rrd* next_rrd = temp_rrd->next_rrd;
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
    addEdge_rrd(graph_rrd, 4, 5, 6);
    return graph_rrd;
}

void displayMenu_rrd() {
    cout << "\n===== Dijkstra's Algorithm for Shortest Path =====" << endl;
    cout << "1. Add Edge" << endl;
    cout << "2. Print Graph" << endl;
    cout << "3. Find Shortest Paths (Dijkstra's Algorithm)" << endl;
    cout << "4. Create Sample Graph" << endl;
    cout << "5. Exit" << endl;
    cout << "===============================================" << endl;
    cout << "Enter your choice: ";
}

int main() {
    cout << "Welcome to Dijkstra's Algorithm for Shortest Path!" << endl;
    int vertices_rrd;
    cout << "Enter the number of vertices in the graph: ";
    cin >> vertices_rrd;
    if (vertices_rrd <= 0 || vertices_rrd > MAX_VERTICES)
{
        cout << "Invalid number of vertices! Must be between 1 and " << MAX_VERTICES << "." << endl;
        return 1;
    }

    struct Graph_rrd* graph_rrd = createGraph_rrd(vertices_rrd);
    int choice_rrd;
    while (1)
{
        displayMenu_rrd();
        cin >> choice_rrd;
        switch (choice_rrd)
{
{
                int src_rrd, dest_rrd, weight_rrd;
                cout << "Enter source vertex (0-" << vertices_rrd - 1 << "): ";
                cin >> src_rrd;
                cout << "Enter destination vertex (0-" << vertices_rrd - 1 << "): ";
                cin >> dest_rrd;
                cout << "Enter weight of edge: ";
                cin >> weight_rrd;
                if (src_rrd < 0 || src_rrd >= vertices_rrd || dest_rrd < 0 || dest_rrd >= vertices_rrd)
{
                    cout << "Invalid vertex numbers!" << endl;
                } else if (weight_rrd < 0)

{
                    cout << "Edge weight cannot be negative!" << endl;
                } else
{

                    addEdge_rrd(graph_rrd, src_rrd, dest_rrd, weight_rrd);
                    cout << "Directed edge added from " << src_rrd, dest_rrd, weight_rrd << " to %d with weight %d successfully!" << endl;
                }
                break;
            }

{
                printGraph_rrd(graph_rrd);
                break;
            }

{
                int src_rrd;
                cout << "Enter source vertex (0-" << vertices_rrd - 1 << "): ";
                cin >> src_rrd;
                if (src_rrd < 0 || src_rrd >= vertices_rrd)
{
                    cout << "Invalid source vertex!" << endl;
                } else
{

                    dijkstra_rrd(graph_rrd, src_rrd);
                }
                break;
            }

{
                freeGraph_rrd(graph_rrd);
                graph_rrd = createSampleGraph_rrd();
                cout << "Sample graph created successfully!" << endl;
                printGraph_rrd(graph_rrd);
                break;
            }

{
                cout << "Thank you for using Dijkstra's Algorithm for Shortest Path!" << endl;
                freeGraph_rrd(graph_rrd);
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
Welcome to Dijkstra's Algorithm for Shortest Path!
Enter the number of vertices in the graph: 6
===== Dijkstra's Algorithm for Shortest Path =====
1. Add Edge
2. Print Graph
3. Find Shortest Paths (Dijkstra's Algorithm)
4. Create Sample Graph
5. Exit
===============================================
Enter your choice: 4
Sample graph created successfully!
Graph Representation (Adjacency List):
Vertex 0: (2, 3) (1, 4) 
Vertex 1: (3, 2) (2, 1) 
Vertex 2: (3, 4) 
Vertex 3: (4, 2) 
Vertex 4: (5, 6) 
Vertex 5: 
===== Dijkstra's Algorithm for Shortest Path =====
1. Add Edge
2. Print Graph
3. Find Shortest Paths (Dijkstra's Algorithm)
4. Create Sample Graph
5. Exit
===============================================
Enter your choice: 3
Enter source vertex (0-5): 0
Vertex Distance from Source (0):
Vertex	Distance
0	0
1	4
2	3
3	6
4	8
5	14
```

## Dry Run

For a directed graph with 6 vertices and weighted edges:
- (0,1):4, (0,2):3, (1,2):1, (1,3):2, (2,3):4, (3,4):2, (4,5):6

Starting from vertex 0:

1. **Initialization**:
   - Distance: [0, ∞, ∞, ∞, ∞, ∞]
   - MinHeap: [(0,0), (1,∞), (2,∞), (3,∞), (4,∞), (5,∞)]

2. **First Iteration (Extract 0)**:
   - Process vertex 0
   - Update adjacent vertices:
     * Distance to 1: 0+4=4 < ∞ → Update to 4
     * Distance to 2: 0+3=3 < ∞ → Update to 3
   - Distance: [0, 4, 3, ∞, ∞, ∞]
   - MinHeap: [(2,3), (1,4), (3,∞), (4,∞), (5,∞)]

3. **Second Iteration (Extract 2)**:
   - Process vertex 2
   - Update adjacent vertices:
     * Distance to 3: 3+4=7 < ∞ → Update to 7
   - Distance: [0, 4, 3, 7, ∞, ∞]
   - MinHeap: [(1,4), (3,7), (4,∞), (5,∞)]

4. **Third Iteration (Extract 1)**:
   - Process vertex 1
   - Update adjacent vertices:
     * Distance to 2: 4+1=5 > 3 → No update
     * Distance to 3: 4+2=6 < 7 → Update to 6
   - Distance: [0, 4, 3, 6, ∞, ∞]
   - MinHeap: [(3,6), (4,∞), (5,∞)]

5. **Fourth Iteration (Extract 3)**:
   - Process vertex 3
   - Update adjacent vertices:
     * Distance to 4: 6+2=8 < ∞ → Update to 8
   - Distance: [0, 4, 3, 6, 8, ∞]
   - MinHeap: [(4,8), (5,∞)]

6. **Fifth Iteration (Extract 4)**:
   - Process vertex 4
   - Update adjacent vertices:
     * Distance to 5: 8+6=14 < ∞ → Update to 14
   - Distance: [0, 4, 3, 6, 8, 14]
   - MinHeap: [(5,14)]

7. **Sixth Iteration (Extract 5)**:
   - Process vertex 5
   - No adjacent vertices
   - Distance: [0, 4, 3, 6, 8, 14]

Final shortest distances from vertex 0:
- Vertex 0: 0
- Vertex 1: 4
- Vertex 2: 3
- Vertex 3: 6
- Vertex 4: 8
- Vertex 5: 14

## Conclusion

The implementation demonstrates Dijkstra's algorithm for finding shortest paths from a source vertex using adjacency list representation. Key features include:

1. **Adjacency List Representation**: Memory efficient for sparse graphs
2. **Dijkstra's Algorithm**: Greedy approach to find shortest paths
3. **Min Heap Implementation**: Efficient priority queue for vertex selection
4. **Complete Operations**: All required graph operations plus additional utilities

**Time Complexities**:
- Add Edge: O(1) - constant time insertion at head of list
- Dijkstra's Algorithm: O((V + E) log V) where V is vertices and E is edges
- Print Graph: O(V + E) where V is vertices and E is edges

**Space Complexity**: O(V + E) for the adjacency list and O(V) for the min heap

The adjacency list approach is ideal for this application because:
1. **Memory Efficiency**: For sparse graphs, saves space compared to adjacency matrix
2. **Dynamic Size**: Can easily add/remove edges
3. **Easy Traversal**: Simple to iterate through adjacent vertices
4. **Weighted Edges**: Natural support for edge weights

The min heap implementation is crucial for performance:
1. **Efficient Extraction**: O(log V) time to extract minimum distance vertex
2. **Fast Updates**: O(log V) time to update distance values
3. **Priority Management**: Maintains vertices in order of distance

The implementation handles edge cases properly:
- Invalid vertex numbers with appropriate error messages
- Negative weight validation (Dijkstra's requires non-negative weights)
- Memory management to prevent leaks
- Comprehensive user interface with clear feedback

Additional features beyond requirements:
- Graph visualization through adjacency list display
- Sample graph creation for testing
- Interactive menu system
- Complete error handling
- Distance array display

In real-world applications, this system could be extended to:
1. Support undirected graphs
2. Implement other shortest path algorithms (Bellman-Ford for negative weights)
3. Add path reconstruction to show actual paths
4. Add graphical visualization
5. Support dynamic graph resizing

Shortest path algorithms are used in:
1. **GPS Navigation**: Finding shortest routes between locations
2. **Network Routing**: Determining optimal paths in computer networks
3. **Game Development**: Pathfinding for AI characters
4. **Social Networks**: Finding degrees of separation between users
5. **Supply Chain**: Optimizing delivery routes

This implementation provides a solid foundation for understanding graph algorithms and shortest path problems, which are essential in computer science and network optimization. Dijkstra's algorithm is particularly useful for graphs with non-negative edge weights.
