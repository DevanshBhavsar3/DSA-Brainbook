03-03-2026  17:09

Status: #Revision

Tags: [[Tags/DSA|DSA]] [[Dynamic Programming]]

# Chocolate Pickup

https://www.naukri.com/code360/problems/ninja-and-his-friends_3125885

## Memoization

- Calculate the maximum path sum by moving both Alice & Bob together.
- If any of the pointer goes out of bound, return INT_MIN.
- If at the last row, return the chocolates collected by both Alice and Bob (check for common cell).
- For every possible moves for Alice, move Bob to every possible cell.
- Memoize the maximum path sum by a particular row and the Alice and Bob's cell index.

```cpp
#include <bits/stdc++.h> 

int pickup(int row, int aliceCol, int bobCol, int r, int c, vector<vector<int>>& grid, vector<vector<vector<int>>>& dp) {
    if(aliceCol < 0 || aliceCol >= c || bobCol < 0 || bobCol >= c) {
        return INT_MIN;
    } else if(row == r - 1) {
        if(aliceCol == bobCol) {
            return grid[row][aliceCol];    
        }
		
        return grid[row][aliceCol] + grid[row][bobCol];
    }
	
    if(dp[row][aliceCol][bobCol] != -1) {
        return dp[row][aliceCol][bobCol];
    }
     
    int maxi = INT_MIN;
	
    for(int i = -1; i <= 1; i++) {
        for(int j = -1; j <= 1; j++) {
            maxi = max(maxi, pickup(row + 1, aliceCol + i, bobCol + j, r, c, grid, dp));
        }
    }
    
    int ans = maxi + grid[row][aliceCol];
	
    if(aliceCol != bobCol) {
        ans += grid[row][bobCol];
    }
	
    return dp[row][aliceCol][bobCol] = ans;
}

int maximumChocolates(int r, int c, vector<vector<int>> &grid) {
    vector<vector<vector<int>>> dp(r, vector<vector<int>>(c, vector<int>(c, -1)));
	
    return pickup(0, 0, c - 1, r, c, grid, dp);
}
```

| **Time Complexity** | **Space Complexity** |
| :-----------------: | :------------------: |
| $O(N * M * M * 9)$  |  $O(N * M * M + N)$  |


## Tabulation

```cpp
#include <bits/stdc++.h> 

int maximumChocolates(int r, int c, vector<vector<int>> &grid) {
    vector<vector<vector<int>>> dp(r, vector<vector<int>>(c, vector<int>(c, INT_MIN)));
	
    for(int i = r - 1; i >= 0; i--) {
        for(int j = 0; j < c; j++) {
            for(int k = 0; k < c; k++) {
                if(i == r - 1) {
                    if(j == k) {
                        dp[i][j][k] = grid[i][j];
                    } else {
                        dp[i][j][k] = grid[i][j] + grid[i][k];
                    }
					
                    continue;
                }
				
                int maxi = INT_MIN;
				
                for(int dA = -1; dA <= 1; dA++) {
                    for(int dB = -1; dB <= 1; dB++) {
                        if(j + dA >= 0 && j + dA < c && k + dB >= 0 && k + dB < c) {
                            maxi = max(maxi, dp[i + 1][j + dA][k + dB]);
                        }
                    }
                }
                
                int ans = maxi + grid[i][j];
				
                if(j != k) {
                    ans += grid[i][k];
                }
				
                dp[i][j][k] = ans;
            }
        }
    }
	
    return dp[0][0][c - 1];
}
```

| **Time Complexity** | **Space Complexity** |
| :-----------------: | :------------------: |
| $O(N * M * M * 9)$  |    $O(N * M * M)$    |
### Space Optimization

```cpp
#include <bits/stdc++.h> 

int maximumChocolates(int r, int c, vector<vector<int>> &grid) {
    vector<vector<int>> prev(c, vector<int>(c, INT_MIN));
	
    for(int i = r - 1; i >= 0; i--) {
        vector<vector<int>> tmp(c, vector<int>(c));
		
        for(int j = 0; j < c; j++) {
            for(int k = 0; k < c; k++) {
                if(i == r - 1) {
                    if(j == k) {
                        tmp[j][k] = grid[i][j];
                    } else {
                        tmp[j][k] = grid[i][j] + grid[i][k];
                    }
					
                    continue;
                }
				
                int maxi = INT_MIN;
				
                for(int dA = -1; dA <= 1; dA++) {
                    for(int dB = -1; dB <= 1; dB++) {
                        if(j + dA >= 0 && j + dA < c && k + dB >= 0 && k + dB < c) {
                            maxi = max(maxi, prev[j + dA][k + dB]);
                        }
                    }
                }
                
                int ans = maxi + grid[i][j];
				
                if(j != k) {
                    ans += grid[i][k];
                }
				
                tmp[j][k] = ans;
            }
        }
		
        prev = tmp;
    }
	
    return prev[0][c - 1];
}
```

| **Time Complexity** | **Space Complexity** |
| :-----------------: | :------------------: |
| $O(N * M * M * 9)$  |      $O(M * M)$      |





# References