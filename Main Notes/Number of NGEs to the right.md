04-08-2025  16:24

Status: #Revision-02

Tags: [[Tags/DSA]]

# Number of NGEs to the right

https://www.geeksforgeeks.org/problems/number-of-nges-to-the-right/1

## Brute Force

- For every element, count the greater elements on its right.

```cpp
for(int i -> n) {
	for(int j = i + 1 -> n) {
		if(arr[j] > arr[i]) {
			ans[i]++;
		}
	}
}
```

| **Time Complexity** | **Space Complexity** |
| :-----------------: | :------------------: |
|      $O(N^2)$       |        $O(N)$        |
## Better

- Create a monotonic stack of increasing element.
- Push the popped off element to another stack.
- The number of NGEs to the right will be the stack size.
- Add the popped off element back to the stack.

```cpp
class Solution {
  public:
	
    vector<int> count_NGE(vector<int> &arr, vector<int> &indices) {
        vector<int> nges(arr.size(), 0);
        stack<int> st;
        stack<int> st2;
        
        for(int i = arr.size() - 1; i >= 0; i--) {
            while(!st.empty() && st.top() <= arr[i]) {
                st2.push(st.top());
                st.pop();
            }
            
            if(!st.empty()) {
                nges[i] = st.size();
            }
            
            st.push(arr[i]);
            
            while(!st2.empty()) {
                st.push(st2.top());
                st2.pop();
            }
        }
        
        vector<int> ans;
        
        for(int i = 0; i < indices.size(); i++) {
            ans.push_back(nges[indices[i]]);
        }
        
        return ans;
    }
};
```

| **Time Complexity** | **Space Complexity** |
| :-----------------: | :------------------: |
|   $O(3N) + O(Q)$    |    $O(3N) + O(Q)$    |


## Optimal

- Perform merge sort on the copy of the array of type pair<int, int>.
- When merging if the arr[i] < arr[j] then, increase the nge count to high - j.

| **Time Complexity** | **Space Complexity** |
| :-----------------: | :------------------: |
|    $O(N \log N)$    |        $O(N)$        |


# References

[[Next Greater Element I]]