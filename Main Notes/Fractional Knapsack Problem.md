21-09-2025  15:08

Status: #Revision-02  

Tags: [[Tags/DSA|DSA]] [[Greedy Algorithms]]

# Fractional Knapsack Problem

https://www.naukri.com/code360/problems/fractional-knapsack_975286

- Sort the items based on its per weight value ( value / weight ) in decreasing order.
- Add the items if its weight <= the capacity.
- Else add the fraction of it.

```cpp
#include <bits/stdc++.h>

bool comp(pair<int, int>x, pair<int, int> y) {
    double a = x.second / (double) x.first;
    double b = y.second / (double) y.first;
    
    return a >= b;
}

double maximumValue (vector<pair<int, int>>& items, int n, int w)
{
    sort(items.begin(), items.end(), comp);
    
    int weight = w;
    double totalValue = 0;
    
    for(int i = 0; i < items.size(); i++) {
        if(items[i].first <= weight) {
            totalValue += items[i].second;
            weight -= items[i].first;
        } else {
	        // Per weight value * remaining weight
            totalValue += (items[i].second / (double) items[i].first) * weight;
            break;
        }
    }
    
    return totalValue;
}
```

| **Time Complexity**  | **Space Complexity** |
| :------------------: | :------------------: |
| $O(N \log N) + O(N)$ |        $O(1)$        |





# References