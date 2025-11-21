# Unit V Assignment 5: Graph Representation with BFS and DFS Traversals using Adjacency List

Implementation to accept a graph from a user, represent it with an adjacency list, and perform BFS and DFS traversals.

## Problem Statement

Write a Program to accept a graph from a user and represent it with Adjacency List and perform BFS and DFS traversals on it.

## Pseudo Code

### Graph Structure
```
Structure GraphNode:
    vertex: integer
    next: pointer to GraphNode
Structure Graph:
    vertices: integer
    adjList: array of pointers to GraphNode of size vertices
```

### Add Edge
```
Algorithm AddEdge(graph, src, dest):
    Create new node with dest
    new node.next = graph.adjList[src]
    graph.adjList[src] = new node
    Create new node with src
    new node.next = graph.adjList[dest]
    graph.adjList[dest] = new node
```

### BFS Traversal
```
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
```

### DFS Traversal
```
Algorithm DFSTraversal(graph, startVertex):
    Initialize visited array of size vertices with all false
    Call DFSUtil(graph, startVertex, visited)
Algorithm DFSUtil(graph, vertex, visited):
    Mark vertex as visited
    Print vertex
    For each adjacent vertex of vertex:
        If not visited:
            Call DFSUtil(graph, adjacent vertex, visited)
```

## Code Implementation

