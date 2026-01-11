02-08-2025  14:52

Status: #Revision-03

Tags: [[Tags/DSA]] [[Stack]]

# Next Greater Element I

https://leetcode.com/problems/next-greater-element-i/description/

## Brute Force

- For every element in the nums1, find the same element in nums2.
- If found, find the next greater element, and add it to ans.

```cpp
class Solution {
public:
    vector<int> nextGreaterElement(vector<int>& nums1, vector<int>& nums2) {
        vector<int> ans(nums1.size(), -1);
		
        for(int i = 0; i < nums1.size(); i++) {
            for(int j = 0; j < nums2.size(); j++) {
                if(nums1[i] == nums2[j]) {
                    for(int k = j + 1; k < nums2.size(); k++) {
                        if(nums2[k] > nums1[i]) {
                            ans[i] = nums2[k];
                            break;
                        }
	                }
					
                    break;
                }
            }
        }
		
        return ans;
    }
};
```

| **Time Complexity** | **Space Complexity** |
| :-----------------: | :------------------: |
|    $O(N1 * N2)$     |       $O(N1)$        |


## Optimal

- Start iterating from the back.
- Make an monotonic stack of decreasing element.
- The stack top will be the next greater element of the element.


```cpp
class Solution {
public:
    vector<int> nextGreaterElement(vector<int>& nums1, vector<int>& nums2) {
        stack<int> st;
        unordered_map<int, int> mp;
		
        for(int i = (nums2.size() - 1); i >= 0; i--) {
            while(!st.empty() && st.top() <= nums2[i]) {
                st.pop();
            }
			
            if(st.empty()) {
                mp[nums2[i]] = -1;
            } else {
                mp[nums2[i]] = st.top();
            }
			
            st.push(nums2[i]);
        }
		
        vector<int> ans;
		
        for(int i = 0; i < nums1.size(); i++) {
            ans.push_back(mp[nums1[i]]);
        }
		
        return ans;
    }
};
```

|   **Time Complexity**   |  **Space Complexity**   |
| :---------------------: | :---------------------: |
| $O(N2) + O(N2) + O(N1)$ | $O(N2) + O(N2) + O(N1)$ |



# References

[[Monotonic Stack]]