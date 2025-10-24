27-09-2025  16:54

Status: #Revision-02  

Tags: [[Tags/DSA|DSA]] [[Greedy Algorithms]]

# Non-overlapping Intervals

https://leetcode.com/problems/non-overlapping-intervals/

- Sort the intervals based on its ending time.
- Count how many intervals are non-overlapping ( start time >= last end time ).
- Return total intervals - non-overlapping intervals.

```cpp
class Solution {
public:
    static bool comp(vector<int> x, vector<int> y) {
        return x[1] < y[1];
    }
    
    int eraseOverlapIntervals(vector<vector<int>>& intervals) {
        sort(intervals.begin(), intervals.end(), comp);
        
        int cnt = 1;
        int lastEnd = intervals[0][1];
        
        for(int i = 1; i < intervals.size(); i++) {
            if(intervals[i][0] >= lastEnd) {
                cnt++;
                lastEnd = intervals[i][1];
            }
        }
        
        return intervals.size() - cnt;
    }
};
```

| **Time Complexity** | **Space Complexity** |
| :-----------------: | :------------------: |
|  $O(N \log N + N)$  |        $O(1)$        |





# References

[[N meetings in 1 room]]