```c
#include <iostream>
using namespace std;
#include <stdlib.h>
#define MAX_VERTICES 100
struct GraphNode_rrd {
    int vertex_rrd;
    struct GraphNode_rrd* next_rrd;
};

struct Graph_rrd {
    int vertices_rrd;
    struct GraphNode_rrd* adjList_rrd[MAX_VERTICES];
};

struct Queue_rrd {
    int items_rrd[MAX_VERTICES];
    int front_rrd;
    int rear_rrd;
    int size_rrd;
};

struct GraphNode_rrd* createGraphNode_rrd(int vertex_rrd);
struct Graph_rrd* createGraph_rrd(int vertices_rrd);
void addEdge_rrd(struct Graph_rrd* graph_rrd, int src_rrd, int dest_rrd);
struct Queue_rrd* createQueue_rrd();
int isQueueEmpty_rrd(struct Queue_rrd* queue_rrd);
void enqueue_rrd(struct Queue_rrd* queue_rrd, int item_rrd);
int dequeue_rrd(struct Queue_rrd* queue_rrd);
void bfsTraversal_rrd(struct Graph_rrd* graph_rrd, int startVertex_rrd);
void dfsUtil_rrd(struct Graph_rrd* graph_rrd, int vertex_rrd, int visited_rrd[]);
void dfsTraversal_rrd(struct Graph_rrd* graph_rrd, int startVertex_rrd);
void printGraph_rrd(struct Graph_rrd* graph_rrd);
void freeGraph_rrd(struct Graph_rrd* graph_rrd);
struct Graph_rrd* createSampleGraph_rrd();
void displayMenu_rrd();
struct GraphNode_rrd* createGraphNode_rrd(int vertex_rrd) {
    struct GraphNode_rrd* newNode_rrd = (struct GraphNode_rrd*)malloc(sizeof(struct GraphNode_rrd));
    newNode_rrd->vertex_rrd = vertex_rrd;
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

void addEdge_rrd(struct Graph_rrd* graph_rrd, int src_rrd, int dest_rrd) {
    struct GraphNode_rrd* newNode_rrd = createGraphNode_rrd(dest_rrd);
    newNode_rrd->next_rrd = graph_rrd->adjList_rrd[src_rrd];
    graph_rrd->adjList_rrd[src_rrd] = newNode_rrd;
    newNode_rrd = createGraphNode_rrd(src_rrd);
    newNode_rrd->next_rrd = graph_rrd->adjList_rrd[dest_rrd];
    graph_rrd->adjList_rrd[dest_rrd] = newNode_rrd;
}

struct Queue_rrd* createQueue_rrd() {
    struct Queue_rrd* queue_rrd = (struct Queue_rrd*)malloc(sizeof(struct Queue_rrd));
    queue_rrd->front_rrd = 0;
    queue_rrd->rear_rrd = -1;
    queue_rrd->size_rrd = 0;
    return queue_rrd;
}

int isQueueEmpty_rrd(struct Queue_rrd* queue_rrd) {
    return queue_rrd->size_rrd == 0;
}

void enqueue_rrd(struct Queue_rrd* queue_rrd, int item_rrd) {
    queue_rrd->rear_rrd = (queue_rrd->rear_rrd + 1) % MAX_VERTICES;
    queue_rrd->items_rrd[queue_rrd->rear_rrd] = item_rrd;
    queue_rrd->size_rrd++;
}

int dequeue_rrd(struct Queue_rrd* queue_rrd) {
    int item_rrd = queue_rrd->items_rrd[queue_rrd->front_rrd];
    queue_rrd->front_rrd = (queue_rrd->front_rrd + 1) % MAX_VERTICES;
    queue_rrd->size_rrd--;
    return item_rrd;
}

void bfsTraversal_rrd(struct Graph_rrd* graph_rrd, int startVertex_rrd) {
    int visited_rrd[MAX_VERTICES] = {0};
    struct Queue_rrd* queue_rrd = createQueue_rrd();
    visited_rrd[startVertex_rrd] = 1;
    enqueue_rrd(queue_rrd, startVertex_rrd);
    cout << "BFS Traversal starting from vertex " << startVertex_rrd << ": ";
    while (!isQueueEmpty_rrd(queue_rrd))
{
        int currentVertex_rrd = dequeue_rrd(queue_rrd);
        cout << "" << currentVertex_rrd << " ";
        struct GraphNode_rrd* temp_rrd = graph_rrd->adjList_rrd[currentVertex_rrd];
        while (temp_rrd)
{
            int adjVertex_rrd = temp_rrd->vertex_rrd;
            if (!visited_rrd[adjVertex_rrd])
{
                visited_rrd[adjVertex_rrd] = 1;
                enqueue_rrd(queue_rrd, adjVertex_rrd);
            }

            temp_rrd = temp_rrd->next_rrd;
        }
    }

    cout << "" << endl;
    free(queue_rrd);
}

void dfsUtil_rrd(struct Graph_rrd* graph_rrd, int vertex_rrd, int visited_rrd[]) {
    visited_rrd[vertex_rrd] = 1;
    cout << "" << vertex_rrd << " ";
    struct GraphNode_rrd* temp_rrd = graph_rrd->adjList_rrd[vertex_rrd];
    while (temp_rrd)
{
        int adjVertex_rrd = temp_rrd->vertex_rrd;
        if (!visited_rrd[adjVertex_rrd])
{
            dfsUtil_rrd(graph_rrd, adjVertex_rrd, visited_rrd);
        }

        temp_rrd = temp_rrd->next_rrd;
    }
}

void dfsTraversal_rrd(struct Graph_rrd* graph_rrd, int startVertex_rrd) {
    int visited_rrd[MAX_VERTICES] = {0};
    cout << "DFS Traversal starting from vertex " << startVertex_rrd << ": ";
    dfsUtil_rrd(graph_rrd, startVertex_rrd, visited_rrd);
    cout << "" << endl;
}

void printGraph_rrd(struct Graph_rrd* graph_rrd) {
    cout << "\nGraph Representation (Adjacency List):" << endl;
    for (int v_rrd = 0; v_rrd < graph_rrd->vertices_rrd; v_rrd++)
{
        struct GraphNode_rrd* temp_rrd = graph_rrd->adjList_rrd[v_rrd];
        cout << "Vertex " << v_rrd << ": ";
        while (temp_rrd)
{
            cout << "" << temp_rrd->vertex_rrd << " ";
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
    addEdge_rrd(graph_rrd, 0, 1);
    addEdge_rrd(graph_rrd, 0, 2);
    addEdge_rrd(graph_rrd, 1, 3);
    addEdge_rrd(graph_rrd, 1, 4);
    addEdge_rrd(graph_rrd, 2, 5);
    return graph_rrd;
}

void displayMenu_rrd() {
    cout << "\n===== Graph Operations using Adjacency List =====" << endl;
    cout << "1. Add Edge" << endl;
    cout << "2. Print Graph" << endl;
    cout << "3. BFS Traversal" << endl;
    cout << "4. DFS Traversal" << endl;
    cout << "5. Create Sample Graph" << endl;
    cout << "6. Exit" << endl;
    cout << "===============================================" << endl;
    cout << "Enter your choice: ";
}

int main() {
    cout << "Welcome to Graph Representation using Adjacency List!" << endl;
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
                int src_rrd, dest_rrd;
                cout << "Enter source vertex (0-" << vertices_rrd - 1 << "): ";
                cin >> src_rrd;
                cout << "Enter destination vertex (0-" << vertices_rrd - 1 << "): ";
                cin >> dest_rrd;
                if (src_rrd < 0 || src_rrd >= vertices_rrd || dest_rrd < 0 || dest_rrd >= vertices_rrd)
{
                    cout << "Invalid vertex numbers!" << endl;
                } else
{

                    addEdge_rrd(graph_rrd, src_rrd, dest_rrd);
                    cout << "Edge added between " << src_rrd, dest_rrd << " and %d successfully!" << endl;
                }
                break;
            }

{
                printGraph_rrd(graph_rrd);
                break;
            }

{
                int startVertex_rrd;
                cout << "Enter starting vertex for BFS (0-" << vertices_rrd - 1 << "): ";
                cin >> startVertex_rrd;
                if (startVertex_rrd < 0 || startVertex_rrd >= vertices_rrd)
{
                    cout << "Invalid vertex number!" << endl;
                } else
{

                    bfsTraversal_rrd(graph_rrd, startVertex_rrd);
                }
                break;
            }

{
                int startVertex_rrd;
                cout << "Enter starting vertex for DFS (0-" << vertices_rrd - 1 << "): ";
                cin >> startVertex_rrd;
                if (startVertex_rrd < 0 || startVertex_rrd >= vertices_rrd)
{
                    cout << "Invalid vertex number!" << endl;
                } else
{

                    dfsTraversal_rrd(graph_rrd, startVertex_rrd);
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
                cout << "Thank you for using Graph Representation using Adjacency List!" << endl;
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
Welcome to Graph Representation using Adjacency List!
Enter the number of vertices in the graph: 6
===== Graph Operations using Adjacency List =====
1. Add Edge
2. Print Graph
3. BFS Traversal
4. DFS Traversal
5. Create Sample Graph
6. Exit
===============================================
Enter your choice: 5
Sample graph created successfully!
Graph Representation (Adjacency List):
Vertex 0: 2 1 
Vertex 1: 4 3 0 
Vertex 2: 5 0 
Vertex 3: 1 
Vertex 4: 1 
Vertex 5: 2 
===== Graph Operations using Adjacency List =====
1. Add Edge
2. Print Graph
3. BFS Traversal
4. DFS Traversal
5. Create Sample Graph
6. Exit
===============================================
Enter your choice: 3
Enter starting vertex for BFS (0-5): 0
BFS Traversal starting from vertex 0: 0 2 1 5 4 3
===== Graph Operations using Adjacency List =====
1. Add Edge
2. Print Graph
3. BFS Traversal
4. DFS Traversal
5. Create Sample Graph
6. Exit
===============================================
Enter your choice: 4
Enter starting vertex for DFS (0-5): 0
DFS Traversal starting from vertex 0: 0 2 5 1 4 3
```

