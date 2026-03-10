09-03-2026  14:51

Status: #Revision

Tags: [[Tags/DSA|DSA]] [[Dynamic Programming]]

# Target Sum

https://leetcode.com/problems/target-sum/

- We need to create 2 partitions of the array such that, $S1 - S2 = \text{Target}$.
- Meaning add the elements that need to be additioned to S1 and elements that need to be subtracted in S2 and the subtraction of S1 and S2 needs to be the target.
- The problem will become same as count partitions with difference equals to target.

```cpp
class Solution {
public:
    int findWays(vector<int>& arr, int k) {
        int n = arr.size();
        vector<int> prev(k + 1, 0);
		
        prev[0] = 1;
		
        for (int i = 0; i < n; i++) {
            vector<int> tmp(k + 1, 0);
			
            for (int j = 0; j <= k; j++) {
                int notPick = prev[j];
                int pick = 0;
				
                if (arr[i] <= j) {
                    pick = prev[j - arr[i]];
                }
				
                tmp[j] = pick + notPick;
            }
			
            prev = tmp;
        }
		
        return prev[k];
    }
	
    int countPartitions(int n, int d, vector<int>& arr) {
        int total = 0;
        for (int i = 0; i < n; i++) {
            total += arr[i];
        }
		
        if ((total - d) & 1 || total - d < 0) {
            return 0;
        }
		
        return findWays(arr, (total - d) / 2);
    }
	
    int findTargetSumWays(vector<int>& nums, int target) {
        return countPartitions(nums.size(), target, nums);
    }
};
```

| **Time Complexity** | **Space Complexity** |
| :-----------------: | :------------------: |
|      $O(N*K)$       |        $O(K)$        |
$K = (\text{Total} - \text{Target}) / 2$





# References
[[Count Partitions With Given Difference]]]