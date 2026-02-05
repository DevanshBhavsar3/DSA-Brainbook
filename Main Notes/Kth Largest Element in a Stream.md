04-02-2026  16:51

Status: #Revision 

Tags: [[Tags/DSA|DSA]] [[Heaps]]

# Kth Largest Element in a Stream

https://leetcode.com/problems/kth-largest-element-in-a-stream/

- Create a min heap and fill it with initial nums.
- If the size of the min heap is > k, remove the smallest element.
- For every add function call, do the same.

```cpp
class KthLargest {
    priority_queue<int, vector<int>, greater<int>> pq;
    int k;
	
public:
	
    KthLargest(int k, vector<int>& nums) {
        this->k = k;
		
        for(int num: nums) {
            pq.push(num);
			
            if(pq.size() > k) {
                pq.pop();
            }
        }    
    }
	
	// O(log K)
    int add(int val) {
        pq.push(val);
        
        if(pq.size() > k) {
            pq.pop();
        }
		
        return pq.top();
    }
};
```

| **Time Complexity** | **Space Complexity** |
| :-----------------: | :------------------: |
|     $O(\log K)$     |        $O(K)$        |





# References