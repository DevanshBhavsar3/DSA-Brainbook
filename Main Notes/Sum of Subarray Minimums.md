06-08-2025  16:14

Status: #Revision 

Tags: [[Tags/DSA]] [[Stack]]

# Sum of Subarray Minimums

https://leetcode.com/problems/sum-of-subarray-minimums/

## Brute Force

- For every subarray, get the minimum and add it to total.

```cpp
class Solution {
public:
    int sumSubarrayMins(vector<int>& arr) {
        int n = arr.size();
        int mod = 1e9 + 7;
        int total = 0;
		
        for(int i = 0; i < n; i++) {
            int mini = arr[i];
			
            for(int j = i; j < n; j++) {
                mini = min(arr[j], mini);
				
                total = (total + mini) % mod;
            }
        }
		
        return total;
    }
};
```

| **Time Complexity** | **Space Complexity** |
| :-----------------: | :------------------: |
|      $O(N^2)$       |        $O(1)$        |


## Optimal

```
     4
  -------
1 4 6 7 3 7 8 1
        ----
		  3

4 * 3 = 12 (Total subsets in which 3 appear as minimum)

12 * 3 = 36 (Total of 3's)
```

- For, every element in the array, 
	- Find the previous smaller and next smaller element's index.
	- Count the total subsets in which it will appear as minimum. (i.e, i - pse[i] * nse[i] - i)
	- Add the element to ans multiplied by its occurrence.

```cpp
class Solution {
public:
    vector<int> findPse(vector<int>& arr) {
        stack<int> st;
        vector<int> ans(arr.size());
		
        for(int i = 0; i < arr.size(); i++) {
			// IMPORTANT: Only remove < elements from the stack not =
            while(!st.empty() && arr[i] < arr[st.top()]) {
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
	
    vector<int> findNse(vector<int>& arr) {
        stack<int> st;
        vector<int> ans(arr.size());
		
        for(int i = (arr.size() - 1); i >= 0; i--) {
            while(!st.empty() && arr[i] <= arr[st.top()]) {
                st.pop();
            }
			
            if(st.empty()) {
                ans[i] = arr.size();
            } else {
                ans[i] = st.top();
            }
			
            st.push(i);
        }
		
        return ans;
    }
	
    int sumSubarrayMins(vector<int>& arr) {
        int mod = 1e9 + 7;
		
        vector<int> nse = findNse(arr);
        vector<int> pse = findPse(arr);
		
        int total = 0;
		
        for(int i = 0; i < arr.size(); i++) {
            int left = i - pse[i];
            int right = nse[i] - i;
			
            total = (total + (((long long) left * right) * arr[i])) % mod;
        }
		
        return total;
    }
};
```

| **Time Complexity** | **Space Complexity** |
| :-----------------: | :------------------: |
|       $O(5N)$       |       $O(5N)$        |



# References

[[Next Smaller Element]]