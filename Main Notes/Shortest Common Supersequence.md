14-03-2026  17:23

Status: #Revision

Tags: [[Tags/DSA|DSA]] [[Dynamic Programming]]

# Shortest Common Supersequence

https://leetcode.com/problems/shortest-common-supersequence/

- Generate dp matrix from lcs problem.
- Backtrack until you reach 0, 0 cell.
- Push the characters to the end of the ans as you move index. 

```cpp
class Solution {
public:
    string shortestCommonSupersequence(string str1, string str2) {
        int n = str1.size();
        int m = str2.size();
		
        vector<vector<int>> dp(n + 1, vector<int>(m + 1));
		
        for(int i = 1; i <= n; i++) {
            for(int j = 1; j <= m; j++) {
                if(str1[i - 1] == str2[j - 1]) {
                    dp[i][j] = dp[i - 1][j - 1] + 1;
                } else {
                    dp[i][j] = max(
                        dp[i - 1][j],
                        dp[i][j - 1]
                    );
                }
            }
        }
		
        int i = n;
        int j = m;
		
        string scs = "";
		
        while(i > 0 && j > 0) {
            if(str1[i - 1] == str2[j - 1]) {
                scs = str1[i - 1] + scs;
                i--;
                j--;
            } else if(dp[i - 1][j] > dp[i][j - 1]) {
                scs = str1[i - 1] + scs;
                i--;
            } else {
                scs = str2[j - 1] + scs;
                j--;
            }
        }
		
        while(i > 0) {
            scs = str1[i - 1] + scs;
            i--;
        }
		
        while(j > 0) {
            scs = str2[j - 1] + scs;
            j--;
        }
		
        return scs;
    }
};
```

| **Time Complexity** | **Space Complexity** |
| :-----------------: | :------------------: |
| $O(N*M) + O(N + M)$ |      $O(N * M)$      |





# References
[[Longest Common Subsequence]]