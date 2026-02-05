04-02-2026  17:21

Status: #Revision

Tags: [[Tags/DSA|DSA]] [[Heaps]]

# Maximum Sum Combination

https://www.geeksforgeeks.org/problems/maximum-sum-combination/1

## Brute Force

- For every pair from both array, put their sum into a min heap.
- If the min heap size is > k, remove the smallest int.
- Convert min heap to vector and return it.

```cpp
class Solution {
  public:
    vector<int> topKSumPairs(vector<int>& a, vector<int>& b, int k) {
        priority_queue<int, vector<int>, greater<int>> pq;
        
        for(int i = 0; i < a.size(); i++) {
            for(int j = 0; j < b.size(); j++) {
                pq.push(a[i] + b[j]);
                
                if(pq.size() > k) {
                    pq.pop();
                }
            }
        }
        
        vector<int> ans;
        
        while(!pq.empty()) {
            ans.push_back(pq.top());
            pq.pop();
        }
        
        reverse(ans.begin(), ans.end());
        
        return ans;
    }
};
```

| **Time Complexity** | **Space Complexity** |
| :-----------------: | :------------------: |
|   $O(N^2 \log K)$   |        $O(K)$        |


## Optimal

- Sort both the arrays in decreasing order. 
- Create a max heap and a set for visited pairs.
- Push the sum of the largest elements to the heap with pair index and mark the pair as visited.
- For k times, 
	- Get the top element from the heap and add the sum to the ans.
	- If not visited, push all the possible neighbor sum to the max heap and mark them as visited.

```cpp
class Solution {
  public:
    vector<int> topKSumPairs(vector<int>& a, vector<int>& b, int k) {
        sort(a.begin(), a.end(), greater<int>());
        sort(b.begin(), b.end(), greater<int>());
        
        priority_queue<pair<int, pair<int, int>>> pq;
        set<pair<int, int>> visited;
        vector<int> ans;
        
        pq.push({a[0] + b[0], {0, 0}});
        visited.insert({0, 0});
        
        int da[] = {0, 1};
        int db[] = {1, 0};
        
        while(k-- && !pq.empty()) {
            pair<int, pair<int, int>> top = pq.top();
            int sum = top.first;
            int i = top.second.first;
            int j = top.second.second;
            pq.pop();
            
            ans.push_back(sum);
            
            for(int l = 0; l < 2; l++) {
                int na = i + da[l];
                int nb = j + db[l];
                
                if(na < a.size() && nb < b.size() && !visited.count({na, nb})) {
                    pq.push({a[na] + b[nb], {na, nb}});
                    visited.insert({na, nb});
                }
            }
        }
        
        return ans;
    }
};
```

|     **Time Complexity**      | **Space Complexity** |
| :--------------------------: | :------------------: |
| $O(2 * N \log N + K \log K)$ |       $O(2K)$        |





# References