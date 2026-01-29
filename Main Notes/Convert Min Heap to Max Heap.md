29-01-2026  17:40

Status: #Revision

Tags: [[Tags/DSA|DSA]] [[Heaps]]

# Convert Min Heap to Max Heap

https://www.geeksforgeeks.org/problems/convert-min-heap-to-max-heap-1666385109/1

- Run the heapify function of max heap for all the nodes, starting from the bottom and rightmost non-leaf node.
- Because heapify function resolves the heap property, and it assumes all the subtrees are valid heap, we start from the root of leaf nodes.

```cpp
class Solution {
  public:
    void heapify(int idx, vector<int>& arr, int N) {
        int leftChild = (2 * idx) + 1;
        int rightChild = (2 * idx) + 2;
        int greatest = idx;
        
        if(leftChild < N && arr[leftChild] > arr[greatest]) {
            greatest = leftChild;
        }
        
        if(rightChild < N && arr[rightChild] > arr[greatest]) {
            greatest = rightChild;
        }
        
        if(greatest != idx) {
            swap(arr[greatest], arr[idx]);
            heapify(greatest, arr, N);
        }
    }
	
    void convertMinToMaxHeap(vector<int> &arr, int N) {
        for(int i = (N / 2) - 1; i >= 0; i--) {
            heapify(i, arr, N);
        }
    }
};
```

| **Time Complexity** | **Space Complexity** |
| :-----------------: | :------------------: |
|   $O(N * \log N)$   |        $O(1)$        |





# References