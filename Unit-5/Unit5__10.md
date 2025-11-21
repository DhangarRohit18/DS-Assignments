# Unit V Assignment 10: Dijkstra's Algorithm for Shortest Path using Adjacency List

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

### Min Heap Structure (for optimization)
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

### Dijkstra's Algorithm (Simple Implementation)
```
Algorithm Dijkstra(graph, src):
    Initialize dist array of size vertices with all INFINITY
    Initialize visited array of size vertices with all false
    dist[src] = 0
    For count = 0 to vertices-1:
        u = vertex with minimum distance value among unvisited vertices
        visited[u] = true
        For each adjacent vertex v of u:
            If visited[v] is false AND dist[u] + weight(u,v) < dist[v]:
                dist[v] = dist[u] + weight(u,v)
    Return dist array
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
int findMinDistance_rrd(int dist_rrd[], int visited_rrd[], int vertices_rrd);
void dijkstra_rrd(struct Graph_rrd* graph_rrd, int src_rrd, int dist_rrd[]);
void printShortestPaths_rrd(struct Graph_rrd* graph_rrd, int src_rrd);
void printPath_rrd(struct Graph_rrd* graph_rrd, int src_rrd, int dest_rrd);
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
    

    /*
    newNode_rrd = createGraphNode_rrd(src_rrd, weight_rrd);
    newNode_rrd->next_rrd = graph_rrd->adjList_rrd[dest_rrd];
    graph_rrd->adjList_rrd[dest_rrd] = newNode_rrd;
    */
}

int findMinDistance_rrd(int dist_rrd[], int visited_rrd[], int vertices_rrd) {
    int min_rrd = INT_MAX, minIndex_rrd = -1;
    int v_rrd;
    
    for (v_rrd = 0; v_rrd < vertices_rrd; v_rrd++) {
        if (visited_rrd[v_rrd] == 0 && dist_rrd[v_rrd] <= min_rrd) {
            min_rrd = dist_rrd[v_rrd];
            minIndex_rrd = v_rrd;
        }
    }
    
    return minIndex_rrd;
}

void dijkstra_rrd(struct Graph_rrd* graph_rrd, int src_rrd, int dist_rrd[]) {
    int visited_rrd[MAX_VERTICES];
    int i_rrd, count_rrd, u_rrd, v_rrd;
    struct GraphNode_rrd* temp_rrd;
    

    for (i_rrd = 0; i_rrd < graph_rrd->vertices_rrd; i_rrd++) {
        dist_rrd[i_rrd] = INT_MAX;
        visited_rrd[i_rrd] = 0;
    }
    

    dist_rrd[src_rrd] = 0;
    

    for (count_rrd = 0; count_rrd < graph_rrd->vertices_rrd - 1; count_rrd++) {

        u_rrd = findMinDistance_rrd(dist_rrd, visited_rrd, graph_rrd->vertices_rrd);
        

        visited_rrd[u_rrd] = 1;
        

        temp_rrd = graph_rrd->adjList_rrd[u_rrd];
        while (temp_rrd != NULL) {
            v_rrd = temp_rrd->vertex_rrd;
            



            if (!visited_rrd[v_rrd] && dist_rrd[u_rrd] != INT_MAX && 
                dist_rrd[u_rrd] + temp_rrd->weight_rrd < dist_rrd[v_rrd]) {
                dist_rrd[v_rrd] = dist_rrd[u_rrd] + temp_rrd->weight_rrd;
            }
            temp_rrd = temp_rrd->next_rrd;
        }
    }
}

void printShortestPaths_rrd(struct Graph_rrd* graph_rrd, int src_rrd) {
    int dist_rrd[MAX_VERTICES];
    int i_rrd;
    
    dijkstra_rrd(graph_rrd, src_rrd, dist_rrd);
    
    cout << "\nShortest distances from vertex " << src_rrd << ":" << endl;
    cout << "Vertex\tDistance" << endl;
    cout << "------\t--------" << endl;
    
    for (i_rrd = 0; i_rrd < graph_rrd->vertices_rrd; i_rrd++) {
        if (dist_rrd[i_rrd] == INT_MAX) {
            cout << "" << i_rrd << "\tINF" << endl;
        } else {
            cout << "" << i_rrd, dist_rrd[i_rrd] << "\t%d" << endl;
        }
    }
}

void printPath_rrd(struct Graph_rrd* graph_rrd, int src_rrd, int dest_rrd) {
    int dist_rrd[MAX_VERTICES];
    dijkstra_rrd(graph_rrd, src_rrd, dist_rrd);
    
    if (dist_rrd[dest_rrd] == INT_MAX) {
        cout << "No path exists from vertex " << src_rrd, dest_rrd << " to vertex %d" << endl;
    } else {
        cout << "Shortest distance from vertex " << src_rrd, dest_rrd, dist_rrd[dest_rrd] << " to vertex %d is: %d" << endl;
    }
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
    cout << "\n===== Dijkstra's Algorithm - Shortest Path =====" << endl;
    cout << "1. Create Graph with Sample Data" << endl;
    cout << "2. Add Edge to Graph" << endl;
    cout << "3. Display Graph" << endl;
    cout << "4. Find Shortest Paths from Source" << endl;
    cout << "5. Find Shortest Path between Two Vertices" << endl;
    cout << "6. Exit" << endl;
    cout << "==============================================" << endl;
    cout << "Enter your choice: ";
}

int main() {
    struct Graph_rrd* graph_rrd = NULL;
    int choice_rrd, src_rrd, dest_rrd, weight_rrd, vertices_rrd;
    
    cout << "Dijkstra's Algorithm for Shortest Path using Adjacency List" << endl;
    cout << "==========================================================" << endl;
    
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
                
                if (weight_rrd < 0) {
                    cout << "Edge weight must be non-negative!" << endl;
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
                cout << "Enter source vertex: ";
                cin >> src_rrd;
                
                if (src_rrd < 0 || src_rrd >= graph_rrd->vertices_rrd) {
                    cout << "Invalid source vertex!" << endl;
                    break;
                }
                
                printShortestPaths_rrd(graph_rrd, src_rrd);
                break;
                
            case 5:
                if (graph_rrd == NULL) {
                    cout << "Please create a graph first!" << endl;
                    break;
                }
                cout << "Enter source vertex: ";
                cin >> src_rrd;
                cout << "Enter destination vertex: ";
                cin >> dest_rrd;
                
                if (src_rrd < 0 || src_rrd >= graph_rrd->vertices_rrd || 
                    dest_rrd < 0 || dest_rrd >= graph_rrd->vertices_rrd) {
                    cout << "Invalid vertex numbers!" << endl;
                    break;
                }
                
                printPath_rrd(graph_rrd, src_rrd, dest_rrd);
                break;
                
            case 6:
                cout << "Thank you for using Dijkstra's Algorithm Implementation!" << endl;
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
Dijkstra's Algorithm for Shortest Path using Adjacency List
==========================================================

===== Dijkstra's Algorithm - Shortest Path =====
1. Create Graph with Sample Data
2. Add Edge to Graph
3. Display Graph
4. Find Shortest Paths from Source
5. Find Shortest Path between Two Vertices
6. Exit
==============================================
Enter your choice: 1
Enter number of vertices: 6
Graph with 6 vertices created successfully!

===== Dijkstra's Algorithm - Shortest Path =====
1. Create Graph with Sample Data
2. Add Edge to Graph
3. Display Graph
4. Find Shortest Paths from Source
5. Find Shortest Path between Two Vertices
6. Exit
==============================================
Enter your choice: 2
Enter source vertex: 0
Enter destination vertex: 1
Enter weight: 4
Edge added successfully!

===== Dijkstra's Algorithm - Shortest Path =====
1. Create Graph with Sample Data
2. Add Edge to Graph
3. Display Graph
4. Find Shortest Paths from Source
5. Find Shortest Path between Two Vertices
6. Exit
==============================================
Enter your choice: 2
Enter source vertex: 0
Enter destination vertex: 2
Enter weight: 3
Edge added successfully!

===== Dijkstra's Algorithm - Shortest Path =====
1. Create Graph with Sample Data
2. Add Edge to Graph
3. Display Graph
4. Find Shortest Paths from Source
5. Find Shortest Path between Two Vertices
6. Exit
==============================================
Enter your choice: 2
Enter source vertex: 1
Enter destination vertex: 2
Enter weight: 1
Edge added successfully!

===== Dijkstra's Algorithm - Shortest Path =====
1. Create Graph with Sample Data
2. Add Edge to Graph
3. Display Graph
4. Find Shortest Paths from Source
5. Find Shortest Path between Two Vertices
6. Exit
==============================================
Enter your choice: 2
Enter source vertex: 1
Enter destination vertex: 3
Enter weight: 2
Edge added successfully!

===== Dijkstra's Algorithm - Shortest Path =====
1. Create Graph with Sample Data
2. Add Edge to Graph
3. Display Graph
4. Find Shortest Paths from Source
5. Find Shortest Path between Two Vertices
6. Exit
==============================================
Enter your choice: 2
Enter source vertex: 2
Enter destination vertex: 3
Enter weight: 4
Edge added successfully!

===== Dijkstra's Algorithm - Shortest Path =====
1. Create Graph with Sample Data
2. Add Edge to Graph
3. Display Graph
4. Find Shortest Paths from Source
5. Find Shortest Path between Two Vertices
6. Exit
==============================================
Enter your choice: 2
Enter source vertex: 3
Enter destination vertex: 4
Enter weight: 2
Edge added successfully!

===== Dijkstra's Algorithm - Shortest Path =====
1. Create Graph with Sample Data
2. Add Edge to Graph
3. Display Graph
4. Find Shortest Paths from Source
5. Find Shortest Path between Two Vertices
6. Exit
==============================================
Enter your choice: 2
Enter source vertex: 3
Enter destination vertex: 5
Enter weight: 6
Edge added successfully!

===== Dijkstra's Algorithm - Shortest Path =====
1. Create Graph with Sample Data
2. Add Edge to Graph
3. Display Graph
4. Find Shortest Paths from Source
5. Find Shortest Path between Two Vertices
6. Exit
==============================================
Enter your choice: 2
Enter source vertex: 4
Enter destination vertex: 5
Enter weight: 3
Edge added successfully!

===== Dijkstra's Algorithm - Shortest Path =====
1. Create Graph with Sample Data
2. Add Edge to Graph
3. Display Graph
4. Find Shortest Paths from Source
5. Find Shortest Path between Two Vertices
6. Exit
==============================================
Enter your choice: 3

Graph Representation (Adjacency List):
Vertex 0: (2, 3) (1, 4) 
Vertex 1: (3, 2) (2, 1) 
Vertex 2: (3, 4) 
Vertex 3: (5, 6) (4, 2) 
Vertex 4: (5, 3) 
Vertex 5: 

===== Dijkstra's Algorithm - Shortest Path =====
1. Create Graph with Sample Data
2. Add Edge to Graph
3. Display Graph
4. Find Shortest Paths from Source
5. Find Shortest Path between Two Vertices
6. Exit
==============================================
Enter your choice: 4
Enter source vertex: 0

Shortest distances from vertex 0:
Vertex	Distance
------	--------
0	0
1	4
2	3
3	6
4	8
5	11

===== Dijkstra's Algorithm - Shortest Path =====
1. Create Graph with Sample Data
2. Add Edge to Graph
3. Display Graph
4. Find Shortest Paths from Source
5. Find Shortest Path between Two Vertices
6. Exit
==============================================
Enter your choice: 5
Enter source vertex: 0
Enter destination vertex: 5
Shortest distance from vertex 0 to vertex 5 is: 11
```

