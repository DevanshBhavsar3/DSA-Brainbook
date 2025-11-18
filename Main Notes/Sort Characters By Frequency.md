14-11-2025  14:49

Status: #Revision 

Tags: [[Tags/DSA|DSA]] [[Strings]]

# Sort Characters By Frequency

https://leetcode.com/problems/sort-characters-by-frequency/

- Hash frequency of every chars in string.
- Add the frequency, char pair to priority queue.
- While the queue is not empty, add the top char for its frequency times to the ans.

```cpp
class Solution {
public:
    string frequencySort(string s) {
        map<char, int> mp;
        priority_queue<pair<int, char>> pq;
		
        for(int i = 0; i < s.size(); i++) {
            mp[s[i]]++;
        }
		
        for(auto it: mp) {
            pq.push({it.second, it.first});
        }
		
        string ans = "";
		
        while(!pq.empty()) {
            pair<int, char> ch = pq.top();
            pq.pop();
			
            for(int i = 0; i < ch.first; i++) {
                ans.push_back(ch.second);
            }
        }
		
        return ans;
    }
};
```

|        **Time Complexity**         | **Space Complexity** |
| :--------------------------------: | :------------------: |
| $O(N \log K)$, K = Unique elements |        $O(K)$        |





# References