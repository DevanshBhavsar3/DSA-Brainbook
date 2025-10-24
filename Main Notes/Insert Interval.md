27-09-2025  15:52

Status: #Revision-02  

Tags: [[Tags/DSA|DSA]] [[Greedy Algorithms]]

# Insert Interval

https://leetcode.com/problems/insert-interval/

- Add all the left intervals that don't collide with new interval.
- Merge all colliding intervals into 1 and add it to ans.
- Add all remaining intervals.

```cpp
class Solution {
public:
    vector<vector<int>> insert(vector<vector<int>>& intervals, vector<int>& newInterval) {
        vector<vector<int>> ans;
        
        int i = 0;
        
        // Left Portion
        while(i < intervals.size() && intervals[i][1] < newInterval[0]) {
            ans.push_back(intervals[i]);
            i++;
        }
        
        // Middle / Overlapping Portion
        while(i < intervals.size() && intervals[i][0] <= newInterval[1]) {
            newInterval[0] = min(newInterval[0], intervals[i][0]);
            newInterval[1] = max(newInterval[1], intervals[i][1]);
            i++;
        }
        
        ans.push_back(newInterval);
        
        // Right Portion
        while(i < intervals.size()) {
            ans.push_back(intervals[i]);
            i++;
        }
        
        return ans;
    }
};
```

| **Time Complexity** | **Space Complexity** |
| :-----------------: | :------------------: |
|       $O(N)$        |        $O(N)$        |





# References