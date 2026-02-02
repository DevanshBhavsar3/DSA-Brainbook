01-02-2026  16:49

Status: #Revision 

Tags: [[Tags/DSA|DSA]] [[Heaps]]

# Replace Each Element Of Array With Its Corresponding Rank

https://www.naukri.com/code360/problems/replace-each-element-of-array-with-its-corresponding-rank_975384

## Brute Force

- For every element in the arrays, find distinct smaller elements.
- The rank of the element will be total smaller distinct elements + 1.

```cpp
vector<int> replaceWithRank(vector<int> &arr, int n) {
    vector<int> ranks(n);
	
    for(int i = 0; i < n; i++) {
        unordered_set<int> st;
		
        for(int j = 0; j < n; j++) {
            if(arr[j] < arr[i]) {
                st.insert(arr[j]);
            }
        }
		
        ranks[i] = st.size() + 1;
    }
	
    return ranks;
}
```

| **Time Complexity** | **Space Complexity** |
| :-----------------: | :------------------: |
|      $O(N^2)$       |        $O(N)$        |


## Optimal

- Sort the original array.
- Find the rank of every element and store them into the map.
- Create ans array with rank of every element from the map.

```cpp
vector<int> replaceWithRank(vector<int> &arr, int n) {
    unordered_map<int, int> mp;
    vector<int> ranks;
	
    ranks.insert(ranks.begin(), arr.begin(), arr.end());
    sort(ranks.begin(), ranks.end());
	
    int rank = 1;
	
    for(int i = 0; i < n; i++) {
        if(mp.find(ranks[i]) == mp.end()) {
            mp[ranks[i]] = rank;
            rank++;
        }
    }
	
    for(int i = 0; i < n; i++) {
        ranks[i] = mp[arr[i]];
    }
	
    return ranks;
}
```

| **Time Complexity** | **Space Complexity** |
| :-----------------: | :------------------: |
| $O(N \log N + 2N)$  |        $O(N)$        |





# References