## Dry Run

For a graph with 6 vertices and edges: (0,1), (0,2), (1,3), (1,4), (2,5)

1. **Adjacency List Representation**:
   ```
   Vertex 0: 2 1 
   Vertex 1: 4 3 0 
   Vertex 2: 5 0 
   Vertex 3: 1 
   Vertex 4: 1 
   Vertex 5: 2 
   ```

2. **BFS Traversal starting from vertex 0**:
   - Enqueue 0, mark as visited: Queue=[0], Visited=[1,0,0,0,0,0]
   - Dequeue 0, print 0: Queue=[], Visited=[1,0,0,0,0,0], Output="0"
   - Enqueue adjacent unvisited vertices (2,1): Queue=[2,1], Visited=[1,1,1,0,0,0]
   - Dequeue 2, print 2: Queue=[1], Visited=[1,1,1,0,0,0], Output="0 2"
   - Enqueue adjacent unvisited vertex (5): Queue=[1,5], Visited=[1,1,1,0,0,1]
   - Dequeue 1, print 1: Queue=[5], Visited=[1,1,1,0,0,1], Output="0 2 1"
   - Enqueue adjacent unvisited vertices (4,3): Queue=[5,4,3], Visited=[1,1,1,1,1,1]
   - Dequeue 5, print 5: Queue=[4,3], Visited=[1,1,1,1,1,1], Output="0 2 1 5"
   - Dequeue 4, print 4: Queue=[3], Visited=[1,1,1,1,1,1], Output="0 2 1 5 4"
   - Dequeue 3, print 3: Queue=[], Visited=[1,1,1,1,1,1], Output="0 2 1 5 4 3"

