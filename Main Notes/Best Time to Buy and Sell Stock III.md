18-03-2026  15:29

Status: #Revision-02

Tags: [[Tags/DSA|DSA]] [[Dynamic Programming]]

# Best Time to Buy and Sell Stock III

https://leetcode.com/problems/best-time-to-buy-and-sell-stock-iii/

## Memoization

- The problem is same as previous one with just a cap parameter of 2. 
- When the cap parameter is exhausted, just return 0.

```cpp
class Solution {
public:
    int trade(int i, int canBuy, int total, vector<int>& prices, vector<vector<vector<int>>>& dp) {
        if(total == 0) {
            return 0;
        } else if(i == prices.size() - 1) {
            return canBuy ? 0 : prices[i];
        }
		
        if(dp[i][canBuy][total] != -1) {
            return dp[i][canBuy][total];
        }
		
        if(canBuy) {
            int notBuy = trade(i + 1, 1, total, prices, dp);
            int buy = trade(i + 1, 0, total, prices, dp) - prices[i];
			
            return dp[i][canBuy][total] = max(buy, notBuy);
        } else {
            int notSell = trade(i + 1, 0, total, prices, dp);
            int sell = trade(i + 1, 1, total - 1, prices, dp) + prices[i];
			
            return dp[i][canBuy][total] = max(sell, notSell);
        }
    }
	
    int maxProfit(vector<int>& prices) {
        int n = prices.size();
        vector<vector<vector<int>>> dp(n, vector<vector<int>>(2, vector<int>(3, -1)));
		
        return trade(0, 1, 2, prices, dp);
    }
};
```

| **Time Complexity** | **Space Complexity** |
| :-----------------: | :------------------: |
|     $O(N*2*3)$      |  $O(N*2*3) + O(N)$   |


## Tabulation

```cpp
class Solution {
public:
    int maxProfit(vector<int>& prices) {
        int n = prices.size();
        vector<vector<vector<int>>> dp(n + 1, vector<vector<int>>(2, vector<int>(3)));
		
        for(int i = n - 1; i >= 0; i--) {
            for(int canBuy = 0; canBuy <= 1; canBuy++) {
                for(int total = 1; total <= 2; total++) {
                    if(canBuy) {
                        int notBuy = dp[i + 1][1][total];
                        int buy = dp[i + 1][0][total] - prices[i];
						
                        dp[i][canBuy][total] = max(buy, notBuy);
                    } else {
                        int notSell = dp[i + 1][0][total];
                        int sell = dp[i + 1][1][total - 1] + prices[i];
						
                        dp[i][canBuy][total] = max(sell, notSell);
                    }
                }
            }
        }
		
        return dp[0][1][2];
    }
};
```

| **Time Complexity** | **Space Complexity** |
| :-----------------: | :------------------: |
|     $O(N*2*2)$      |      $O(N*2*3)$      |
### Space Optimization

```cpp
class Solution {
public:
    int maxProfit(vector<int>& prices) {
        int n = prices.size();
        vector<vector<int>> next(2, vector<int>(3));
		
        for(int i = n - 1; i >= 0; i--) {
            vector<vector<int>> curr(2, vector<int>(3));
			
            for(int canBuy = 0; canBuy < 2; canBuy++) {
                for(int total = 1; total <= 2; total++) {
                    if(canBuy) {
                        int notBuy = next[1][total];
                        int buy = next[0][total] - prices[i];
						
                        curr[canBuy][total] = max(buy, notBuy);
                    } else {
                        int notSell = next[0][total];
                        int sell = next[1][total - 1] + prices[i];
						
                        curr[canBuy][total] = max(sell, notSell);
                    }
                }
            }
			
            next = curr;
        }
		
        return next[1][2];
    }
};
```

| **Time Complexity** | **Space Complexity** |
| :-----------------: | :------------------: |
|     $O(N*2*2)$      |        $O(1)$        |

```cpp
class Solution {
public:
    int maxProfit(vector<int>& prices) {
        int n = prices.size();
		
        // 0      1   | 2      3
        //   Cap 1    |   Cap 2
        // NotBuy Buy | NotBuy Buy
        vector<int> next(4);
		
        for(int i = n - 1; i >= 0; i--) {
            vector<int> curr(4);
			
            curr[0] = max(next[0], prices[i]);
            curr[1] = max(next[1], next[0] - prices[i]);
			
            curr[2] = max(next[2], next[1] + prices[i]);
            curr[3] = max(next[3], next[2] - prices[i]);
			
            next = curr;
        }
		
        return next[3];
    }
};
```

| **Time Complexity** | **Space Complexity** |
| :-----------------: | :------------------: |
|       $O(N)$        |        $O(1)$        |





# References
[[Best Time to Buy and Sell Stock II]]