## Dry Run

For a directed graph with 6 vertices and the following edges:
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
- Vertex 1: (3,2) -> (2,1)
- Vertex 2: (3,4)
- Vertex 3: (5,6) -> (4,2)
- Vertex 4: (5,3)
- Vertex 5: (no outgoing edges)

**Finding shortest paths from vertex 0:**

**Initialization**:
- dist[] = {0, INF, INF, INF, INF, INF}
- visited[] = {0, 0, 0, 0, 0, 0}

**Iteration 1** (u=0):
- Add 0 to visited: visited[0] = 1
- Update neighbors: dist[1] = min(INF, 0+4) = 4, dist[2] = min(INF, 0+3) = 3
- dist[] = {0, 4, 3, INF, INF, INF}

**Iteration 2** (u=2):
- Add 2 to visited: visited[2] = 1
- Update neighbors: dist[3] = min(INF, 3+4) = 7
- dist[] = {0, 4, 3, 7, INF, INF}

**Iteration 3** (u=1):
- Add 1 to visited: visited[1] = 1
- Update neighbors: dist[3] = min(7, 4+2) = 6, dist[2] = min(3, 4+1) = 3 (no change)
- dist[] = {0, 4, 3, 6, INF, INF}

**Iteration 4** (u=3):
- Add 3 to visited: visited[3] = 1
- Update neighbors: dist[4] = min(INF, 6+2) = 8, dist[5] = min(INF, 6+6) = 12
- dist[] = {0, 4, 3, 6, 8, 12}

