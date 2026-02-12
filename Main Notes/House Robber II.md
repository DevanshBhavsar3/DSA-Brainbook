12-02-2026  18:17

Status: #Revision

Tags: [[Tags/DSA|DSA]] [[Dynamic Programming]]

# House Robber II

https://leetcode.com/problems/house-robber-ii/

- To rob non-adjacent house, you can either choose first or last, not both.
- So, return the maximum amount by removing the first element and the last element.

```cpp
class Solution {
public:
    int breakInHouse(vector<int>& nums) {
        int prev = nums[0];
        int prev2 = 0;
		
        for(int i = 1; i < nums.size(); i++) {
            int tmp = prev;
            prev = max(prev, prev2 + nums[i]);
            prev2 = tmp;
        }
		
        return prev;
    }
	
    int rob(vector<int>& nums) {
        if(nums.size() == 1) {
            return nums[0];
        }
		
        int tmp = nums[0];

		// Remove first
        nums.erase(nums.begin());
        int ans1 = breakInHouse(nums);  
        nums.insert(nums.begin(), tmp);
		
        tmp = nums.back();

		// Remove last
        nums.pop_back();
        int ans2 = breakInHouse(nums);  
        nums[nums.size() - 1] = tmp;
		
        return max(ans1, ans2);
    }
};
```

| **Time Complexity** | **Space Complexity** |
| :-----------------: | :------------------: |
|       $O(2N)$       |        $O(1)$        |





# References
[[Maximum Sum Of Non Adjacent Elements]]