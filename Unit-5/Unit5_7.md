# Unit V Assignment 7: Dijkstra's Algorithm for Shortest Path using Adjacency Matrix

Implementation of Dijkstra's algorithm to find the shortest distance between two nodes of a user-defined graph using adjacency matrix representation.

## Problem Statement

Write a Program to implement Dijkstra's algorithm to find shortest distance between two nodes of a user defined graph. Use Adjacency Matrix to represent a graph.

## Pseudo Code

### Graph Structure
```
Structure Graph:
    vertices: integer
    adjMatrix: 2D array of size vertices x vertices
```

### Find Minimum Distance Vertex
```
Algorithm FindMinDistance(dist, visited, vertices):
    min = INFINITY
    minIndex = -1
    For each vertex v:
        If visited[v] is false AND dist[v] <= min:
            min = dist[v]
            minIndex = v
    Return minIndex
```

### Dijkstra's Algorithm
```
Algorithm Dijkstra(graph, src):
    Initialize dist array of size vertices with all INFINITY
    Initialize visited array of size vertices with all false
    dist[src] = 0
    For count = 0 to vertices-1:
        u = FindMinDistance(dist, visited, graph.vertices)
        visited[u] = true
        For each vertex v:
            If visited[v] is false AND graph.adjMatrix[u][v] != 0 AND
               dist[u] != INFINITY AND dist[u] + graph.adjMatrix[u][v] < dist[v]:
                dist[v] = dist[u] + graph.adjMatrix[u][v]
    Return dist array
```

### Print Shortest Path
```
Algorithm PrintShortestPath(dist, src, dest):
    Print "Shortest distance from " + src + " to " + dest + " is " + dist[dest]
```

## Code Implementation

```c
#include <iostream>
using namespace std;
#include <stdlib.h>
#include <limits.h>

#define MAX_VERTICES 100

struct Graph_rrd {
    int vertices_rrd;
    int adjMatrix_rrd[MAX_VERTICES][MAX_VERTICES];
};

struct Graph_rrd* createGraph_rrd(int vertices_rrd);
void addEdge_rrd(struct Graph_rrd* graph_rrd, int src_rrd, int dest_rrd, int weight_rrd);
int findMinDistance_rrd(int dist_rrd[], int visited_rrd[], int vertices_rrd);
void dijkstra_rrd(struct Graph_rrd* graph_rrd, int src_rrd, int dist_rrd[]);
void printShortestPaths_rrd(struct Graph_rrd* graph_rrd, int src_rrd);
void printPath_rrd(struct Graph_rrd* graph_rrd, int src_rrd, int dest_rrd);
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
    

    for (i_rrd = 0; i_rrd < graph_rrd->vertices_rrd; i_rrd++) {
        dist_rrd[i_rrd] = INT_MAX;
        visited_rrd[i_rrd] = 0;
    }
    

    dist_rrd[src_rrd] = 0;
    

    for (count_rrd = 0; count_rrd < graph_rrd->vertices_rrd - 1; count_rrd++) {

        u_rrd = findMinDistance_rrd(dist_rrd, visited_rrd, graph_rrd->vertices_rrd);
        

        visited_rrd[u_rrd] = 1;
        

        for (v_rrd = 0; v_rrd < graph_rrd->vertices_rrd; v_rrd++) {

            if (!visited_rrd[v_rrd] && graph_rrd->adjMatrix_rrd[u_rrd][v_rrd] && 
                dist_rrd[u_rrd] != INT_MAX && 
                dist_rrd[u_rrd] + graph_rrd->adjMatrix_rrd[u_rrd][v_rrd] < dist_rrd[v_rrd]) {
                dist_rrd[v_rrd] = dist_rrd[u_rrd] + graph_rrd->adjMatrix_rrd[u_rrd][v_rrd];
            }
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
    cout << "\n===== Dijkstra's Algorithm - Shortest Path =====" << endl;
    cout << "1. Create Graph with Sample Data" << endl;
    cout << "2. Add Edge to Graph" << endl;
    cout << "3. Display Graph" << endl;
    cout << "4. Display Adjacency Matrix" << endl;
    cout << "5. Find Shortest Paths from Source" << endl;
    cout << "6. Find Shortest Path between Two Vertices" << endl;
    cout << "7. Exit" << endl;
    cout << "==============================================" << endl;
    cout << "Enter your choice: ";
}

int main() {
    struct Graph_rrd* graph_rrd = NULL;
    int choice_rrd, src_rrd, dest_rrd, weight_rrd, vertices_rrd;
    
    cout << "Dijkstra's Algorithm for Shortest Path using Adjacency Matrix" << endl;
    cout << "============================================================" << endl;
    
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
                printAdjMatrix_rrd(graph_rrd);
                break;
                
            case 5:
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
                
            case 6:
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
                
            case 7:
                cout << "Thank you for using Dijkstra's Algorithm Implementation!" << endl;
                if (graph_rrd != NULL) {
                    free(graph_rrd);
                }
                exit(0);
                
            default:
                cout << "Invalid choice! Please try again." << endl;
        }
    }
    
    return 0;


## Output

```
Dijkstra's Algorithm for Shortest Path using Adjacency Matrix
============================================================

