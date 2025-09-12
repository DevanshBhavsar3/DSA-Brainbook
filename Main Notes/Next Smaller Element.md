04-08-2025  15:34

Status: #Revision-02  

Tags: [[Tags/DSA]] [[Stack]]

# Next Smaller Element

https://www.naukri.com/code360/problems/next-smaller-element_1112581

## Brute Force

- For every element, find the next smaller element in the array.

```cpp
for(int i -> n) {
	for(int j = i -> n) {
		if(arr[j] < arr[n]) {
			ans[i] = arr[j];
		}
	}
}
```

| **Time Complexity** | **Space Complexity** |
| :-----------------: | :------------------: |
|      $O(N^2)$       |        $O(N)$        |


## Optimal

- Start iterating from the back.
- Make an monotonic stack of decreasing element.
- The stack top will be the next smaller element of the element.

```cpp
#include <bits/stdc++.h>

vector<int> nextSmallerElement(vector<int> &arr, int n) {
    stack<int> st;
    vector<int> ans(n, -1);
	
    for(int i = (n - 1); i >= 0; i--) {
        while(!st.empty() && arr[i] <= st.top()) {
            st.pop();
        }
		
        if(!st.empty()) {
            ans[i] = st.top();
        }
		
        st.push(arr[i]);
    }
	
    return ans;
}
```

| **Time Complexity** | **Space Complexity** |
| :-----------------: | :------------------: |
|    $O(N) + O(N)$    |    $O(N) + O(N)$     |





# References

[[Monotonic Stack]]