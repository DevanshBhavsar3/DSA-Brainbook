22-11-2025  15:29

Status:

Tags: [[Tags/DSA|DSA]] [[Graphs]]

# Introduction to Graphs

![[Pasted image 20251122153033.png]]

- The circle drawn in the graph are called **Nodes** or **Vertices**.
- The line that connects two nodes are called **Edge**.

There are various types of graphs:
#### Directed Graph
You can travel to both the nodes from the same edge.

#### Undirected Graph
You can only travel to directed node from the edge.

#### Cyclic Graph
The graph in which you can start from a node and again reach that node.

#### Acyclic Graph
The graph in which you can start from a node and can't reach that node again via any path.


### Path
A path is a series of **unique** vertices which can be used to reach from point A to point B. 


### Degrees in Graph

#### Undirected Graph

The degree of any node in the undirected graph is the total edges connected to it.

The degree of the graph = 2 * No. of edges, because every edge is connected to 2 nodes.

#### Directed Graph

The **In-degree** of the node is total no. of edged directing to the node.

The **Out-degree** of the node is the total edges going out of the node.


### Edge Weight

The edges of the graph can have weights assigned to them. If not, you would consider Unit Weights (1).



### Code Representation

#### Adjacency Matrix

- Create N x N matrix to represent connection of i, j node.
- Space Complexity: $O(N^2)$

```cpp
#include <iostream>
using namespace std;

int main(void) {
  int n, m;

  cin >> n >> m;
  
  int adj[n + 1][n + 1];
  
  for (int i = 0; i < m; i++) {
    int u, v;
    cin >> u >> v;
	
    adj[u][v] = 1;
    adj[v][u] = 1;
  }
  
  return 0;
}
```

#### Adjacency List

- Create a list of size n, where each node index will store its neighbor nodes.
- Space Complexity: $O(2E)$

```cpp
#include <iostream>
#include <vector>
using namespace std;

int main(void) {
  int n, m;

  cin >> n >> m;

  vector<int> adj[n + 1];

  for (int i = 0; i < m; i++) {
    int u, v;
    cin >> u >> v;
	
    adj[u].push_back(v);
    adj[v].push_back(u);
  }

  return 0;
}
```





# References