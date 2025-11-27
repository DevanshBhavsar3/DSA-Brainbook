27-11-2025  15:40

Status: #Revision 

Tags: [[Tags/DSA|DSA]] [[Graphs]]

# Surrounded Regions

https://leetcode.com/problems/surrounded-regions/

- For the O's to be not surrounded there should be a single O in the group, that is at the boundary.
- Traverse from all O's that are at the boundary with DFS and mark them to not change.
- All the other O's will be surrounded, so convert them to X.

```cpp
class Solution {
public:
    // O(4 * M * N)
    void traverse(int row, int col, vector<vector<char>>& board) {
        int m = board.size();
        int n = board[0].size();
		
        board[row][col] = 'Y';
		
        int dy[] = {1, -1, 0, 0};
        int dx[] = {0, 0, -1, 1};
		
        for(int i = 0; i < 4; i++) {
            int nrow = row + dy[i];
            int ncol = col + dx[i];
			
            if(nrow >= 0 && nrow < m && ncol >= 0 && ncol < n && board[nrow][ncol] == 'O') {
                traverse(nrow, ncol, board);
            }
        }
    }
	
    void solve(vector<vector<char>>& board) {
        int m = board.size();
        int n = board[0].size();
		
        // O(M)
        for(int i = 0; i < m; i++) {
            if(board[i][0] == 'O') {
                traverse(i, 0, board);
            }
			
            if(board[i][n - 1] == 'O') {
                traverse(i, n - 1, board);
            }
        }
		
        // O(N)
        for(int i = 0; i < n; i++) {
            if(board[0][i] == 'O') {
                traverse(0, i, board);
            }
			
            if(board[m - 1][i] == 'O') {
                traverse(m - 1, i, board);
            }
        }
		
        // O(M * N)
        for(int i = 0; i < m; i++) {
            for(int j = 0; j < n; j++) {
                if(board[i][j] == 'O') {
                    board[i][j] = 'X';
                } else if(board[i][j] == 'Y') {
                    board[i][j] = 'O';
                }
            }
        }
    }
};
```

|          **Time Complexity**          | **Space Complexity** |
| :-----------------------------------: | :------------------: |
| $O(N) + O(M) + O(M*N) + O(4 * M * N)$ |       $O(M*N)$       |





# References