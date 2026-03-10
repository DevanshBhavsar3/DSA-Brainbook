08-03-2026  16:28

Status: #Revision

Tags: [[Tags/DSA|DSA]] [[Dynamic Programming]]

# Coin Change

https://leetcode.com/problems/coin-change/

## Memoization

- Use pick & not pick algorithm.
- If you pick a coin, you can stand at the same index because there is infinite supply of coin.
- At index 0, if the amount is divisible by element 0, return total coins required.
- Memoize the amount at every index.

```cpp
class Solution {
public:
    int change(int idx, vector<int>& coins, int amount, vector<vector<int>>& dp) {
        if(idx == 0) {
            if(amount % coins[idx] == 0) {
                return amount / coins[idx];
            }
            
            return 1e9;
        }
		
        if(dp[idx][amount] != -1) {
            return dp[idx][amount];
        }
		
        int notPick = change(idx - 1, coins, amount, dp);
		
        int pick = INT_MAX;
        if(coins[idx] <= amount) {
            pick = change(idx, coins, amount - coins[idx], dp) + 1;
        }
		
        return dp[idx][amount] = min(pick, notPick);
    }
	
    int coinChange(vector<int>& coins, int amount) {
        int n = coins.size();
        vector<vector<int>> dp(n, vector<int>(amount + 1, -1));
		
        int ans = change(n - 1, coins, amount, dp);
		
        return (ans == 1e9) ? -1 : ans;
    }
};
```

| **Time Complexity** |     **Space Complexity**      |
| :-----------------: | :---------------------------: |
|      $O(N*K)$       | $O(N*K + \text{Stack Space})$ |
$K = \text{Amount}$


## Tabulation

```cpp
class Solution {
public:
    int coinChange(vector<int>& coins, int amount) {
        int n = coins.size();
        vector<vector<int>> dp(n, vector<int>(amount + 1));
		
        for(int i = 0; i <= amount; i++) {
            if(i % coins[0] == 0) {
                dp[0][i] = i / coins[0];
            } else {
                dp[0][i] = 1e9;
            }
        }
		
        for(int i = 1; i < n; i++) {
            for(int j = 0; j <= amount; j++) {
                int notPick = dp[i - 1][j];
				
                int pick = INT_MAX;
                if(coins[i] <= j) {
                    pick = dp[i][j - coins[i]] + 1;
                }
				
                dp[i][j] = min(pick, notPick);
            }
        }
		
        return dp[n - 1][amount] == 1e9 ? -1 : dp[n - 1][amount];
    }
};
```

| **Time Complexity** | **Space Complexity** |
| :-----------------: | :------------------: |
|      $O(N*K)$       |       $O(N*K)$       |
$K = \text{Amount}$
### Space Optimization

```cpp
class Solution {
public:
    int coinChange(vector<int>& coins, int amount) {
        int n = coins.size();
        vector<int> prev(amount + 1, 1e9);
		
        for(int i = 0; i <= amount; i++) {
            if(i % coins[0] == 0) {
                prev[i] = i / coins[0];
            }
        }
		
        for(int i = 1; i < n; i++) {
            for(int j = 0; j <= amount; j++) {
                int notPick = prev[j];
				
                int pick = INT_MAX;
                if(coins[i] <= j) {
                    pick = prev[j - coins[i]] + 1;
                }
				
                prev[j] = min(pick, notPick);
            }
        }
		
        return prev[amount] == 1e9 ? -1 : prev[amount];
    }
};
```

| **Time Complexity** | **Space Complexity** |
| :-----------------: | :------------------: |
|      $O(N*K)$       |        $O(K)$        |
$K = \text{Amount}$





# References