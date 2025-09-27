21-09-2025  16:15

Status: #Revision 

Tags: [[Tags/DSA|DSA]] [[Greedy Algorithms]]

# Minimum number of coins

https://www.naukri.com/code360/problems/find-minimum-number-of-coins_975277

- Start iterating from the back of the denominators.
- While the amount can be reduced by denominator, reduce it and add it to the ans.

```cpp
vector<int> MinimumCoins(int n)
{
    vector<int> d = {1, 2, 5, 10, 20, 50, 100, 500, 1000};
    vector<int> ans;
    
    int currAmount = n;
    
    for(int i = d.size() - 1; i >= 0; i--) {
        while(currAmount >= d[i]) {
            ans.push_back(d[i]);
            currAmount -= d[i];
        }
    }
    
    return ans;
}
```

| **Time Complexity** | **Space Complexity** |
| :-----------------: | :------------------: |
|       $O(N)$        |        $O(N)$        |





# References