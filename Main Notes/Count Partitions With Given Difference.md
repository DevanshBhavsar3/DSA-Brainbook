06-03-2026  17:31

Status: #Revision

Tags: [[Tags/DSA|DSA]] [[Dynamic Programming]]

# Count Partitions With Given Difference

https://www.naukri.com/code360/problems/partitions-with-given-difference_3751628

- We want to find $S1 - S2 = D$
- Let's say,
	$(\text{Total} - S2) - S2 = D$,
	
	$\text{Total} - D = 2 * S2$,
	
	$S2 = \frac{\text{Total} - D}{2}$
	
- So we need to count subsets with sum equals to  $\frac{\text{Total} - D}{2}$.

> Also $\text{Total} - D$ should be non-negative even number for valid partitioning.

```cpp
#include <bits/stdc++.h> 

int findWays(vector<int>& arr, int k) {
	int n = arr.size();
	vector<int> prev(k + 1, 0);
	
	prev[0] = 1;
	
	for(int i = 0; i < n; i++) {
		vector<int> tmp(k + 1, 0);
		
		for(int j = 0; j <= k; j++) {
			int notPick = prev[j];
			int pick = 0;
			
			if(arr[i] <= j) {
				pick = prev[j - arr[i]];
			}
			
			tmp[j] = (pick + notPick) % ((int) 1e9 + 7);
		}
		
		prev = tmp;
	}
	
	return prev[k];
}

int countPartitions(int n, int d, vector<int> &arr) {
    int total = 0;
    for(int i = 0; i < n; i++) {
        total += arr[i];
    }
	
    if((total - d) & 1 || total - d < 0) {
        return 0;
    }
	
    return findWays(arr, (total - d) / 2);
}
```

| **Time Complexity** | **Space Complexity** |
| :-----------------: | :------------------: |
|     $O(N * K)$      |        $O(K)$        |
$K = (\text{Total} - D) / 2$





# References
[[Count Subsets with Sum K]]