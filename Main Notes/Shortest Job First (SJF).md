26-09-2025  15:56

Status: #Revision 

Tags: [[Tags/DSA|DSA]] [[Greedy Algorithms]]

# Shortest Job First (SJF)

https://www.geeksforgeeks.org/problems/shortest-job-first/1

- Sort the burst times.
- Add current time to waiting time.
- Accumulate the time.
- Return total waiting time / N.

```cpp
class Solution {
	public:
    long long solve(vector<int>& bt) {
        sort(bt.begin(), bt.end());
        
        int wt = 0;
        int t = 0;
        
        for(int i = 0; i < bt.size(); i++) {
            wt += t;
            t += bt[i];
        }
        
        return wt / bt.size();
    }
};
```

| **Time Complexity** | **Space Complexity** |
| :-----------------: | :------------------: |
|  $O(N + N \log N)$  |        $O(1)$        |





# References