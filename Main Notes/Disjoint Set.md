08-01-2026  14:47

Status: #Revision

Tags: [[Tags/DSA|DSA]] [[Graphs]]

# Disjoint Set

- Disjoint set are mainly used to check if the nodes u & v belongs to the same components at point of time. As it creates disjoint sets of the graph.
- It provides main 2 functionalities,
	-  ```findParent()```: Returns the ultimate parent
	-  ```union()```: Unite 2 nodes of the graph. ( Implemented by Rank / Size )


###  Union by Rank

- Find the ultimate parent of u & v.
- Find rank of those parent.
- If both parent are not same, connect smaller rank parent to larger rank parent.
- If the rank of both parent are similar, connect anyone to the other and increase the rank by 1.

> We are connecting smaller rank parent to the larger rank parent because, more rank means more height resulting in greater time complexity in path compression.

###  Union by Size

- Instead of storing the rank we can store the size of the nodes in the set.
- If ultimate parent of both nodes are not same, connect smaller sized parent to larger sized parent.


### Disjoint Set Template

```cpp
#include <bits/stdc++.h>
using namespace std;

class DisjointSet {
private:
	vector<int> rank, parent, size;
public:
	DisjointSet(int n) {
	    rank.resize(n + 1, 0);
	    parent.resize(n + 1);
	    size.resize(n + 1, 1);
		
	    for (int i = 0; i <= n; i++) {
		    parent[i] = i;
	    }
	}
	
	// Path compression
	int findParent(int node) {
	    if (parent[node] == node) {
		    return node;
	    }
		
		parent[node] = findParent(parent[node]);
		
	    return parent[node];
	}
	
	void unionByRank(int u, int v) {
	    int pU = findParent(u);
	    int pV = findParent(v);
		
	    if (pU == pV) {
		    return;
	    }
		
	    if (rank[pU] == rank[pV]) {
			parent[pV] = pU;
			rank[pU]++;
	    } else if (rank[pU] > rank[pV]) {
			parent[pV] = pU;
	    } else {
			parent[pU] = pV;
	    }
	}
	
	void unionBySize(int u, int v) {
	    int pU = findParent(u);
	    int pV = findParent(v);
		
	    if (pU == pV) {
		    return;
	    }
		
	    if (size[pU] > size[pV]) {
			parent[pV] = pU;
			size[pU] += size[pV];
	    } else {
		    parent[pU] = pV;
		    size[pV] += size[pU];
	    }
	}
};

int main(void) {
	DisjointSet ds(7);
	
	ds.unionBySize(1, 2);
	ds.unionBySize(2, 3);
	ds.unionBySize(4, 5);
	ds.unionBySize(6, 7);
	ds.unionBySize(5, 6);
	
	if (ds.findParent(3) == ds.findParent(7)) {
		cout << "Same\n";
	} else {
		cout << "Not same\n";
	}
	
	ds.unionBySize(3, 7);
	
	if (ds.findParent(3) == ds.findParent(7)) {
		cout << "Same\n";
	} else {
		cout << "Not same\n";
	}
	
	return 0;
}
```

### Time Complexity

```findParent()```: $O(4\alpha)$
```union()```: $O(4\alpha)$





# References