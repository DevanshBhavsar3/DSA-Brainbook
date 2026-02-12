11-02-2026  16:31

Status: #Revision

Tags: [[Tags/DSA|DSA]] [[Dynamic Programming]]

# Frog Jump With K Distance

https://takeuforward.org/plus/dsa/problems/frog-jump-with-k-distances

## Memoization

- For every index, 
	- Find the cost to reach 0 from index - k, for all valid k.
	- Add the cost to reach that index from current index and find minimum of all.
- Maintain a dp array of size n, that will store the cost to reach 0 for particular index.

```cpp
class Solution {
public:
    int jump(int idx, vector<int>& heights, int k, vector<int>& dp) {
        if(idx == 0) {
            return 0;
        }
		
        if(dp[idx] == -1) {
            return dp[idx];
        }
		
        int mini = INT_MAX;
		
        for(int i = 1; i <= k; i++) {
            if(idx >= i) {
                mini = min(mini, jump(idx - i, heights, k, dp) + abs(heights[idx] - heights[idx - i]));
            }
        }
		
        return dp[idx] = mini;
    }
	
    int frogJump(vector<int>& heights, int k) {
        vector<int> dp(n, -1);
		
        return jump(heights.size() - 1, heights, k, dp);
    }
};
```

| **Time Complexity** | **Space Complexity** |
| :-----------------: | :------------------: |
|      $O(N*K)$       |       $O(2N)$        |


## Tabulation

- Store base cases in dp array.
- Iterate till n, and calculate the minimum cost from all the k steps.
- Return the (n - 1)th result.

```cpp
class Solution {
public:
    int frogJump(vector<int>& heights, int k) {
        vector<int> dp(n, -1);
        dp[0] = 0;
		
        for(int i = 1; i < n; i++) {
            int mini = INT_MAX;
			
            for(int j = 1; j <= k; j++) {
                if(i < j) {
                    break;
                }
				
                mini = min(mini, dp[i - j] + abs(heights[i] - heights[i - j]));
            }
			
            dp[i] = mini;
        }
		
        return dp[heights.size() - 1];
    }
};
```

| **Time Complexity** | **Space Complexity** |
| :-----------------: | :------------------: |
|      $O(N*K)$       |        $O(N)$        |





# References