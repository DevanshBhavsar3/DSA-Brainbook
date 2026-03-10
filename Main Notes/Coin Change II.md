09-03-2026  15:51

Status: #Revision

Tags: [[Tags/DSA|DSA]] [[Dynamic Programming]]

# Coin Change II

https://leetcode.com/problems/coin-change-ii/

- The problem is same as coin change.
- The only difference being we need to calculate total combinations instead of minimum no. of coins required.

```cpp
class Solution {
public:
    int change(int amount, vector<int>& coins) {
        vector<int> prev(amount + 1);
		
        prev[0] = 1;
		
        for(int i = 0; i < coins.size(); i++) {
            for(int j = 0; j <= amount; j++) {
                int notPick = prev[j];
                int pick = 0;
                
                if(coins[i] <= j) {
                    pick = prev[j - coins[i]];
                }
				
                prev[j] = (long) pick + notPick;
            }
        }
		
        return prev[amount];
    }
};
```

| **Time Complexity** | **Space Complexity** |
| :-----------------: | :------------------: |
|      $O(N*K)$       |        $O(K)$        |
$K = \text{Amount}$





# References
[[Coin Change]]