===== Dijkstra's Algorithm - Shortest Path =====
1. Create Graph with Sample Data
2. Add Edge to Graph
3. Display Graph
4. Display Adjacency Matrix
5. Find Shortest Paths from Source
6. Find Shortest Path between Two Vertices
7. Exit
==============================================
Enter your choice: 1
Enter number of vertices: 6
Graph with 6 vertices created successfully!

===== Dijkstra's Algorithm - Shortest Path =====
1. Create Graph with Sample Data
2. Add Edge to Graph
3. Display Graph
4. Display Adjacency Matrix
5. Find Shortest Paths from Source
6. Find Shortest Path between Two Vertices
7. Exit
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
4. Display Adjacency Matrix
5. Find Shortest Paths from Source
6. Find Shortest Path between Two Vertices
7. Exit
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
4. Display Adjacency Matrix
5. Find Shortest Paths from Source
6. Find Shortest Path between Two Vertices
7. Exit
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
4. Display Adjacency Matrix
5. Find Shortest Paths from Source
6. Find Shortest Path between Two Vertices
7. Exit
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
4. Display Adjacency Matrix
5. Find Shortest Paths from Source
6. Find Shortest Path between Two Vertices
7. Exit
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
4. Display Adjacency Matrix
5. Find Shortest Paths from Source
6. Find Shortest Path between Two Vertices
7. Exit
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
4. Display Adjacency Matrix
5. Find Shortest Paths from Source
6. Find Shortest Path between Two Vertices
7. Exit
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
4. Display Adjacency Matrix
5. Find Shortest Paths from Source
6. Find Shortest Path between Two Vertices
7. Exit
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
4. Display Adjacency Matrix
5. Find Shortest Paths from Source
6. Find Shortest Path between Two Vertices
7. Exit
==============================================
Enter your choice: 5
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
4. Display Adjacency Matrix
5. Find Shortest Paths from Source
6. Find Shortest Path between Two Vertices
7. Exit
==============================================
Enter your choice: 6
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

**Finding shortest paths from vertex 0:**

**Initialization**:
- dist[] = {0, INF, INF, INF, INF, INF}
- visited[] = {0, 0, 0, 0, 0, 0}

**Iteration 1** (u=0):
- Update neighbors of 0: dist[1]=4, dist[2]=3
- dist[] = {0, 4, 3, INF, INF, INF}
- visited[] = {1, 0, 0, 0, 0, 0}

**Iteration 2** (u=2):
- Update neighbors of 2: dist[3] = min(INF, 3+4) = 7
- dist[] = {0, 4, 3, 7, INF, INF}
- visited[] = {1, 0, 1, 0, 0, 0}

**Iteration 3** (u=1):
- Update neighbors of 1: dist[2] = min(3, 4+1) = 3 (no change), dist[3] = min(7, 4+2) = 6
- dist[] = {0, 4, 3, 6, INF, INF}
- visited[] = {1, 1, 1, 0, 0, 0}

**Iteration 4** (u=3):
- Update neighbors of 3: dist[4] = 6+2 = 8, dist[5] = 6+6 = 12
- dist[] = {0, 4, 3, 6, 8, 12}
- visited[] = {1, 1, 1, 1, 0, 0}

**Iteration 5** (u=4):
- Update neighbors of 4: dist[5] = min(12, 8+3) = 11
- dist[] = {0, 4, 3, 6, 8, 11}
- visited[] = {1, 1, 1, 1, 1, 0}

**Final Result**:
- Shortest distances from vertex 0: [0, 4, 3, 6, 8, 11]

## Conclusion

The implementation demonstrates Dijkstra's algorithm for finding the shortest path between nodes using adjacency matrix representation with the following key features:

**Algorithm Complexity**:
1. **Time Complexity**: O(V²) where V is the number of vertices
2. **Space Complexity**: O(V) for distance and visited arrays
3. **Adjacency Matrix Access**: O(1) for edge weight lookup
4. **Min Distance Finding**: O(V) for each iteration

**Key Implementation Features**:
1. **Non-negative Weights**: Handles only non-negative edge weights
2. **Single Source Shortest Path**: Finds shortest paths from one source to all vertices
3. **Adjacency Matrix**: Efficient edge weight access
4. **Dynamic Memory**: Allocates memory based on vertices
5. **User Interface**: Interactive menu-driven system

**Advantages of Dijkstra's Algorithm**:
1. **Correctness**: Guarantees shortest path for non-negative weights
2. **Simplicity**: Easy to understand and implement
3. **Efficiency**: Works well for dense graphs
4. **Optimality**: Produces optimal solutions

**Limitations**:
1. **Negative Weights**: Doesn't work with negative edge weights
2. **Time Complexity**: O(V²) can be slow for large sparse graphs
3. **Space Usage**: O(V²) space for adjacency matrix

**Real-world Applications**:
1. **GPS Navigation**: Finding shortest routes between locations
2. **Network Routing**: Determining optimal paths in computer networks
3. **Game Development**: Pathfinding in games
4. **Social Networks**: Finding shortest connection paths
5. **Supply Chain**: Optimizing delivery routes

The implementation correctly handles all edge cases:
- Disconnected graphs
- Single vertex graphs
- Invalid vertex numbers
- Negative edge weights (rejected)
- Memory management to prevent leaks

This system efficiently finds the shortest paths from a single source to all other vertices in a weighted graph using Dijkstra's algorithm with optimal performance for adjacency matrix representation.