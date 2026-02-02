02-02-2026  15:05

Status: #Revision

Tags: [[Tags/DSA|DSA]] [[Heaps]]

# Task Scheduler

https://leetcode.com/problems/task-scheduler/

## Brute Force

- Count the frequency of every task and add it to the max heap.
- While the max heap is not empty, perform N cycle operations.
- Which will pop the element from the max heap reduce the count by 1, and add it again to the max heap if it is non zero.
- Add any ideal time to the total if it exists.

```cpp
class Solution {
public:
    int leastInterval(vector<char>& tasks, int n) {
        unordered_map<char, int> mp;
        for(char& ch: tasks) {
            mp[ch]++;
        }
		
        priority_queue<int> pq;
        for(auto& it: mp) {
            pq.push(it.second);
        }
		
        int total = 0;
		
        while(!pq.empty()) {
            int i = 0;
            vector<int> tmp;
			
            while(i <= n && !pq.empty()) {
                int cnt = pq.top();
                pq.pop();
				
                cnt--;
				
                if(cnt > 0) {
                    tmp.push_back(cnt);
                }
				
                total++;
                i++;
            }
			
            for(int& it: tmp) {
                pq.push(it);
            }
			
            if(pq.empty()) {
                break;
            }
			
            total += n + 1 - i;
        }
		
        return total;
    }
};
```

| **Time Complexity** | **Space Complexity** |
| :-----------------: | :------------------: |
|    $O(N \log K)$    |       $O(2K)$        |
k = Unique tasks


## Optimal

- Find the maximum frequency task.
- The total time required to complete all the task will be,
	maximum frequency task - 1 (The last task) * cycle length (n + 1).
- For every task if its frequency is equal to maximum, increase time by 1.
- Return the maximum of task size and calculated time.

> The remaining task are filled in the cycle length. If the remaining task can't be filled there, the total will always be < than tasks size.

```cpp
class Solution {
public:
    int leastInterval(vector<char>& tasks, int n) {
        map<char, int> mp;
        int maxi = INT_MIN;
		
        for(auto task: tasks) {
            mp[task]++;
            maxi = max(maxi, mp[task]);
        }
		
        int total = (maxi - 1) * (n + 1);
        for(auto it: mp) {
            if(it.second == maxi) {
                total++;
            }
        }
		
        return max((int) tasks.size(), total);
    }
};
```

| **Time Complexity** | **Space Complexity** |
| :-----------------: | :------------------: |
|     $O(N + K)$      |        $O(K)$        |
k = Unique tasks





# References