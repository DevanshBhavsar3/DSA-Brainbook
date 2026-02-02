31-01-2026  15:51

Status: #Revision

Tags: [[Tags/DSA|DSA]] [[Heaps]]

# Kth Smallest Element in an Array

https://www.geeksforgeeks.org/problems/kth-smallest-element5635/1

## Brute Force

- First create a max heap of k element from the array.
- For every index after k, if the element is < than the max heap's root, remove the root and add that element into the max heap.
- The root of the max heap will have the Kth Smallest Element.

```cpp
class Solution {
  public:
    int kthSmallest(vector<int> &arr, int k) {
        priority_queue<int> pq;
        
        for(int i = 0; i < arr.size(); i++) {
            if(i < k) {
                pq.push(arr[i]);
            } else if(arr[i] < pq.top()) {
                pq.pop();
                pq.push(arr[i]);
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
- Swap every > element to the left side.
- Swap the pivot with the last > element.
- If the pivot index is Kth smallest element index, return the ans.
- Else if the pivot index is < Kth smallest element index, perform the steps again on the right partition.
- Else perform on left partition.

```cpp
class Solution {
  public:
    int solve(int low, int high, vector<int> arr, int k) {
        if(low < 0 || high >= arr.size()) {
            return -1;
        }
        
        int idx = low + 1;
        
        for(int i = low + 1; i <= high; i++) {
            if(arr[i] > arr[low]) {
                swap(arr[i], arr[idx]);
                idx++;
            }
        }
        
        idx--;
        swap(arr[low], arr[idx]);
        
        if(idx == arr.size() - k) {
            return arr[idx];
        } else if(idx < arr.size() - k) {
            return solve(idx + 1, high, arr, k);
        } else {
            return solve(low, idx - 1, arr, k);
        }
    }
    
    int kthSmallest(vector<int> &arr, int k) {
        return solve(0, arr.size() - 1, arr, k);
    }
};
```

|   **Time Complexity**   | **Space Complexity** |
| :---------------------: | :------------------: |
| $\theta(N)$<br>$O(N^2)$ |        $O(1)$        |





# References