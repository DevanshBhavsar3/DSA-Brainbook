16-03-2026  16:51

Status: #Revision-02

Tags: [[Tags/DSA|DSA]] [[Dynamic Programming]]

# Delete Operation for Two Strings

https://leetcode.com/problems/delete-operation-for-two-strings/

- Find the longest common subsequence of `word1` and `word2`.
- The remaining character should be removed from both strings.

```cpp
class Solution {
public:
    int findLCS(string s1, string s2) {
        int n = s1.size();
        int m = s2.size();
		
        vector<int> prev(m + 1);
		
        for(int i = 1; i <= n; i++) {
            vector<int> curr(m + 1);
			
            for(int j = 1; j <= m; j++) {
                if(s1[i - 1] == s2[j - 1]) {
                    curr[j] = prev[j - 1] + 1;
                } else {
                    curr[j] = max(
                        prev[j],
                        curr[j - 1]
                    );
                }
            }
			
            prev = curr;
        }
		
        return prev[m];
    }
	
    int minDistance(string word1, string word2) {
        int n = word1.size();
        int m = word2.size();
		
        return n + m - (findLCS(word1, word2) * 2);
    }
};
```

| **Time Complexity** | **Space Complexity** |
| :-----------------: | :------------------: |
|      $O(N*M)$       |        $O(M)$        |





# References