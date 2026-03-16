12-03-2026  15:24

Status: #Revision

Tags: [[Tags/DSA|DSA]] [[Dynamic Programming]]

# Longest Common Subsequence

https://leetcode.com/problems/longest-common-subsequence/

## Memoization

- The indices `idx1` and `idx2` in the recursion will tell you the longest common subsequence in string1 from 0 to idx1 and string2 from  0 to idx2.
- If the character from both the string matches, we can reduce both index by 1 and return the lcs of the rest of the string.
	- `text1[idx1] == text2[idx2]`
- Else we need to generate all possible way to match `text1[idx1]` with `string2` and vice versa and return the maximum lcs.

```cpp
class Solution {
public:
    int find(int idx1, int idx2, string& text1, string& text2, vector<vector<int>>& dp) {
        if(idx1 < 0 || idx2 < 0) {
            return 0;
        }
		
        if(dp[idx1][idx2] != -1) {
            return dp[idx1][idx2];
        }
		
        // Match
        if(text1[idx1] == text2[idx2]) {
            return dp[idx1][idx2] = find(idx1 - 1, idx2 - 1, text1, text2, dp) + 1;
        }
        
        // Not match
        return dp[idx1][idx2] = max(
            find(idx1, idx2 - 1, text1, text2, dp),
            find(idx1 - 1, idx2, text1, text2, dp)
        );
    }
	
    int longestCommonSubsequence(string text1, string text2) {
        int n = text1.size();
        int m = text2.size();
		
        vector<vector<int>> dp(n + 1, vector<int>(m + 1, -1));
		
        return find(n - 1, m - 1, text1, text2, dp);   
    }
};
```

| **Time Complexity** | **Space Complexity** |
| :-----------------: | :------------------: |
|      $O(N*M)$       |  $O(N*M) + O(N+M)$   |


## Tabulation

```cpp
class Solution {
public:
    int longestCommonSubsequence(string text1, string text2) {
        int n = text1.size();
        int m = text2.size();
		
        vector<vector<int>> dp(n + 1, vector<int>(m + 1, -1));
		
        for(int i = 0; i <= n; i++) {
            dp[i][0] = 0;
        }
		
        for(int j = 0; j <= m; j++) {
            dp[0][j] = 0;
        }
		
        for(int i = 1; i <= n; i++) {
            for(int j = 1; j <= m; j++) {
                if(text1[i - 1] == text2[j - 1]) {
                    dp[i][j] = dp[i - 1][j - 1] + 1;
                } else {
                    dp[i][j] = max(
                        dp[i][j - 1],
                        dp[i - 1][j]
                    );
                }
            }
        }
		
        return dp[n][m];
    }
};
```

| **Time Complexity** | **Space Complexity** |
| :-----------------: | :------------------: |
|      $O(N*M)$       |       $O(N*M)$       |
### Space Optimization

```cpp
class Solution {
public:
    int longestCommonSubsequence(string text1, string text2) {
        int n = text1.size();
        int m = text2.size();
		
        vector<int> prev(m + 1);
		
        for(int i = 1; i <= n; i++) {
            vector<int> tmp(m + 1);
			
            for(int j = 1; j <= m; j++) {
                if(text1[i - 1] == text2[j - 1]) {
                    tmp[j] = prev[j - 1] + 1;
                } else {
                    tmp[j] = max(
                        tmp[j - 1],
                        prev[j]
                    );
                }
            }
			
            prev = tmp;
        }
		
        return prev[m];
    }
};
```

| **Time Complexity** | **Space Complexity** |
| :-----------------: | :------------------: |
|      $O(N*M)$       |        $O(M)$        |





# References