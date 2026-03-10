05-03-2026  16:37

Status: #Revision

Tags: [[Tags/DSA|DSA]] [[Dynamic Programming]]

# Partition Array Into Two Arrays to Minimize Sum Difference

https://www.naukri.com/code360/problems/partition-a-set-into-two-subsets-such-that-the-difference-of-subset-sums-is-minimum_842494

- Find all the targets from 1 to K that are possible to get by creating a subset from the last index.
- This can be done by getting the last row of the populated dp matrix from subset sum equals to K problem.
- For all the possible target think each of them as a sum of elements of partition 1 and the partition 2's total will be `total - partition 1's sum`.
- Find the minimum possible absolute difference between them.

```cpp
vector<bool> subsetSumK(int k, vector<int>& nums) {
    int n = nums.size();
	
    vector<bool> prev(k + 1, false);
    prev[0] = true;
	
    if(nums[0] <= k) {
        prev[nums[0]] = true;
    }
	
    for(int i = 1; i < n; i++) {
        vector<bool> tmp(k + 1, false);
        tmp[0] = true;
		
        for(int j = 1; j <= k; j++) {
            tmp[j] = ((nums[i] <= j) ? prev[j - nums[i]] : false) || prev[j];
        }
		
        prev = tmp;
    }
	
    return prev;
}

int minSubsetSumDifference(vector<int>& arr, int n)
{
    int total = 0;
    for(int i = 0; i < n; i++) {
        total += arr[i];
    }
	
    vector<bool> subsetSums = subsetSumK(total / 2, arr);
	
    int mini = INT_MAX;
    for(int i = 0; i <= total / 2; i++) {
        if(subsetSums[i]) {
            mini = min(mini, abs(i - (total - i)));
        }
    }
	
    return mini;
}
```

| **Time Complexity** | **Space Complexity** |
| :-----------------: | :------------------: |
|      $O(N*K)$       |        $O(K)$        |
$K = \text{Total / 2}$





# References
[[Subset Sum Equal to K]]