12-12-2025  18:41

Status: #Revision 

Tags: [[Tags/DSA|DSA]] [[Graphs]]

# Number of Distinct Islands

https://www.naukri.com/code360/problems/distinct-islands_630460

- Perform BFS while storing the offset indices of all the cells of an island from the starting cell. 
- Put the offset indices in a set, return set size.

> This will work because everytime you will start with the top-left cell of an island. The similar structure will result in similar offset array.

```cpp
#include <bits/stdc++.h>

void traverse(int baseRow, int baseCol, int row, int col, int n, int m, vector<pair<int, int>>& structure, int** arr, vector<vector<int>>& visited) {   
    visited[row][col] = 1;
    structure.push_back({row - baseRow, col - baseCol});
	
    int dy[] = {-1, 1, 0, 0};
    int dx[] = {0, 0, -1, 1};
	
    for(int i = 0; i < 4; i++) {
        int nrow = row + dy[i];
        int ncol = col + dx[i];
		
        if(nrow >= 0 && nrow < n && ncol >= 0 && ncol < m && arr[nrow][ncol] && !visited[nrow][ncol]) {
            traverse(baseRow, baseCol, nrow, ncol, n, m, structure, arr, visited);
        }
    }
}

int distinctIslands(int** arr, int n, int m)
{
    set<vector<pair<int, int>>> st;
    vector<vector<int>> visited(n, vector<int>(m));
	
    for(int i = 0; i < n; i++) {
        for(int j = 0; j < m; j++) {
            if(arr[i][j] && !visited[i][j]) {
                vector<pair<int, int>> structure;
				
                traverse(i, j, i, j, n, m, structure, arr, visited);
				
                st.insert(structure);
            }
        }
    }
	
    return st.size();
}
```

|        **Time Complexity**        | **Space Complexity** |
| :-------------------------------: | :------------------: |
| $O(N*M) + O(4*N*M) + O(\log N*M)$ |     $O(3*(N*M))$     |





# References