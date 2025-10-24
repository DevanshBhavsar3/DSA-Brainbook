25-09-2025  14:51

Status: #Revision-02  

Tags: [[Tags/DSA|DSA]] [[Greedy Algorithms]]

# Minimum Number of Platforms

https://www.naukri.com/code360/problems/minimum-number-of-platforms_799400

### Brute Force

- For each train's arrival time and departure time increase the count in the hash.
- Find the max count when increased.

```cpp
int calculateMinPatforms(int at[], int dt[], int n) {
    vector<int> arr(2359, 0);
    int total = 0;
    
    for(int i = 0; i < n; i++) {
        for(int j = at[i]; j <= dt[i]; j++) {
            arr[j]++;
            
            total = max(total, arr[j]);
        }
    }
    
    return total;
}
```

| **Time Complexity** | **Space Complexity** |
| :-----------------: | :------------------: |
|    $O(N * 2360)$    |      $O(2360)$       |


### Optimal

- Sort both arrivals and departures.
- Perform operation that occurs first as if you standing at the station and watching the events.
- If a train arrives, increase count, else decrease it.
- Find the maximum count throughout the iteration.

```cpp
int calculateMinPatforms(int at[], int dt[], int n) {
    int platforms = 0;
    
    sort(at, at + n);
    sort(dt, dt + n);
    
    int arrivalPtr = 0;
    int DepPtr = 0;
    
    int cnt = 0;
    
    while(arrivalPtr < n && DepPtr < n) {
        if(at[arrivalPtr] <= dt[DepPtr]) {
            cnt++;
            arrivalPtr++;
        } else {
            cnt--;
            DepPtr++;
        }
        
        platforms = max(platforms, cnt);
    }
    
    return platforms;
}
```

|  **Time Complexity**   | **Space Complexity** |
| :--------------------: | :------------------: |
| $O(2 * N \log N + 2N)$ |        $O(1)$        |





# References