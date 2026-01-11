09-01-2026  15:40

Status: #Revision

Tags: [[Tags/DSA|DSA]] [[Graphs]]

# Kruskal's Algorithm

https://www.naukri.com/code360/problems/minimum-spanning-tree_631769

- Sort all the edges based on the edge weight, so the shorter weighted edges will be connected first.
- Use a disjoint set data structure to connect all the edges.

```cpp
#include <bits/stdc++.h>

int findParent(int node, vector<int>& parent) {
	if(parent[node] == node) {
		return node;
	}
	
	parent[node] = findParent(parent[node], parent);
	
	return parent[node];
}

bool comp(vector<int>& edge1, vector<int>& edge2) {
	return edge1[2] < edge2[2];
}

int minimumSpanningTree(vector<vector<int>>& edges, int n) {
	vector<int> parent(n);
	vector<int> size(n, 1);
	int weight = 0;
	
	// O(M log M)
	sort(edges.begin(), edges.end(), comp);
	
	for(int i = 0; i < n; i++) {
		parent[i] = i;
	}
	
	// O(M * 2 * 4 * alpha)
	for(auto& it: edges) {
		int u = it[0];
	    int v = it[1];
	    int wt = it[2];
		
		// O(v alpha)
	    int pU = findParent(u, parent);
		
		// O(v alpha)
	    int pV = findParent(v, parent);
		
	    if(pU == pV) {
		    continue;
	    }
		
	    weight += wt;
		
	    if(size[pU] < size[pV]) {
			parent[pU] = pV;
		    size[pV] += size[pU];
	    } else {
			parent[pV] = pU;
			size[pU] += size[pV];
	    }
	}
	
	return weight;
}
```

|       **Time Complexity**       | **Space Complexity** |
| :-----------------------------: | :------------------: |
| $O(M \log M + M * 2 * 4\alpha)$ |       $O(2V)$        |
M = No. of edges





# References
[[Disjoint Set]]