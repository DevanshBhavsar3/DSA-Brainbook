17-03-2026  15:52

Status: #Revision

Tags: [[Tags/DSA|DSA]] [[Dynamic Programming]]

# Best Time to Buy and Sell Stock II

https://leetcode.com/problems/best-time-to-buy-and-sell-stock-ii/

## Memoization

- At a particular day you can either buy (If not already bought) or sell stock.
- So maintain a flag for checking, if the stock is bought or not.
- If you can buy a stock, you can either buy it or ignore it.
- If you already bought a stock, you can either sell it or ignore it.
- Memoize if you can buy or not buy on a particular index, and return the maximum.

```cpp
class Solution {
public:
    int trade(int idx, int canBuy, vector<int>& prices, vector<vector<int>>& dp) {
        if(idx == prices.size() - 1) {
            if(canBuy) {
                return 0;
            } else {
               return prices[idx]; 
            }
        }
		
        if(dp[idx][canBuy] != -1) {
            return dp[idx][canBuy];
        }
		
        if(canBuy) {
            int notBuy = trade(idx + 1, canBuy, prices, dp);
            int buy = trade(idx + 1, 0, prices, dp) - prices[idx];
			
            return dp[idx][canBuy] = max(buy, notBuy);
        } else {
            int notSell = trade(idx + 1, canBuy, prices, dp);
            int sell = trade(idx + 1, 1, prices, dp) + prices[idx];
			
            return dp[idx][canBuy] = max(sell, notSell);
        }
    }
	
    int maxProfit(vector<int>& prices) {
        int n = prices.size();
		
        vector<vector<int>> dp(n, vector<int>(2, -1));
		
        return trade(0, 1, prices, dp);
    }
};
```

| **Time Complexity** | **Space Complexity** |
| :-----------------: | :------------------: |
|      $O(N*2)$       |     $O(N*2 + N)$     |


## Tabulation

```cpp
class Solution {
public:
    int maxProfit(vector<int>& prices) {
        int n = prices.size();
		
        vector<vector<int>> dp(n, vector<int>(2));
		
        dp[n - 1][0] = prices[n - 1];
		
        for(int i = n - 2; i >= 0; i--) {
            int notSell = dp[i + 1][0];
            int sell = dp[i + 1][1] + prices[i];
			
            dp[i][0] = max(sell, notSell);
			
            int notBuy = dp[i + 1][1];
            int buy = dp[i + 1][0] - prices[i];
			
            dp[i][1] = max(buy, notBuy);
        }
		
        return dp[0][1];
    }
};
```

| **Time Complexity** | **Space Complexity** |
| :-----------------: | :------------------: |
|       $O(N)$        |       $O(N*2)$       |
### Space Optimization

```cpp
class Solution {
public:
    int maxProfit(vector<int>& prices) {
        int n = prices.size();
		
        vector<int> prev(2);
		
        for(int i = n - 1; i >= 0; i--) {
            vector<int> curr(2);
			
            curr[0] = max(prev[1] + prices[i], prev[0]);
            curr[1] = max(prev[0] - prices[i], prev[1]);
			
            prev = curr;
        }
		
        return prev[1];
    }
};
```

| **Time Complexity** | **Space Complexity** |
| :-----------------: | :------------------: |
|       $O(N)$        |        $O(1)$        |





# References