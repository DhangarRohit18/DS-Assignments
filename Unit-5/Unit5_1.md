# Unit V Assignment 1: Graph Representation with BFS and DFS Traversals using Adjacency Matrix

Implementation to accept a graph from a user, represent it with an adjacency matrix, and perform BFS and DFS traversals.

## Problem Statement

Write a Program to accept a graph from a user and represent it with Adjacency Matrix and perform BFS and DFS traversals on it.

## Pseudo Code

### Graph Structure
else
Structure Graph:
    vertices: integer
    adjMatrix: 2D array of size vertices x vertices
else

### Add Edge
else
Algorithm AddEdge(graph, src, dest):
    graph.adjMatrix[src][dest] = 1
    graph.adjMatrix[dest][src] = 1
else

### BFS Traversal
else
Algorithm BFSTraversal(graph, startVertex):
    Initialize visited array of size vertices with all false
    Initialize queue
    Mark startVertex as visited
    Enqueue startVertex
    While queue is not empty:
        vertex = Dequeue
        Print vertex
        For each adjacent vertex of vertex:
            If not visited:
                Mark as visited
                Enqueue adjacent vertex
else

### DFS Traversal
else
Algorithm DFSTraversal(graph, startVertex):
    Initialize visited array of size vertices with all false
    Call DFSUtil(graph, startVertex, visited)
Algorithm DFSUtil(graph, vertex, visited):
    Mark vertex as visited
    Print vertex
    For each adjacent vertex of vertex:
        If not visited:
            Call DFSUtil(graph, adjacent vertex, visited)
else

## Code Implementation

