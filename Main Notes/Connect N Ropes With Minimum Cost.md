03-02-2026  15:15

Status: #Revision

Tags: [[Tags/DSA|DSA]] [[Heaps]]

# Connect N Ropes With Minimum Cost

https://www.naukri.com/code360/problems/connect-n-ropes-with-minimum-cost_630476

- Create a min heap from all the ropes.
- While the size of the min heap is > 1.
- Get 2 smallest rope, connect them and add the cost to the min heap.
- Maintain a total cost variable.

```cpp
long long connectRopes(int* arr, int n)
{
    if(n == 1) {
        return 0;
    }
	
    priority_queue<int, vector<int>, greater<int>> pq;
	
    for(int i = 0; i < n; i++) {
        pq.push(arr[i]);
    }
	
    int total = 0;
	
    while(pq.size() != 1) {
        int first = pq.top();
        pq.pop();
		
        int second = pq.top();
        pq.pop();
		
        total += first + second;
		
        pq.push(first + second);
    }
	
    return total;
}
```

| **Time Complexity** | **Space Complexity** |
| :-----------------: | :------------------: |
|    $O(N \log N)$    |        $O(N)$        |





# References