**Iteration 5** (u=4):
- Add 4 to visited: visited[4] = 1
- Update neighbors: dist[5] = min(12, 8+3) = 11
- dist[] = {0, 4, 3, 6, 8, 11}

**Final Result**:
- Shortest distances from vertex 0: [0, 4, 3, 6, 8, 11]

## Conclusion

The implementation demonstrates Dijkstra's algorithm for finding the shortest path between nodes using adjacency list representation with the following key features:

**Algorithm Complexity**:
1. **Time Complexity**: O(V²) with simple implementation, O(E + V log V) with binary heap
2. **Space Complexity**: O(V + E) for adjacency list representation
3. **Adjacency List Access**: O(degree) for accessing neighbors of a vertex
4. **Min Distance Finding**: O(V) for each iteration

**Key Implementation Features**:
1. **Non-negative Weights**: Handles only non-negative edge weights
2. **Single Source Shortest Path**: Finds shortest paths from one source to all vertices
3. **Adjacency List**: Memory-efficient graph representation
4. **Directed Graph**: Handles directed edges correctly
5. **User Interface**: Interactive menu-driven system
6. **Proper Cleanup**: Memory deallocation to prevent leaks

**Advantages of Dijkstra's Algorithm**:
1. **Correctness**: Guarantees shortest path for non-negative weights
2. **Simplicity**: Easy to understand and implement
3. **Optimality**: Produces optimal solutions
4. **Flexibility**: Can be optimized with priority queues