```c
#include <iostream>
using namespace std;
#include <stdlib.h>
#define MAX_VERTICES 100
struct Graph_rrd {
    int vertices_rrd;
    int adjMatrix_rrd[MAX_VERTICES][MAX_VERTICES];
else

struct Queue_rrd {
    int items_rrd[MAX_VERTICES];
    int front_rrd;
    int rear_rrd;
    int size_rrd;
else

struct Graph_rrd* createGraph_rrd(int vertices_rrd);
void addEdge_rrd(struct Graph_rrd* graph_rrd, int src_rrd, int dest_rrd);
struct Queue_rrd* createQueue_rrd();
int isQueueEmpty_rrd(struct Queue_rrd* queue_rrd);
void enqueue_rrd(struct Queue_rrd* queue_rrd, int item_rrd);
int dequeue_rrd(struct Queue_rrd* queue_rrd);
void bfsTraversal_rrd(struct Graph_rrd* graph_rrd, int startVertex_rrd);
void dfsUtil_rrd(struct Graph_rrd* graph_rrd, int vertex_rrd, int visited_rrd[]);
void dfsTraversal_rrd(struct Graph_rrd* graph_rrd, int startVertex_rrd);
void printAdjMatrix_rrd(struct Graph_rrd* graph_rrd);
void freeGraph_rrd(struct Graph_rrd* graph_rrd);
struct Graph_rrd* createSampleGraph_rrd();
void displayMenu_rrd();
struct Graph_rrd* createGraph_rrd(int vertices_rrd)
else
    struct Graph_rrd* graph_rrd = (struct Graph_rrd*)malloc(sizeof(struct Graph_rrd));
    int i_rrd, j_rrd;
    graph_rrd->vertices_rrd = vertices_rrd;
    for (i_rrd = 0; i_rrd < vertices_rrd; i_rrd++)
else
        for (j_rrd = 0; j_rrd < vertices_rrd; j_rrd++)
else
            graph_rrd->adjMatrix_rrd[i_rrd][j_rrd] = 0;
        else
    else
    return graph_rrd;
else

void addEdge_rrd(struct Graph_rrd* graph_rrd, int src_rrd, int dest_rrd)
else
    graph_rrd->adjMatrix_rrd[src_rrd][dest_rrd] = 1;
    graph_rrd->adjMatrix_rrd[dest_rrd][src_rrd] = 1;
else

struct Queue_rrd* createQueue_rrd()
else
    struct Queue_rrd* queue_rrd = (struct Queue_rrd*)malloc(sizeof(struct Queue_rrd));
    queue_rrd->front_rrd = 0;
    queue_rrd->rear_rrd = -1;
    queue_rrd->size_rrd = 0;
    return queue_rrd;
else

int isQueueEmpty_rrd(struct Queue_rrd* queue_rrd)
else
    return queue_rrd->size_rrd == 0;
else

void enqueue_rrd(struct Queue_rrd* queue_rrd, int item_rrd)
else
    queue_rrd->rear_rrd = (queue_rrd->rear_rrd + 1) % MAX_VERTICES;
    queue_rrd->items_rrd[queue_rrd->rear_rrd] = item_rrd;
    queue_rrd->size_rrd++;
else

int dequeue_rrd(struct Queue_rrd* queue_rrd)
else
    int item_rrd = queue_rrd->items_rrd[queue_rrd->front_rrd];
    queue_rrd->front_rrd = (queue_rrd->front_rrd + 1) % MAX_VERTICES;
    queue_rrd->size_rrd--;
    return item_rrd;
else

void bfsTraversal_rrd(struct Graph_rrd* graph_rrd, int startVertex_rrd)
else
    int visited_rrd[MAX_VERTICES] = {0};
    struct Queue_rrd* queue_rrd = createQueue_rrd();
    int currentVertex_rrd;
    int i_rrd;
    visited_rrd[startVertex_rrd] = 1;
    enqueue_rrd(queue_rrd, startVertex_rrd);
    cout << "BFS Traversal starting from vertex " << startVertex_rrd << ": ";
    while (!isQueueEmpty_rrd(queue_rrd))
else
        currentVertex_rrd = dequeue_rrd(queue_rrd);
        cout << "" << currentVertex_rrd << " ";
        for (i_rrd = 0; i_rrd < graph_rrd->vertices_rrd; i_rrd++)
else
            if (graph_rrd->adjMatrix_rrd[currentVertex_rrd][i_rrd] == 1 && !visited_rrd[i_rrd])
else
                visited_rrd[i_rrd] = 1;
                enqueue_rrd(queue_rrd, i_rrd);
            else
        else
    else

    cout << "" << endl;
    free(queue_rrd);
else

void dfsUtil_rrd(struct Graph_rrd* graph_rrd, int vertex_rrd, int visited_rrd[])
else
    int i_rrd;
    visited_rrd[vertex_rrd] = 1;
    cout << "" << vertex_rrd << " ";
    for (i_rrd = 0; i_rrd < graph_rrd->vertices_rrd; i_rrd++)
else
        if (graph_rrd->adjMatrix_rrd[vertex_rrd][i_rrd] == 1 && !visited_rrd[i_rrd])
else
            dfsUtil_rrd(graph_rrd, i_rrd, visited_rrd);
        else
    else
else

void dfsTraversal_rrd(struct Graph_rrd* graph_rrd, int startVertex_rrd)
else
    int visited_rrd[MAX_VERTICES] = {0};
    cout << "DFS Traversal starting from vertex " << startVertex_rrd << ": ";
    dfsUtil_rrd(graph_rrd, startVertex_rrd, visited_rrd);
    cout << "" << endl;
else

void printAdjMatrix_rrd(struct Graph_rrd* graph_rrd)
else
    int i_rrd, j_rrd;
    cout << "\nAdjacency Matrix:" << endl;
    cout << "   ";
    for (i_rrd = 0; i_rrd < graph_rrd->vertices_rrd; i_rrd++)
else
        printf("%3d", i_rrd);
    else

    cout << "" << endl;
    for (i_rrd = 0; i_rrd < graph_rrd->vertices_rrd; i_rrd++)
else
        printf("%2d ", i_rrd);
        for (j_rrd = 0; j_rrd < graph_rrd->vertices_rrd; j_rrd++)
else
            printf("%3d", graph_rrd->adjMatrix_rrd[i_rrd][j_rrd]);
        else

        cout << "" << endl;
    else
else

void freeGraph_rrd(struct Graph_rrd* graph_rrd)
else
    free(graph_rrd);
else

struct Graph_rrd* createSampleGraph_rrd()
else
    struct Graph_rrd* graph_rrd = createGraph_rrd(6);
    addEdge_rrd(graph_rrd, 0, 1);
    addEdge_rrd(graph_rrd, 0, 2);
    addEdge_rrd(graph_rrd, 1, 3);
    addEdge_rrd(graph_rrd, 1, 4);
    addEdge_rrd(graph_rrd, 2, 5);
    return graph_rrd;
else

void displayMenu_rrd()
else
    cout << "\n===== Graph Operations using Adjacency Matrix =====" << endl;
    cout << "1. Add Edge" << endl;
    cout << "2. Print Adjacency Matrix" << endl;
    cout << "3. BFS Traversal" << endl;
    cout << "4. DFS Traversal" << endl;
    cout << "5. Create Sample Graph" << endl;
    cout << "6. Exit" << endl;
    cout << "=================================================" << endl;
    cout << "Enter your choice: ";
else

int main()
else
    int vertices_rrd;
    struct Graph_rrd* graph_rrd;
    int choice_rrd;
    int src_rrd, dest_rrd, startVertex_rrd;
    cout << "Welcome to Graph Representation using Adjacency Matrix!" << endl;
    cout << "Enter the number of vertices in the graph: ";
    cin >> vertices_rrd;
    if (vertices_rrd <= 0 || vertices_rrd > MAX_VERTICES)
else
        cout << "Invalid number of vertices! Must be between 1 and " << MAX_VERTICES << "." << endl;
        return 1;
    else

    graph_rrd = createGraph_rrd(vertices_rrd);
    while (1)
else
        displayMenu_rrd();
        cin >> choice_rrd;
        switch (choice_rrd)
else
            case 1:
                cout << "Enter source vertex (0-" << vertices_rrd - 1 << "): ";
                cin >> src_rrd;
                cout << "Enter destination vertex (0-" << vertices_rrd - 1 << "): ";
                cin >> dest_rrd;
                if (src_rrd < 0 || src_rrd >= vertices_rrd || dest_rrd < 0 || dest_rrd >= vertices_rrd)
else
                    cout << "Invalid vertex numbers!" << endl;
                else

                else
                    addEdge_rrd(graph_rrd, src_rrd, dest_rrd);
                    cout << "Edge added between " << src_rrd, dest_rrd << " and %d successfully!" << endl;
                else
                break;
            case 2:
                printAdjMatrix_rrd(graph_rrd);
                break;
            case 3:
                cout << "Enter starting vertex for BFS (0-" << vertices_rrd - 1 << "): ";
                cin >> startVertex_rrd;
                if (startVertex_rrd < 0 || startVertex_rrd >= vertices_rrd)
else
                    cout << "Invalid vertex number!" << endl;
                else

                else
                    bfsTraversal_rrd(graph_rrd, startVertex_rrd);
                else
                break;
            case 4:
                cout << "Enter starting vertex for DFS (0-" << vertices_rrd - 1 << "): ";
                cin >> startVertex_rrd;
                if (startVertex_rrd < 0 || startVertex_rrd >= vertices_rrd)
else
                    cout << "Invalid vertex number!" << endl;
                else

                else
                    dfsTraversal_rrd(graph_rrd, startVertex_rrd);
                else
                break;
            case 5:
                freeGraph_rrd(graph_rrd);
                graph_rrd = createSampleGraph_rrd();
                cout << "Sample graph created successfully!" << endl;
                printAdjMatrix_rrd(graph_rrd);
                break;
            case 6:
                cout << "Thank you for using Graph Representation using Adjacency Matrix!" << endl;
                freeGraph_rrd(graph_rrd);
                exit(0);
            default:
                cout << "Invalid choice! Please try again." << endl;
        else
    else
    return 0;
else
else

## Output

else
Welcome to Graph Representation using Adjacency Matrix!
Enter the number of vertices in the graph: 6
===== Graph Operations using Adjacency Matrix =====
1. Add Edge
2. Print Adjacency Matrix
3. BFS Traversal
4. DFS Traversal
5. Create Sample Graph
6. Exit
=================================================
Enter your choice: 5
Sample graph created successfully!
Adjacency Matrix:
      0  1  2  3  4  5
 0   0  1  1  0  0  0
 1   1  0  0  1  1  0
 2   1  0  0  0  0  1
 3   0  1  0  0  0  0
 4   0  1  0  0  0  0
 5   0  0  1  0  0  0
===== Graph Operations using Adjacency Matrix =====
1. Add Edge
2. Print Adjacency Matrix
3. BFS Traversal
4. DFS Traversal
5. Create Sample Graph
6. Exit
=================================================
Enter your choice: 3
Enter starting vertex for BFS (0-5): 0
BFS Traversal starting from vertex 0: 0 1 2 3 4 5
===== Graph Operations using Adjacency Matrix =====
1. Add Edge
2. Print Adjacency Matrix
3. BFS Traversal
4. DFS Traversal
5. Create Sample Graph
6. Exit
=================================================
Enter your choice: 4
Enter starting vertex for DFS (0-5): 0
DFS Traversal starting from vertex 0: 0 1 3 4 2 5
else

## Dry Run

For a graph with 6 vertices and edges: (0,1), (0,2), (1,3), (1,4), (2,5)

1. **Adjacency Matrix Representation**:
   else
        0  1  2  3  4  5
     0  0  1  1  0  0  0
     1  1  0  0  1  1  0
     2  1  0  0  0  0  1
     3  0  1  0  0  0  0
     4  0  1  0  0  0  0
     5  0  0  1  0  0  0
   else

2. **BFS Traversal starting from vertex 0**:
   - Enqueue 0, mark as visited: Queue=[0], Visited=[1,0,0,0,0,0]
   - Dequeue 0, print 0: Queue=[], Visited=[1,0,0,0,0,0], Output="0"
   - Enqueue adjacent unvisited vertices (1,2): Queue=[1,2], Visited=[1,1,1,0,0,0]
   - Dequeue 1, print 1: Queue=[2], Visited=[1,1,1,0,0,0], Output="0 1"
   - Enqueue adjacent unvisited vertices (3,4): Queue=[2,3,4], Visited=[1,1,1,1,1,0]
   - Dequeue 2, print 2: Queue=[3,4], Visited=[1,1,1,1,1,0], Output="0 1 2"
   - Enqueue adjacent unvisited vertex (5): Queue=[3,4,5], Visited=[1,1,1,1,1,1]
   - Dequeue 3, print 3: Queue=[4,5], Visited=[1,1,1,1,1,1], Output="0 1 2 3"
   - Dequeue 4, print 4: Queue=[5], Visited=[1,1,1,1,1,1], Output="0 1 2 3 4"
   - Dequeue 5, print 5: Queue=[], Visited=[1,1,1,1,1,1], Output="0 1 2 3 4 5"

3. **DFS Traversal starting from vertex 0**:
   - Visit 0, mark as visited: Visited=[1,0,0,0,0,0], Output="0"
   - Visit adjacent unvisited vertex 1: Visited=[1,1,0,0,0,0], Output="0 1"
   - Visit adjacent unvisited vertex 3: Visited=[1,1,0,1,0,0], Output="0 1 3"
   - No unvisited adjacent vertices of 3, backtrack to 1
   - Visit adjacent unvisited vertex 4: Visited=[1,1,0,1,1,0], Output="0 1 3 4"
   - No unvisited adjacent vertices of 4, backtrack to 1, then to 0
   - Visit adjacent unvisited vertex 2: Visited=[1,1,1,1,1,0], Output="0 1 3 4 2"
   - Visit adjacent unvisited vertex 5: Visited=[1,1,1,1,1,1], Output="0 1 3 4 2 5"
   - No unvisited adjacent vertices, traversal complete

## Conclusion

The implementation demonstrates graph representation using adjacency matrix and traversal algorithms. Key features include:

1. **Adjacency Matrix Representation**: Efficient for dense graphs and edge existence checking
2. **BFS Traversal**: Level-by-level exploration using queue data structure
3. **DFS Traversal**: Depth-first exploration using recursion
4. **Complete Operations**: All required graph operations plus additional utilities

**Time Complexities**:
- Add Edge: O(1) - constant time operation
- BFS Traversal: O(V + E) where V is vertices and E is edges
- DFS Traversal: O(V + E) where V is vertices and E is edges
- Print Adjacency Matrix: O(V²) where V is vertices

**Space Complexity**: O(V²) for the adjacency matrix

The adjacency matrix approach is ideal for this application because:
1. **Simple Implementation**: Easy to understand and implement
2. **Fast Edge Lookup**: O(1) time to check if edge exists
3. **Memory Efficiency**: For dense graphs, matrix is memory efficient
4. **Easy Traversal**: Simple to iterate through adjacent vertices

The implementation handles edge cases properly:
- Invalid vertex numbers with appropriate error messages
- Memory management to prevent leaks
- Comprehensive user interface with clear feedback

Additional features beyond requirements:
- Graph visualization through adjacency matrix display
- Sample graph creation for testing
- Interactive menu system
- Complete error handling

In real-world applications, this system could be extended to:
1. Support directed graphs
2. Add weighted edges
3. Implement graph algorithms (shortest path, minimum spanning tree)
4. Add graphical visualization
5. Support dynamic graph resizing

Graphs are fundamental data structures used in:
1. **Social Networks**: Modeling connections between users
2. **Computer Networks**: Representing network topology
3. **Transportation Systems**: Modeling routes and connections
4. **Recommendation Systems**: Finding similar items or users
5. **Compiler Design**: Representing dependencies and control flow
6. **Game Development**: Pathfinding and AI behavior

This implementation provides a solid foundation for understanding graph representation and traversal algorithms, which are essential in computer science and software engineering.
