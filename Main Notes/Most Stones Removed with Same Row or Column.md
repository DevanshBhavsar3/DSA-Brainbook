10-01-2026  14:52

Status: #Revision 

Tags: [[Tags/DSA|DSA]] [[Graphs]]

# Most Stones Removed with Same Row or Column

https://leetcode.com/problems/most-stones-removed-with-same-row-or-column/

- Treat every row and col as separate nodes.
- Treat stones from same row or column as single component.
- Find no. of components in the disjoint set. 
- Return total stones - components, because there will be 1 stone left in every components.

```cpp
class DisjointSet {
    public:
    vector<int> size, parent;
	
    DisjointSet(int n) {
        size.resize(n, 1);
        parent.resize(n);
		
        for(int i = 0; i < n; i++) {
            parent[i] = i;
        }
    }
	
    int findParent(int node) {
        if(parent[node] == node) {
            return node;
        }
		
        parent[node] = findParent(parent[node]);
		
        return parent[node];
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
    int removeStones(vector<vector<int>>& stones) {
		// Find the maximum X and Y
        int lastX = 0;
        int lastY = 0;
		
        for(auto& stone: stones) {
            int x = stone[0];
            int y = stone[1];
			
            lastX = max(lastX, x);
            lastY = max(lastY, y);
        }
		
		// Total nodes will be maxX + maxY + 2
        DisjointSet ds(lastX + lastY + 2);
		
		// Make a disjoint set of unique x and y
        for(auto& stone: stones) {
            int x = stone[0];
            int y = lastX + 1 + stone[1];
			
            ds.unionBySize(x, y);
        }
		
		// Find components that have atleast 1 stone
        int components = 0;
		
        for(int i = 0; i < lastX + lastY + 2; i++) {
            if(ds.parent[i] == i && ds.size[i] > 1) {
                components++;
            }
        }
		
        return stones.size() - components;
    }
};
```

| **Time Complexity** | **Space Complexity** |
| :-----------------: | :------------------: |
|  $O(N * 4\alpha)$   |     $O(2 * 2N)$      |





# References