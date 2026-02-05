05-02-2026  16:04

Status: #Revision 

Tags: [[Tags/DSA|DSA]] [[Heaps]]

# Find Median from Data Stream

https://leetcode.com/problems/find-median-from-data-stream/

## Brute Force

- Maintain an array of numbers.
- For every `findMedian` function call, sort the number list and return the median based on the size of the list.

```cpp
class MedianFinder {
    vector<int> nums;
	
public:
    MedianFinder() {
        
    }
    
    void addNum(int num) {
        nums.push_back(num);
    }
	
	// O(N log N)
    double findMedian() {
        sort(nums.begin(), nums.end());
        
        int n = nums.size();
		
        if(n & 1) {
            return nums[n / 2];
        }
		
        return (nums[(n / 2) - 1] + nums[n / 2]) / 2.0;
    }
};
```

| **Time Complexity** | **Space Complexity** |
| :-----------------: | :------------------: |
|    $O(N \log N)$    |        $O(N)$        |


## Optimal

- Create two heaps to represent 2 partition of the array from the median.
- The left partition will be stored in a max heap and the right will be stored in a min heap.
- When adding new element add it to the left heap, and then add the left heap's top to the right heap. (Because we want to add the maximum element from the left to the right).
- Whenever the right heap become > left, add the smallest value back to the left heap.
- If the size of both heaps are similar, median will be the mean of both heap's root.
- Else the median will be the left heap's root.

```cpp
class MedianFinder {
public:
    priority_queue<int> left;
    priority_queue<int, vector<int>, greater<int>> right;
	
    MedianFinder() {
        
    }
	
	// O(log N)
    void addNum(int num) {
        left.push(num);
		
        right.push(left.top());
        left.pop();
        
        if(right.size() > left.size()) {
            left.push(right.top());
            right.pop();
        }
    }
    
    double findMedian() {
        if(left.size() == right.size()) {
            return (left.top() + right.top()) / 2.0;
        }
        
        return left.top();
    }
};
```

| **Time Complexity** | **Space Complexity** |
| :-----------------: | :------------------: |
|      $\log N$       |        $O(N)$        |





# References