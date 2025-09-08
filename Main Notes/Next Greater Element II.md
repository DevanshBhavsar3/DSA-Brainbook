02-08-2025  15:56

Status: #Revision 

Tags: [[Tags/DSA]] [[Stack]]

# Next Greater Element II

https://leetcode.com/problems/next-greater-element-ii/

## Brute Force

- For every elements in nums, iterate over the circular array i + n  - 1 times. 
- Add the grater element to the ans array.

```cpp
class Solution {
public:
    vector<int> nextGreaterElements(vector<int>& nums) {
        int n = nums.size();
		
        vector<int> nge(n, -1);
		
        for(int i = 0; i < n; i++) {
            for(int j = (i + 1); j <= (i + n - 1); j++) {
                int idx = j % n;
                if(nums[idx] > nums[i]) {
                    nge[i] = nums[idx];
                    break;
                }
            }
        }
		
        return nge;
    }
};
```

| **Time Complexity** | **Space Complexity** |
| :-----------------: | :------------------: |
|      $O(N^2)$       |        $O(N)$        |


## Optimal

```
nums = 1 4 12 1 11
n = 5

hypothetical nums: 1 4 12 1 11 1 4 12 1 11
n = 10
```

- Start iterating from 2 * n - 1 to 0, so the circular array is created hypothetically.
- Create a monotonic stack of decreasing element.
- If i < n, add the st.top() || -1 to the ans.
- Push the current element to stack.

```cpp
class Solution {
public:
    vector<int> nextGreaterElements(vector<int>& nums) {
        stack<int> st;
        vector<int> ans(nums.size(), -1);
		
        int n = nums.size();
		
        for(int i = (2 * n - 1); i >= 0; i--) {
            int idx = i % n;
			
            while(!st.empty() && st.top() <= nums[idx]) {
                st.pop();
            }
			
            if(i < n) {
                if(st.empty()) {
                    ans[i] = -1;
                } else {
                    ans[i] = st.top();
                }
            }
            
			
            st.push(nums[idx]);
        }
		
        return ans;
    }
};
```

| **Time Complexity** | **Space Complexity** |
| :-----------------: | :------------------: |
|   $O(2N) + O(2N)$   |    $O(2N) + O(N)$    |





# References

[[Monotonic Stack]]