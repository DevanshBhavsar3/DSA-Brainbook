17-03-2026  15:35

Status: #Revision

Tags: [[Tags/DSA|DSA]] [[Dynamic Programming]]

# Best Time to Buy and Sell Stock

https://leetcode.com/problems/best-time-to-buy-and-sell-stock/

- To get the maximum profit you will sell on certain day, and buy the stock with minimum price from all the days before.

```cpp
class Solution {
public:
    int maxProfit(vector<int>& prices) {
        int n = prices.size();
        int mini = INT_MAX;
        int profit = 0;
		
        for(int i = 0; i < prices.size(); i++) {
            mini = min(mini, prices[i]);
			
            profit = max(profit, prices[i] - mini);
        }
		
        return profit;
    }
};
```

| **Time Complexity** | **Space Complexity** |
| :-----------------: | :------------------: |
|       $O(N)$        |        $O(1)$        |





# References