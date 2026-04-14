15-03-2026  15:38

Status: #Revision-02

Tags: [[Tags/DSA|DSA]] [[Dynamic Programming]]

# Distinct Subsequences

https://leetcode.com/problems/distinct-subsequences/

## Memoization

- Use the pick & not pick algorithm to generate a subsequence from `s`.
- Only pick a character from `s`, if it matches with the `t`'s character.
- Return 1, if `t` is picked entirely.
- Memoize both string's index.

```cpp
class Solution {
public:
    int find(int i, int j, string& s, string& t, vector<vector<int>>& dp) {
        if(i < 0 || j < 0) {
            return j < 0 ? 1 : 0;
        }
		
        if(dp[i][j] != -1) {
            return dp[i][j];
        }
		
        int notPick = find(i - 1, j, s, t, dp);
        int pick = 0;
		
        if(s[i] == t[j]) {
            pick = find(i - 1, j - 1, s, t, dp);
        }
		
        return dp[i][j] = pick + notPick;
    }
	
    int numDistinct(string s, string t) {
        int n = s.size();
        int m = t.size();
		
        vector<vector<int>> dp(n, vector<int>(m, -1));
		
        return find(n - 1, m - 1, s, t, dp);
    }
};
```

| **Time Complexity** | **Space Complexity** |
| :-----------------: | :------------------: |
|      $O(N*M)$       |   $O(N*M) + O(N)$    |


## Tabulation

```cpp
class Solution {
public:
    int numDistinct(string s, string t) {
        int n = s.size();
        int m = t.size();
		
        vector<vector<int>> dp(n + 1, vector<int>(m + 1));
		
        for(int i = 0; i <= n; i++) {
            dp[i][0] = 1;
        }
		
        for(int i = 1; i <= n; i++) {
            for(int j = 1; j <= m; j++) {
                int notPick = dp[i - 1][j];
                int pick = 0;
				
                if(s[i - 1] == t[j - 1]) {
                    pick = dp[i - 1][j - 1];
                }
				
                dp[i][j] = (long) pick + notPick;
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
    int numDistinct(string s, string t) {
        int n = s.size();
        int m = t.size();
		
        vector<int> prev(m + 1);
        prev[0] = 1;
		
        for(int i = 1; i <= n; i++) {
            for(int j = m; j >= 1; j--) {
                int notPick = prev[j];
                int pick = 0;
				
                if(s[i - 1] == t[j - 1]) {
                    pick = prev[j - 1];
                }
				
                prev[j] = (long) pick + notPick;
            }
        }
		
        return prev[m];
    }
};
```

| **Time Complexity** | **Space Complexity** |
| :-----------------: | :------------------: |
|      $O(N*M)$       |        $O(M)$        |





# References