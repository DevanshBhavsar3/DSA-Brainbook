05-02-2026  17:08

Status: #Revision 

Tags: [[Tags/DSA|DSA]] [[Heaps]]

# Top K Frequent Elements

https://leetcode.com/problems/top-k-frequent-elements/

## Better

- First count the frequency of every element in the array.
- Create a min heap from the frequency. Whenever the min heap's size becomes > k, remove the least frequency element (root).
- Create ans array from the heap.

```cpp
class Solution {
public:
    vector<int> topKFrequent(vector<int>& nums, int k) {
        unordered_map<int, int> mp;
        priority_queue<pair<int, int>, vector<pair<int, int>>, greater<pair<int, int>>> pq;
		
        for(int i = 0; i < nums.size(); i++) {
            mp[nums[i]]++;
        }
		
        for(auto it: mp) {
            pq.push({it.second, it.first});
			
            if(pq.size() > k) {
                pq.pop();
            }
        }
		
        vector<int> ans;
		
        while(!pq.empty()) {
            ans.push_back(pq.top().second);
            pq.pop();
        }
		
        return ans;
    }
};
```

| **Time Complexity** | **Space Complexity** |
| :-----------------: | :------------------: |
|  $O(N + N \log K)$  |      $O(N + K)$      |


## Optimal

- First find the frequency of every element.
- Create an array which stores every element at its frequency index.
- Iterate the frequency array from the back and add k elements to the ans.

```cpp
class Solution {
public:
    vector<int> topKFrequent(vector<int>& nums, int k) {
        unordered_map<int, int> mp;
		
        for(int i = 0; i < nums.size(); i++) {
            mp[nums[i]]++;
        }
		
        vector<vector<int>> freq(nums.size() + 1);
		
        for(auto it: mp) {
            freq[it.second].push_back(it.first);
        }
		
        vector<int> ans;
		
        for(int i = freq.size() - 1; i >= 0; i--) {
            for(int j = 0; j < freq[i].size(); j++) {
                ans.push_back(freq[i][j]);
				
                if(ans.size() == k) {
                    return ans;
                }
            }
        }
		
        return ans;
    }
};
```

| **Time Complexity** | **Space Complexity** |
| :-----------------: | :------------------: |
|       $O(4N)$       |       $O(3N)$        |





# References