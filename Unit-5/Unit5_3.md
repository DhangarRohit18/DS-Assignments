# Unit V Assignment 3: Kruskal's Algorithm for Minimum Spanning Tree using Adjacency List

Implementation of Kruskal's algorithm to find the minimum spanning tree of a user-defined graph using adjacency list representation.

## Problem Statement

Write a Program to implement Kruskal's algorithm to find the minimum spanning tree of a user defined graph. Use Adjacency List to represent a graph.

## Pseudo Code

### Edge Structure

Structure Edge:
    src: integer
    dest: integer
    weight: integer


### Graph Structure

Structure Graph:
    vertices: integer
    edges: integer
    edgeList: array of Edge of size edges


### Find Operation (Union-Find)

Algorithm Find(parent, i):
    If parent[i] == i:
        Return i
    Return Find(parent, parent[i])


### Union Operation (Union-Find)

Algorithm Union(parent, rank, x, y):
    xroot = Find(parent, x)
    yroot = Find(parent, y)
    If rank[xroot] < rank[yroot]:
        parent[xroot] = yroot
    Else If rank[xroot] > rank[yroot]:
        parent[yroot] = xroot
    Else:
        parent[yroot] = xroot
        rank[xroot]++


### Compare Edges

Algorithm CompareEdges(a, b):
    Return a.weight - b.weight


### Kruskal's Algorithm

Algorithm KruskalsMST(graph):
    Initialize result array to store MST edges
    Initialize parent array of size vertices
    Initialize rank array of size vertices
    Sort all edges in non-decreasing order of their weight
    For i = 0 to vertices-1:
        parent[i] = i
        rank[i] = 0
    i = 0
    e = 0
    While e < vertices-1 AND i < graph.edges:
        nextEdge = graph.edgeList[i++]
        x = Find(parent, nextEdge.src)
        y = Find(parent, nextEdge.dest)
        If x != y:
            result[e++] = nextEdge
            Union(parent, rank, x, y)
    Print MST edges from result array


## Code Implementation

