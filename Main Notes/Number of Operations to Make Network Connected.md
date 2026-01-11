09-01-2026  16:16

Status: #Revision 

Tags: [[Tags/DSA|DSA]] [[Graphs]]

# Number of Operations to Make Network Connected

https://leetcode.com/problems/number-of-operations-to-make-network-connected

- Count the no. of connected components in the graph.
- If total edges are < n - 1, you can't connect every node. So, return -1.
- Else return connected components - 1.

```cpp
class DisjointSet {
public:
    vector<int> size, parent;
	
    DisjointSet(int n) {
        size.resize(n, 1);
        parent.reserve(n);
		
        for(int i = 0; i < n; i++) {
            parent[i] = i;
        }
    }
	
    int findParent(int node) {
        if(parent[node] == node) {
            return node;
        }
		
        return parent[node] = findParent(parent[node]);
    }
	
    void unionBySize(int u, int v) {
        int pU = findParent(u);
        int pV = findParent(v);
		
        if(pU == pV) {
            return;
        }
		
        if(size[pU] < size[pV]) {
            parent[pU] = pV;
            size[pV] += size[pU];
        } else {
            parent[pV] = pU;
            size[pU] += size[pV];
        }
    } 
};

class Solution {
public:
    int makeConnected(int n, vector<vector<int>>& connections) {
        if(connections.size()  < n - 1) {
            return -1;
        }
		
        DisjointSet ds(n);
		
        for(auto& connection: connections) {
            int u = connection[0];
            int v = connection[1];
			
            ds.unionBySize(u, v);
        }
		
        int components = 0;
		
        for(int i = 0; i < n; i++) {
            if(ds.parent[i] == i) {
                components++;
            }
        }
		
        return components - 1;
    }
};
```

| **Time Complexity** | **Space Complexity** |
| :-----------------: | :------------------: |
|  $O(E * 4\alpha)$   |       $O(2V)$        |





# References