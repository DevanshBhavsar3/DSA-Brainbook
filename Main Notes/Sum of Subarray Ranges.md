08-08-2025  14:41

Status: #Revision-02 

Tags: [[Tags/DSA]] [[Stack]]

# Sum of Subarray Ranges

https://leetcode.com/problems/sum-of-subarray-ranges/

## Brute Force

- For every subarray, find the minimum and maximum.
- Add the maximum - minimum to the ans.

```cpp
class Solution {
public:
    long long subArrayRanges(vector<int>& nums) {
        long long ans = 0;
		
        for(int i = 0; i < nums.size(); i++) {
            int largest = nums[i];
            int smallest = nums[i];
			
            for(int j = i + 1; j < nums.size(); j++) {
                largest = max(largest, nums[j]);
                smallest = min(smallest, nums[j]);
				
                ans += largest - smallest;
            }
        }
		
        return ans;
    }
};
```

| **Time Complexity** | **Space Complexity** |
| :-----------------: | :------------------: |
|      $O(N^2)$       |        $O(1)$        |

## Optimal

```
nums = [1 2 3]

1       2     3
1 2     2 3
1 2 3

Subarray minimums:
1 2 3
1 2
1

Subarray maximums:
1 2 3
2 3
3

Final answer:
0 0 0
1 1
2
```

- Find the subarray maximums, and subarray minimums.
- Return maximum - minimums.

```cpp
class Solution {
public:
    vector<int> findPge(vector<int>& nums) {
        stack<int> st;
        vector<int> ans(nums.size(), 0);
		
        for(int i = 0; i < nums.size(); i++) {
            while(!st.empty() && nums[st.top()] < nums[i]) {
                st.pop();
            }
			
            if(st.empty()) {
                ans[i] = -1;
            } else {
                ans[i] = st.top();
            }
			
            st.push(i);
        }
		
        return ans;
    }
	
    vector<int> findNge(vector<int>& nums) {
        stack<int> st;
        vector<int> ans(nums.size(), 0);
		
        for(int i = (nums.size() - 1); i >= 0; i--) {
            while(!st.empty() && nums[st.top()] <= nums[i]) {
                st.pop();
            }
			
            if(st.empty()) {
                ans[i] = nums.size();
            } else {
                ans[i] = st.top();
            }
			
            st.push(i);
        }
		
        return ans;
    }
	
    vector<int> findPse(vector<int>& nums) {
        stack<int> st;
        vector<int> ans(nums.size(), 0);
		
        for(int i = 0; i < nums.size(); i++) {
            while(!st.empty() && nums[st.top()] > nums[i]) {
                st.pop();
            }
			
            if(st.empty()) {
                ans[i] = -1;
            } else {
                ans[i] = st.top();
            }
			
            st.push(i);
        }
		
        return ans;
    }
	
    vector<int> findNse(vector<int>& nums) {
        stack<int> st;
        vector<int> ans(nums.size(), 0);
		
        for(int i = (nums.size() - 1); i >= 0; i--) {
            while(!st.empty() && nums[st.top()] >= nums[i]) {
                st.pop();
            }
			
            if(st.empty()) {
                ans[i] = nums.size();
            } else {
                ans[i] = st.top();
            }
			
            st.push(i);
        }
		
        return ans;
    }
	
    long long findSumOfSubArrayLargest(vector<int>& nums) {
        long long total = 0;
		
        vector<int> nge = findNge(nums);
        vector<int> pge = findPge(nums);
		
        for(int i = 0; i < nums.size(); i++) {
            int left = i - pge[i];
            int right = nge[i] - i;
			
            total = total + ((long long) (left * right) * nums[i]);
        }
		
        return total;
    }
	
    long long findSumOfSubArraySmallest(vector<int>& nums) {
        long long total = 0;
		
        vector<int> nse = findNse(nums);
        vector<int> pse = findPse(nums);
		
        for(int i = 0; i < nums.size(); i++) {
            int left = i - pse[i];
            int right = nse[i] - i;
			
            total = total + ((long long) (left * right) * nums[i]);
        }
		
        return total;
    }
	
    long long subArrayRanges(vector<int>& nums) {
        long long largest = findSumOfSubArrayLargest(nums); // O(5N)
        long long smallest = findSumOfSubArraySmallest(nums); // O(5N)
		
        return largest - smallest;
    }
};
```

| **Time Complexity** | **Space Complexity** |
| :-----------------: | :------------------: |
|      $O(10N)$       |       $O(10N)$       |





# References

[[Sum of Subarray Minimums]]