Dijkstra’s Algorithm in C (Shortest Path Using Adjacency Matrix)

This project implements *Dijkstra’s Shortest Path Algorithm* in C using an *Adjacency Matrix* representation of a graph.

It calculates the shortest distance from a *source vertex* to all other vertices in a *weighted graph*.

---

Project Description

This program:

* Accepts:

  * Number of vertices
  * Adjacency matrix (weighted graph)
  * Starting/source vertex
* Computes shortest paths using *Dijkstra’s Algorithm*
* Displays the minimum distance from source to every vertex

---

What is Dijkstra’s Algorithm?

Dijkstra’s Algorithm finds the *shortest path* from a source node to all other nodes in a graph with:

* Non-negative edge weights
* Greedy approach
* Time complexity: *O(V²)* (for adjacency matrix implementation)

---

Example Graph

Example weighted graph:

![Image](https://www.researchgate.net/publication/345708122/figure/fig3/AS%3A956524520292353%401605064625415/The-complete-graph-on-4-vertices-with-all-edge-weights-equal-to-1-The-labels-on-edges.png)

![Image](https://ucarecdn.com/a67cb888-aa0c-424b-8c7f-847e38dd5691/)

Example adjacency matrix:


0 10 0 30
10 0 50 0
0 50 0 20
30 0 20 0


If starting vertex = 0, shortest paths will be computed from vertex 0.

---

 Source Code

c

#include <stdio.h>

#define MAX 10

#define INF 9999

int minDistance(int dist[], int visited[], int n) {
    
    int min = INF, min_index = -1;

    for (int i = 0; i < n; i++) {
        
        if (visited[i] == 0 && dist[i] < min) {
            min = dist[i];
            min_index = i;
        }
    }
    return min_index;
}

void dijkstra(int graph[MAX][MAX], int n, int start) {
    
    int dist[MAX], visited[MAX];

    for (int i = 0; i < n; i++) {
        dist[i] = INF;
        visited[i] = 0;
    }

    dist[start] = 0;

    for (int count = 0; count < n - 1; count++) {
        
        int u = minDistance(dist, visited, n);
        visited[u] = 1;

        for (int v = 0; v < n; v++) {
           
            if (!visited[v] && graph[u][v] != 0 &&
                dist[u] + graph[u][v] < dist[v]) {
                dist[v] = dist[u] + graph[u][v];
            }
        }
    }

    printf("\nVertex\tDistance from Source\n");
    
    for (int i = 0; i < n; i++) {
        printf("%d\t%d\n", i, dist[i]);
    }
}

int main() {
    
    int graph[MAX][MAX], n, start;

    printf("Enter number of vertices: ");
    scanf("%d", &n);

    printf("Enter adjacency matrix (0 if no edge):\n");
    
    for (int i = 0; i < n; i++)
        for (int j = 0; j < n; j++)
            scanf("%d", &graph[i][j]);

    printf("Enter starting vertex: ");
    scanf("%d", &start);

    dijkstra(graph, n, start);

    return 0;
}   
---

How to Compile and Run

Using GCC

1. Save the file as:


dijkstra.c


2. Compile:

bash
gcc dijkstra.c -o dijkstra


3. Run:

bash
./dijkstra


(On Windows: dijkstra.exe)

---

Sample Input


Enter number of vertices: 4
Enter adjacency matrix (0 if no edge):
0 10 0 30
10 0 50 0
0 50 0 20
30 0 20 0
Enter starting vertex: 0


---

Sample Output


Vertex  Distance from Source
0       0
1       10
2       50
3       30


---

Time and Space Complexity

| Component        | Complexity |
| ---------------- | ---------- |
| Time Complexity  | O(V²)      |
| Space Complexity | O(V²)      |

Where:

* *V* = Number of vertices

---

Concepts Covered

* Graph Data Structure
* Adjacency Matrix
* Greedy Algorithm
* Shortest Path Problem
* Distance Relaxation
* Visited Array

---

How It Works

1. Initialize all distances to infinity (INF)
2. Set source distance to 0
3. Select the minimum unvisited vertex
4. Update (relax) its adjacent vertices
5. Repeat until all vertices are visited

---

Possible Improvements

* Use adjacency list with priority queue → O((V + E) log V)
* Add path reconstruction (print actual shortest path)
* Detect invalid input
* Add directed graph support
* Use dynamic memory instead of fixed MAX

---

Learning Outcome

After completing this project, you will understand:

* How shortest path algorithms work
* Difference between greedy and dynamic programming approaches
* Graph traversal with weight consideration
* Real-world applications (GPS, networking, routing systems)

---
