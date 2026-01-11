04-08-2025  16:24

Status: #Revision-03

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
- When merging if the arr[i] < arr[j] then, increase the nge count to high - j + 1.

```cpp
class Solution {
  public:
    void merge(int low, int mid, int high, vector<pair<int, int>>& arr, map<int, int>& nge) {
        vector<pair<int, int>> tmp;
        int i = low;
        int j = mid + 1;
        
        while(i <= mid && j <= high) {
            if(arr[i].first < arr[j].first) {
                nge[arr[i].second] += high - j + 1;
                
                tmp.push_back(arr[i]);
                i++;
            } else {
                tmp.push_back(arr[j]);
                j++;
            }         
        }
        
        while(i <= mid) {
            tmp.push_back(arr[i]);
            i++;
        }
        
        while(j <= high) {
            tmp.push_back(arr[j]);
            j++;
        }
        
        for(int i = low; i <= high; i++) {
            arr[i] = tmp[i - low];
        }
    }
	
    void mergeSort(int low, int high, vector<pair<int, int>>& arr, map<int, int>& nge) {
        if(low >= high) {
            return;
        }
        
        int mid = low + (high - low) / 2;
        
        mergeSort(low, mid, arr, nge);
        mergeSort(mid + 1, high, arr, nge);
        
        merge(low, mid, high, arr, nge);
    }
	
    vector<int> count_NGE(vector<int> &arr, vector<int> &indices) {
        vector<pair<int, int>> copy;
        map<int, int> nge;
        
        for(int i = 0; i < arr.size(); i++) {
            copy.push_back({arr[i], i});
        }
        
        mergeSort(0, arr.size() - 1, copy, nge);
        
        vector<int> ans;
        
        for(int i = 0; i < indices.size(); i++) {
            ans.push_back(nge[indices[i]]);
        }
        
        return ans;
    }
};
```

| **Time Complexity** | **Space Complexity** |
| :-----------------: | :------------------: |
|    $O(N \log N)$    |        $O(N)$        |


# References

[[Next Greater Element I]]