**Advantages of Adjacency List**:
1. **Space Efficiency**: O(V + E) space compared to O(V²) for adjacency matrix
2. **Flexibility**: Easy to add/remove edges
3. **Iteration**: Efficient iteration over neighbors
4. **Scalability**: Better for sparse graphs

**Limitations**:
1. **Negative Weights**: Doesn't work with negative edge weights
2. **Time Complexity**: O(V²) can be slow for large graphs without optimization
3. **Space for Dense Graphs**: For very dense graphs, adjacency matrix might be more efficient

**Real-world Applications**:
1. **GPS Navigation**: Finding shortest routes between locations
2. **Network Routing**: Determining optimal paths in computer networks
3. **Game Development**: Pathfinding in games
4. **Social Networks**: Finding shortest connection paths
5. **Supply Chain**: Optimizing delivery routes
6. **Internet Routing**: BGP and other routing protocols

The implementation correctly handles all edge cases:
- Disconnected graphs
- Single vertex graphs
- Invalid vertex numbers
- Negative edge weights (rejected)
- Memory management to prevent leaks
- Proper adjacency list construction for directed graphs

This system efficiently finds the shortest paths from a single source to all other vertices in a weighted graph using Dijkstra's algorithm with adjacency list representation, providing optimal space usage for sparse graphs.
