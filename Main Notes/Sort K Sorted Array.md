01-02-2026  15:49

Status: #Revision

Tags: [[Tags/DSA|DSA]] [[Heaps]]

# Sort K Sorted Array

https://www.naukri.com/code360/problems/nearly-sorted_982937

## Brute Force

- Perform any sorting algorithm.

| **Time Complexity** | **Space Complexity** |
| :-----------------: | :------------------: |
|    $O(N \log N)$    |        $O(N)$        |


## Optimal

- First create a min heap of k elements.
- For every index > k, push the root of the heap to the ans and pop it.
- At last push remaining element to the ans.
- Because every element is at most k steps away from its sorted index, the min heap will always have the correct value at the root after adding k elements.

```cpp
#include <bits/stdc++.h> 
vector < int > nearlySorted(vector < int > array, int n, int k) {
    vector<int> ans;
    priority_queue<int, vector<int>, greater<int>> pq;
	
    for(int i = 0; i < n; i++) {
        if(i > k) {
            ans.push_back(pq.top());
            pq.pop();
        }
		
        pq.push(array[i]);
    }
	
    while(!pq.empty()) {
        ans.push_back(pq.top());
        pq.pop();
    }
	
    return ans;
}
```

| **Time Complexity** | **Space Complexity** |
| :-----------------: | :------------------: |
|    $O(N \log K)$    |        $O(K)$        |





# References