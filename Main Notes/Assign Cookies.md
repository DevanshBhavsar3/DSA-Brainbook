21-09-2025  14:46

Status: #Revision 

Tags: [[Tags/DSA|DSA]] [[Greedy Algorithms]]

# Assign Cookies

https://leetcode.com/problems/assign-cookies/

- Sort both the array and create 2 pointer for each.
- If current cookie size >= child, move the i pointer.

```cpp
class Solution {
public:
    int findContentChildren(vector<int>& g, vector<int>& s) {
        sort(g.begin(), g.end());
        sort(s.begin(), s.end());
        
        int i = 0;
        int j = 0;
        
        while(i < g.size() && j < s.size()) {
            if(g[i] <= s[j]) {
                i++;
            }
            
            j++;
        }
        
        return i;
    }
};
```

|          **Time Complexity**           | **Space Complexity** |
| :------------------------------------: | :------------------: |
| $O(N \log(N) + M \log(M) + min(M, N))$ |        $O(1)$        |





# References