24-09-2025  14:50

Status: #Revision 

Tags: [[Tags/DSA|DSA]] [[Greedy Algorithms]]

# N meetings in 1 room

https://www.geeksforgeeks.org/problems/n-meetings-in-one-room-1587115620/1

- Sort the meetings based on its ending times.
- Count all the meetings that can be possible. ( start time > last meeting's end time )

```cpp
class Solution {
  public:
    static bool comp(pair<int, int> x, pair<int, int> y) {
        return x.second < y.second;
    }
    
    int maxMeetings(vector<int>& start, vector<int>& end) {
        int n = start.size();
        
        vector<pair<int, int>> sortedMeetings;
        
        for(int i = 0; i < n; i++) {
            sortedMeetings.push_back({start[i], end[i]});
        }
        
        sort(sortedMeetings.begin(), sortedMeetings.end(), comp);
        
        int cnt = 1;
        int lastMeetingEndTime = sortedMeetings[0].second;
        
        for(int i = 1; i < n; i++) {
            if(sortedMeetings[i].first > lastMeetingEndTime) {
                cnt++;
                lastMeetingEndTime = sortedMeetings[i].second;
            }
        }
        
        return cnt;
    }
};
```

| **Time Complexity** | **Space Complexity** |
| :-----------------: | :------------------: |
| $O(2N + N \log N)$  |       $O(2N)$        |





# References