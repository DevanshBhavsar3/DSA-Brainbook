10-08-2025  17:43

Status: #Revision-03

Tags: [[Tags/DSA]] [[Stack]]

# Largest Rectangle in Histogram

https://leetcode.com/problems/largest-rectangle-in-histogram/description/

## Brute Force

- Find the previous smaller and next smaller element for every element.
- The area will be (nse[i] - pse[i] - 1) * arr[i]. 

```cpp
class Solution {
public:
    vector<int> findPse(vector<int>& heights) {
        vector<int> pse(heights.size(), 0);
        stack<int> st;
		
        for(int i = 0; i < heights.size(); i++) {
            while(!st.empty() && heights[i] <= heights[st.top()]) {
                st.pop();
            }
			
            if(st.empty()) {
                pse[i] = -1;
            } else {
                pse[i] = st.top();
            }
			
            st.push(i);
        }
		
        return pse;
    }
	
    vector<int> findNse(vector<int>& heights) {
        vector<int> nse(heights.size(), 0);
        stack<int> st;
		
        for(int i = (heights.size() - 1); i >= 0; i--) {
            while(!st.empty() && heights[i] < heights[st.top()]) {
                st.pop();
            }
			
            if(st.empty()) {
                nse[i] = heights.size();
            } else {
                nse[i] = st.top();
            }
			
            st.push(i);
        }
		
        return nse;
    }
	
    int largestRectangleArea(vector<int>& heights) {
        int ans = 0;
		
        vector<int> pse = findPse(heights);
        vector<int> nse = findNse(heights);
		
        for(int i = 0; i < heights.size(); i++) {
            int width = nse[i] - pse[i] - 1;
            int height = heights[i];
			
            ans = max(ans, height * width);
        } 
	    
	    return ans;
    }
};
```

| **Time Complexity** | **Space Complexity** |
| :-----------------: | :------------------: |
|       $O(5N)$       |       $O(4N)$        |


## Optimal

- Find previous smaller element on the fly.
- Whenever you need to pop out from the stack,
	- The top element's nse will be i.
	- And the pse will be the element before it in the stack.
	- Find the area using heights[el] * (nse - pse - 1).
- At the end, perform the same for remaining elements in the stack.
	- Only the nse will be n.

```cpp
class Solution {
public:
    int largestRectangleArea(vector<int>& heights) {
        stack<int> st;
        int ans;
		
        for(int i = 0; i < heights.size(); i++) {
            while(!st.empty() && heights[i] < heights[st.top()]) {
                int el = st.top();
                st.pop();
				
                int pse = st.empty() ? -1 : st.top();
                int nse = i;
				
                ans = max(ans, heights[el] * (nse - pse - 1));
            }
			
            st.push(i);
        }
		
        while(!st.empty()) {
            int el = st.top();
            st.pop();
			
            int pse = st.empty() ? -1 : st.top();
            int nse = heights.size();
			
            ans = max(ans, heights[el] * (nse - pse - 1));
        }
		
        return ans;
    }
};
```

| **Time Complexity** | **Space Complexity** |
| :-----------------: | :------------------: |
|       $O(2N)$       |        $O(N)$        |





# References

[[Next Greater Element I]]