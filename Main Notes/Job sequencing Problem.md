25-09-2025  15:38

Status: #Revision-02  

Tags: [[Tags/DSA|DSA]] [[Greedy Algorithms]]

# Job sequencing Problem

https://www.naukri.com/code360/problems/job-sequencing-problem_1169460

- Sort the jobs based on its profit.
- Create a hash array of size of maximum deadline day.
- Hash the jobs on its deadline day, if it is already taken find a previous day.

```cpp
#include <bits/stdc++.h>

bool comp(vector<int> x, vector<int> y) {
    return x[2] > y[2];
}

vector<int> jobScheduling(vector<vector<int>> &jobs)
{
	// Sort the jobs based on profit
    sort(jobs.begin(), jobs.end(), comp); // N log N
    
    // Get maximum deadline
    int maxi = INT_MIN;
    
    for(int i = 0; i < jobs.size(); i++) {
        maxi = max(maxi, jobs[i][1]);
    }
    
    // Create a hash till max deadline, and initialize it with -1
    int arr[maxi];
    
    for(int i = 0; i <= maxi; i++) {
        arr[i] = -1;
    }
    
    int jobsDone = 0;
    int totalProfit = 0;
    
    // For all the job
    for(int i = 0; i < jobs.size(); i++) {
        // Find a day to finish it
        for(int j = jobs[i][1]; j > 0; j--) {
            if(arr[j] == -1) {
                arr[j] = jobs[i][0];
                
                jobsDone++;
                totalProfit += jobs[i][2];
                break;
            }
        }
    }
    
    return {jobsDone, totalProfit};
}
```

|        **Time Complexity**        | **Space Complexity** |
| :-------------------------------: | :------------------: |
| $O(N \log N + N * max(deadline))$ |  $O(max(deadline))$  |

> The previous day search can be optimized with DSU to O(1)





# References