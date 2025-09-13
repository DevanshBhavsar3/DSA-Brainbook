14-08-2025  15:07

Status: #Revision-02 

Tags: [[Tags/DSA]] [[Stack]]

# Sliding Window Maximum

https://leetcode.com/problems/sliding-window-maximum/description/

## Brute Force

- For every element, go till i + k elements to find the maximum.

```cpp
class Solution {
public:
    vector<int> maxSlidingWindow(vector<int>& nums, int k) {
        vector<int> ans;
		
        for(int i = 0; i <= (nums.size() - k); i++) {
            int maxi = nums[i];
            for(int j = i; j < (i + k); j++) {
                maxi = max(maxi, nums[j]);
            }
			
            ans.push_back(maxi);
        }
        
        return ans;
    }
};
```

| **Time Complexity** | **Space Complexity** |
| :-----------------: | :------------------: |
|  $O(N - K) * O(K)$  |      $O(N - K)$      |


## Optimal

```
Deque:

   +
|     |  back
|     |
|     |
|     |
|  2  |
|  3  |
|  4  |
|  5  |  front
   -
```

- Create a monotonic stack of decreasing element, with a feature of accessing the first element in the stack.
- Clear all elements whose index is outside of the window.
```cpp
class Solution {
public:
    vector<int> maxSlidingWindow(vector<int>& nums, int k) {
        deque<int> dq;
        vector<int> ans;
		
        for(int i = 0; i < nums.size(); i++) {
			// Last element is outside the window length
            while(!dq.empty() && dq.front() <= i - k) {
                dq.pop_front();
            }

			// Current element is >= top
            while(!dq.empty() && nums[i] >= nums[dq.back()]) {
                dq.pop_back();
            }
			
            dq.push_back(i);

			// Only add to ans after k - 1 iterations
            if(i >= k - 1) {
                ans.push_back(nums[dq.front()]);
            }
        }
		
        return ans;
    }
};
```

| **Time Complexity** | **Space Complexity** |
| :-----------------: | :------------------: |
|       $O(2N)$       |  $O(N - K) + O(K)$   |





# References

[[Monotonic Stack]]