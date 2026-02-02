31-01-2026  14:40

Status: #Revision 

Tags: [[Tags/DSA|DSA]] [[Heaps]]

# Kth Largest Element in an Array

https://leetcode.com/problems/kth-largest-element-in-an-array

## Brute Force

- First create a min heap of k element from the array.
- For every index after k, if the element is > than the min heap's root, remove the root and add that element into the min heap.
- The root of the min heap will have the Kth Largest Element.

```cpp
class Solution {
public:
    int findKthLargest(vector<int>& nums, int k) {
        priority_queue<int, vector<int>, greater<int>> pq;
		
        for(int i = 0; i < nums.size(); i++) {
            if(i < k) {
                pq.push(nums[i]);
            } else if(nums[i] > pq.top()) {
                pq.pop();
                pq.push(nums[i]);
            }
        }
		
        return pq.top();
    }
};
```

| **Time Complexity** | **Space Complexity** |
| :-----------------: | :------------------: |
|    $O(N \log K)$    |        $O(K)$        |


## Optimal

- Partition the array at some random pivot index.
- Swap every <= element to the left side of pivot index and > elements to the right side.
- Swap the pivot with the last <= element.
- If the pivot index is Kth largest element index, return the ans.
- Else if the pivot index is < Kth largest element index, perform the steps again on the right partition.
- Else perform on left partition.

```cpp
class Solution {
public:
    int solve(int low, int high, vector<int>& nums, int k) {
        if(low < 0 || high >= nums.size()) {
            return -1;
        }
		
        int idx = low;
		
        for(int i = low; i < high; i++) {
            if(nums[i] <= nums[high]) {
                swap(nums[i], nums[idx]);
                idx++;
            }
        }
		
        swap(nums[high], nums[idx]);
		
        if(idx == nums.size() - k) {
            return nums[idx];
        } else if(idx > nums.size() - k) {
            return solve(low, idx - 1, nums, k);
        } else {
            return solve(idx + 1, high, nums, k);
        }
    }
	
    int findKthLargest(vector<int>& nums, int k) {
        return solve(0, nums.size() - 1, nums, k);
    }
};
```

|   **Time Complexity**   | **Space Complexity** |
| :---------------------: | :------------------: |
| $\theta(N)$<br>$O(N^2)$ |        $O(1)$        |





# References