3. **DFS Traversal starting from vertex 0**:
   - Visit 0, mark as visited: Visited=[1,0,0,0,0,0], Output="0"
   - Visit adjacent unvisited vertex 2: Visited=[1,0,1,0,0,0], Output="0 2"
   - Visit adjacent unvisited vertex 5: Visited=[1,0,1,0,0,1], Output="0 2 5"
   - No unvisited adjacent vertices of 5, backtrack to 2, then to 0
   - Visit adjacent unvisited vertex 1: Visited=[1,1,1,0,0,1], Output="0 2 5 1"
   - Visit adjacent unvisited vertex 4: Visited=[1,1,1,0,1,1], Output="0 2 5 1 4"
   - No unvisited adjacent vertices of 4, backtrack to 1
   - Visit adjacent unvisited vertex 3: Visited=[1,1,1,1,1,1], Output="0 2 5 1 4 3"
   - No unvisited adjacent vertices, traversal complete

## Conclusion

The implementation demonstrates graph representation using adjacency list and traversal algorithms. Key features include:

1. **Adjacency List Representation**: Memory efficient for sparse graphs
2. **BFS Traversal**: Level-by-level exploration using queue data structure
3. **DFS Traversal**: Depth-first exploration using recursion
4. **Complete Operations**: All required graph operations plus additional utilities

**Time Complexities**:
- Add Edge: O(1) - constant time insertion at head of list
- BFS Traversal: O(V + E) where V is vertices and E is edges
- DFS Traversal: O(V + E) where V is vertices and E is edges
- Print Graph: O(V + E) where V is vertices and E is edges

**Space Complexity**: O(V + E) for the adjacency list

The adjacency list approach is ideal for this application because:
1. **Memory Efficiency**: For sparse graphs, saves space compared to adjacency matrix
2. **Dynamic Size**: Can easily add/remove edges
3. **Easy Traversal**: Simple to iterate through adjacent vertices
4. **Scalability**: Efficient for large graphs with few edges

The implementation handles edge cases properly:
- Invalid vertex numbers with appropriate error messages
- Memory management to prevent leaks
- Comprehensive user interface with clear feedback

Additional features beyond requirements:
- Graph visualization through adjacency list display
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

This implementation provides a solid foundation for understanding graph representation and traversal algorithms, which are essential in computer science and software engineering. The adjacency list representation is particularly useful for sparse graphs where the number of edges is much less than the square of the number of vertices.
