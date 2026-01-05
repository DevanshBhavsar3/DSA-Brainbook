24-07-2025  13:29

Status: #Revision-03 

Tags: [[Tags/DSA]] [[Bit Manipulation]]

# Power Set

https://leetcode.com/problems/subsets/

```
nums = [1, 2, 3]

subsets = 8

3 2 1 -> nums
2 1 0 -> bits
-----
0 0 0
0 0 1
0 1 0
0 1 1
1 0 0
1 0 1
1 1 0
1 1 1
```


- Loop through all the possible subsets index.
- For each subset index check the set bit and add it to the pair.
- Add the pair to the ans.


```cpp
class Solution {
public:
    vector<vector<int>> subsets(vector<int>& nums) {
        int subsets = 1 << nums.size();
        vector<vector<int>> ans;
		
        for(int i = 0; i < subsets; i++) {
            vector<int> pair;
			
            for(int j = 0; j < nums.size(); j++) {
                if(i & (1 << j)) {
                    pair.push_back(nums[j]);
                }
            }
			
            ans.push_back(pair);
        }
		
        return ans;
    }
};
```


| **Time Complexity** | **Space Complexity** |
| ------------------- | -------------------- |
| $O(2^n * n)$        | $O(2^n * n)$         |





# References