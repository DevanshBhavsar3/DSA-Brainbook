02-02-2026  16:40

Status: #Revision 

Tags: [[Tags/DSA|DSA]] [[Heaps]]

# Hand of Straights

https://leetcode.com/problems/hand-of-straights/

- If the array is not perfectly dividable by k, return false.
- Count the frequency of every element and store it into the map.
- Start iterating over the map and check if you can form a group with the smallest value being the current element.
- To form a valid group, all the consecutive K elements should have >= frequency count.

```cpp
class Solution {
public:
    bool isNStraightHand(vector<int>& hand, int groupSize) {
        if(hand.size() % groupSize != 0) {
            return false;
        }
		
        map<int, int> mp;
        for(int i = 0; i < hand.size(); i++) {
            mp[hand[i]]++;
        }
		
        auto it = mp.begin();
		
        while(it != mp.end()) {
            if(it->second == 0) {
                it++;
                continue;
            }
			
            int el = it->first;
            int cnt = it->second;
            
            for(int i = 0; i < groupSize; i++) {
                if(mp[el + i] < cnt) {
                    return false;
                }
				
                mp[el + i] -= cnt;
            }
        }
		
        return true;
    }
};
```

| **Time Complexity** | **Space Complexity** |
| :-----------------: | :------------------: |
|  $O(2 * N \log N)$  |        $O(N)$        |





# References