06-08-2025  15:25

Status: #Revision-03

Tags: [[Tags/DSA]]

# Trapping Rain Water

https://leetcode.com/problems/trapping-rain-water/description/

## Brute Force

- Find the left max, and right max for every element.
- Find building that is lower than its left and right.
- Then add the min(left max, right max) - building size to ans.

```cpp
class Solution {
public:
    int trap(vector<int>& height) {
        int n = height.size();
		
        int suffixMax[n];
        suffixMax[n - 1] = height[n - 1];
		
        for(int i = 1; i < n; i++) {
            suffixMax[n - 1 - i] = max(suffixMax[n - i], height[n - 1 - i]);
        }
		
        int total = 0;
        int prefixMax = height[0];
		
        for(int i = 1; i < (n - 1); i++) {
            prefixMax = max(prefixMax, height[i]);
			
            if(height[i] < prefixMax && height[i] < suffixMax[i]) {
                total += min(prefixMax, suffixMax[i]) - height[i];
            }
        }
		
        return total;
    }
};
```

| **Time Complexity** | **Space Complexity** |
| :-----------------: | :------------------: |
|       $O(2N)$       |       $O(2N)$        |


## Optimal

- Create 2 pointers, left and right.
- If left building is < right
	- And If the building is < leftMax, then add the leftMax - height[left] to total.
	- Else update the leftMax, and update the left.
- If right building is < left 
	- And If the building is < rightMax, then add the rightMax - height[right] to total.
	- Else update the rightMax, and update the right.

```cpp
class Solution {
public:
    int trap(vector<int>& height) {
        int n = height.size();
		
        int left = 0;
        int right = n - 1;
		
        int leftMax = 0;
        int rightMax = 0;
		
        int total = 0;
		
        while(left < right) {
            if(height[left] <= height[right]) {
                if(height[left] < leftMax) {
                    total += leftMax - height[left]; 
                } else {
                    leftMax = height[left];
                }
				
                left++;
            } else {
                if(height[right] < rightMax) {
                    total += rightMax - height[right]; 
                } else {
                    rightMax = height[right];
                }
                
                right--;
            }
        }
		
        return total;
    }
};
```

| **Time Complexity** | **Space Complexity** |
| :-----------------: | :------------------: |
|       $O(N)$        |        $O(1)$        |





# References