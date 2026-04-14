13-03-2026  15:21

Status: #Revision-02

Tags: [[Tags/DSA|DSA]] [[Dynamic Programming]]

# Longest Common Substring

https://www.naukri.com/code360/problems/longest-common-substring_1235207

## Tabulation

![[Pasted image 20260313155754.png]]

- For every substring of `str1` and `str2`, if the last character of both the substring matches. The longest substring till `[i][j]` will be `1 + [i - 1][j - 1]`.
- The lcs will be the maximum from the dp matrix.

```cpp
int lcs(string &str1, string &str2){
    int n = str1.size();
    int m = str2.size();
	
    vector<vector<int>> dp(n + 1, vector<int>(m + 1));
    int maxi = 0;
	
    for(int i = 1; i <= n; i++) {
        for(int j = 1; j <= m; j++) {
            if(str1[i - 1] == str2[j - 1]) {
                dp[i][j] = dp[i - 1][j - 1] + 1;
                maxi = max(maxi, dp[i][j]);
            }
        }
    }
	
    return maxi;
}
```

| **Time Complexity** | **Space Complexity** |
| :-----------------: | :------------------: |
|      $O(N*M)$       |       $O(N*M)$       |
### Space Optimization

```cpp
int lcs(string &str1, string &str2){
    int n = str1.size();
    int m = str2.size();
	
    vector<int> prev(m + 1);
    int maxi = 0;
	
    for(int i = 1; i <= n; i++) {
        vector<int> curr(m + 1);
		
        for(int j = 1; j <= m; j++) {
            if(str1[i - 1] == str2[j - 1]) {
                curr[j] = prev[j - 1] + 1;
                maxi = max(maxi, curr[j]);
            }
        }
		
        prev = curr;
    }
	
    return maxi;
}
```

| **Time Complexity** | **Space Complexity** |
| :-----------------: | :------------------: |
|      $O(N*M)$       |        $O(M)$        |





# References