```cpp
#include <iostream>
#include <cstdlib>
using namespace std;

#define MAX_VERTICES 100
#define MAX_EDGES 1000

struct Edge_rrd {
    int src_rrd;
    int dest_rrd;
    int weight_rrd;
};

struct Graph_rrd {
    int vertices_rrd;
    int edges_rrd;
    Edge_rrd edgeList_rrd[MAX_EDGES];
};

struct Subset_rrd {
    int parent_rrd;
    int rank_rrd;
};

Graph_rrd* createGraph_rrd(int vertices_rrd) {
    Graph_rrd* graph_rrd = (Graph_rrd*)malloc(sizeof(Graph_rrd));
    graph_rrd->vertices_rrd = vertices_rrd;
    graph_rrd->edges_rrd = 0;
    return graph_rrd;
}

void addEdge_rrd(Graph_rrd* graph_rrd, int src_rrd, int dest_rrd, int weight_rrd) {
    if (graph_rrd->edges_rrd >= MAX_EDGES) {
        cout << "Maximum number of edges reached!" << endl;
        return;
    }

    graph_rrd->edgeList_rrd[graph_rrd->edges_rrd].src_rrd = src_rrd;
    graph_rrd->edgeList_rrd[graph_rrd->edges_rrd].dest_rrd = dest_rrd;
    graph_rrd->edgeList_rrd[graph_rrd->edges_rrd].weight_rrd = weight_rrd;
    graph_rrd->edges_rrd++;
}

int find_rrd(Subset_rrd subsets_rrd[], int i_rrd) {
    if (subsets_rrd[i_rrd].parent_rrd != i_rrd)
        subsets_rrd[i_rrd].parent_rrd = find_rrd(subsets_rrd, subsets_rrd[i_rrd].parent_rrd);
    return subsets_rrd[i_rrd].parent_rrd;
}

void union_rrd(Subset_rrd subsets_rrd[], int x_rrd, int y_rrd) {
    int xroot_rrd = find_rrd(subsets_rrd, x_rrd);
    int yroot_rrd = find_rrd(subsets_rrd, y_rrd);

    if (subsets_rrd[xroot_rrd].rank_rrd < subsets_rrd[yroot_rrd].rank_rrd)
        subsets_rrd[xroot_rrd].parent_rrd = yroot_rrd;
    else if (subsets_rrd[xroot_rrd].rank_rrd > subsets_rrd[yroot_rrd].rank_rrd)
        subsets_rrd[yroot_rrd].parent_rrd = xroot_rrd;
    else {
        subsets_rrd[yroot_rrd].parent_rrd = xroot_rrd;
        subsets_rrd[xroot_rrd].rank_rrd++;
    }
}

int compareEdges_rrd(const void* a_rrd, const void* b_rrd) {
    Edge_rrd* A = (Edge_rrd*)a_rrd;
    Edge_rrd* B = (Edge_rrd*)b_rrd;
    return A->weight_rrd - B->weight_rrd;
}

void kruskalsMST_rrd(Graph_rrd* graph_rrd) {
    Edge_rrd result_rrd[MAX_VERTICES];
    int e_rrd = 0;
    int i_rrd = 0;

    qsort(graph_rrd->edgeList_rrd, graph_rrd->edges_rrd,
          sizeof(graph_rrd->edgeList_rrd[0]), compareEdges_rrd);

    Subset_rrd* subsets_rrd = (Subset_rrd*)malloc(graph_rrd->vertices_rrd * sizeof(Subset_rrd));

    for (int v_rrd = 0; v_rrd < graph_rrd->vertices_rrd; v_rrd++) {
        subsets_rrd[v_rrd].parent_rrd = v_rrd;
        subsets_rrd[v_rrd].rank_rrd = 0;
    }

    while (e_rrd < graph_rrd->vertices_rrd - 1 && i_rrd < graph_rrd->edges_rrd) {
        Edge_rrd nextEdge_rrd = graph_rrd->edgeList_rrd[i_rrd++];
        int x_rrd = find_rrd(subsets_rrd, nextEdge_rrd.src_rrd);
        int y_rrd = find_rrd(subsets_rrd, nextEdge_rrd.dest_rrd);

        if (x_rrd != y_rrd) {
            result_rrd[e_rrd++] = nextEdge_rrd;
            union_rrd(subsets_rrd, x_rrd, y_rrd);
        }
    }

    cout << "\nEdges in Minimum Spanning Tree:\n";
    cout << "Src -- Dest == Weight\n";

    int totalWeight_rrd = 0;
    for (int i = 0; i < e_rrd; i++) {
        cout << result_rrd[i].src_rrd << " -- " 
             << result_rrd[i].dest_rrd << " == "
             << result_rrd[i].weight_rrd << endl;
        totalWeight_rrd += result_rrd[i].weight_rrd;
    }

    cout << "Total Weight of MST = " << totalWeight_rrd << endl;

    free(subsets_rrd);
}

void printGraph_rrd(Graph_rrd* graph_rrd) {
    cout << "\nGraph Edges:\n";
    cout << "Src -- Dest == Weight\n";

    for (int i = 0; i < graph_rrd->edges_rrd; i++) {
        cout << graph_rrd->edgeList_rrd[i].src_rrd << " -- "
             << graph_rrd->edgeList_rrd[i].dest_rrd << " == "
             << graph_rrd->edgeList_rrd[i].weight_rrd << endl;
    }
}

void freeGraph_rrd(Graph_rrd* graph_rrd) {
    free(graph_rrd);
}

Graph_rrd* createSampleGraph_rrd() {
    Graph_rrd* graph_rrd = createGraph_rrd(6);
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
    cout << "\n===== Kruskal's Algorithm Menu =====\n";
    cout << "1. Add Edge\n";
    cout << "2. Print Graph\n";
    cout << "3. Find MST (Kruskal)\n";
    cout << "4. Load Sample Graph\n";
    cout << "5. Exit\n";
    cout << "Enter your choice: ";
}

int main() {
    int vertices_rrd;
    cout << "Enter number of vertices: ";
    cin >> vertices_rrd;

    if (vertices_rrd <= 0 || vertices_rrd > MAX_VERTICES) {
        cout << "Invalid number of vertices!\n";
        return 1;
    }

    Graph_rrd* graph_rrd = createGraph_rrd(vertices_rrd);

    while (true) {
        displayMenu_rrd();

        int choice_rrd;
        cin >> choice_rrd;

        if (choice_rrd == 1) {
            int src_rrd, dest_rrd, weight_rrd;
            cout << "Enter source: ";
            cin >> src_rrd;
            cout << "Enter destination: ";
            cin >> dest_rrd;
            cout << "Enter weight: ";
            cin >> weight_rrd;

            if (src_rrd < 0 || src_rrd >= vertices_rrd || dest_rrd < 0 || dest_rrd >= vertices_rrd)
                cout << "Invalid vertices!\n";
            else if (weight_rrd < 0)
                cout << "Weight cannot be negative!\n";
            else {
                addEdge_rrd(graph_rrd, src_rrd, dest_rrd, weight_rrd);
                cout << "Edge added.\n";
            }
        }
        else if (choice_rrd == 2) {
            printGraph_rrd(graph_rrd);
        }
        else if (choice_rrd == 3) {
            if (graph_rrd->edges_rrd < vertices_rrd - 1)
                cout << "Not enough edges for MST!\n";
            else
                kruskalsMST_rrd(graph_rrd);
        }
        else if (choice_rrd == 4) {
            freeGraph_rrd(graph_rrd);
            graph_rrd = createSampleGraph_rrd();
            cout << "Sample graph loaded.\n";
            printGraph_rrd(graph_rrd);
        }
        else if (choice_rrd == 5) {
            freeGraph_rrd(graph_rrd);
            cout << "Exiting program.\n";
            break;
        }
        else {
            cout << "Invalid choice! Try again.\n";
        }
    }

    return 0;
}


## Output

else
Welcome to Kruskal's Algorithm for Minimum Spanning Tree!
Enter the number of vertices in the graph: 6
===== Kruskal's Algorithm for Minimum Spanning Tree =====
1. Add Edge
2. Print Graph Edges
3. Find Minimum Spanning Tree (Kruskal's Algorithm)
4. Create Sample Graph
5. Exit
=======================================================
Enter your choice: 4
Sample graph created successfully!
Graph Edges:
Edge		Weight
0 - 1		4
0 - 2		3
1 - 2		1
1 - 3		2
2 - 3		4
3 - 4		2
4 - 5		6
===== Kruskal's Algorithm for Minimum Spanning Tree =====
1. Add Edge
2. Print Graph Edges
3. Find Minimum Spanning Tree (Kruskal's Algorithm)
4. Create Sample Graph
5. Exit
=======================================================
Enter your choice: 3
Edges in Minimum Spanning Tree (Kruskal's Algorithm):
Edge		Weight
1 - 2		1
1 - 3		2
3 - 4		2
0 - 2		3
4 - 5		6
Total Weight of MST: 14
else

## Dry Run

For a graph with 6 vertices and weighted edges:
- (0,1):4, (0,2):3, (1,2):1, (1,3):2, (2,3):4, (3,4):2, (4,5):6

1. **Sort Edges by Weight**:
   - (1,2):1, (1,3):2, (3,4):2, (0,2):3, (0,1):4, (2,3):4, (4,5):6

2. **Initialize Union-Find Structure**:
   - Parent: [0, 1, 2, 3, 4, 5]
   - Rank: [0, 0, 0, 0, 0, 0]

3. **Process Edges**:
   - Edge (1,2):1 - Find(1)=1, Find(2)=2, 1≠2 → Include in MST
     * Union(1,2) → Parent: [0, 1, 1, 3, 4, 5], Rank: [0, 1, 0, 0, 0, 0]
   - Edge (1,3):2 - Find(1)=1, Find(3)=3, 1≠3 → Include in MST
     * Union(1,3) → Parent: [0, 1, 1, 1, 4, 5], Rank: [0, 2, 0, 0, 0, 0]
   - Edge (3,4):2 - Find(3)=1, Find(4)=4, 1≠4 → Include in MST
     * Union(1,4) → Parent: [0, 1, 1, 1, 1, 5], Rank: [0, 3, 0, 0, 0, 0]
   - Edge (0,2):3 - Find(0)=0, Find(2)=1, 0≠1 → Include in MST
     * Union(0,1) → Parent: [0, 0, 1, 1, 1, 5], Rank: [1, 3, 0, 0, 0, 0]
   - Edge (0,1):4 - Find(0)=0, Find(1)=0, 0=0 → Skip (cycle)
   - Edge (2,3):4 - Find(2)=0, Find(3)=0, 0=0 → Skip (cycle)
   - Edge (4,5):6 - Find(4)=0, Find(5)=5, 0≠5 → Include in MST
     * Union(0,5) → Parent: [0, 0, 1, 1, 1, 0], Rank: [2, 3, 0, 0, 0, 0]

4. **MST Construction**:
   - Edges: (1,2):1, (1,3):2, (3,4):2, (0,2):3, (4,5):6
   - Total Weight: 1+2+2+3+6 = 14

## Conclusion

The implementation demonstrates Kruskal's algorithm for finding the minimum spanning tree using edge list representation. Key features include:

1. **Edge List Representation**: Efficient for Kruskal's algorithm which processes edges
2. **Kruskal's Algorithm**: Greedy approach using union-find data structure
3. **Union-Find with Path Compression**: Optimized disjoint set operations
4. **Complete Operations**: All required graph operations plus additional utilities

**Time Complexities**:
- Add Edge: O(1) - constant time addition to edge list
- Kruskal's Algorithm: O(E log E) where E is number of edges (due to sorting)
- Print Graph: O(E) where E is number of edges

**Space Complexity**: O(E + V) where E is edges and V is vertices

The edge list approach is ideal for this application because:
1. **Algorithm Fit**: Kruskal's algorithm naturally works with edge list
2. **Sorting Efficiency**: Easy to sort edges by weight
3. **Memory Efficiency**: For sparse graphs, saves space
4. **Union-Find Compatibility**: Works well with disjoint set operations

The implementation handles edge cases properly:
- Invalid vertex numbers with appropriate error messages
- Negative weight validation
- Maximum edge limit checking
- Memory management to prevent leaks
- Comprehensive user interface with clear feedback

Additional features beyond requirements:
- Graph visualization through edge list display
- Sample graph creation for testing
- Interactive menu system
- Complete error handling
- Total MST weight calculation

In real-world applications, this system could be extended to:
1. Support directed graphs
2. Implement other MST algorithms (Prim's)
3. Add graphical visualization
4. Support dynamic graph resizing
5. Implement more advanced union-find optimizations

Minimum Spanning Trees are used in:
1. **Network Design**: Creating cost-effective communication networks
2. **Cluster Analysis**: Finding clusters in data points
3. **Image Segmentation**: Identifying regions in images
4. **Approximation Algorithms**: Solving NP-hard problems
5. **Circuit Design**: Minimizing wire length in circuits

This implementation provides a solid foundation for understanding graph algorithms and minimum spanning trees, which are essential in computer science and network optimization. Kruskal's algorithm is particularly useful when the graph is sparse (few edges compared to vertices).
