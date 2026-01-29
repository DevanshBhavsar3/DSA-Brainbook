29-01-2026  16:48

Status: #Revision 

Tags: [[Tags/DSA|DSA]] [[Heaps]]

# Check array represent Heap

https://www.geeksforgeeks.org/problems/does-array-represent-heap4345/1

- For an array to be a max heap, both the child should be < the root node.
- If any of the child is > root node, return false.
- Leaf nodes always satisfies the heap conditions, so don't check for them. 

```cpp
class Solution {
  public:
    bool isMaxHeap(int arr[], int n) {
        for(int i = 0; i < n/2; i++) {
            int leftChild = (2 * i) + 1;
            int rightChild = (2 * i) + 2;
            
            if((leftChild < n && arr[leftChild] > arr[i]) ||
                (rightChild < n && arr[rightChild] > arr[i])) {
                return false;
            }
        }
        
        return true;
    }
};
```

| **Time Complexity** | **Space Complexity** |
| :-----------------: | :------------------: |
|     $O(N / 2)$      |        $O(1)$        |





# References