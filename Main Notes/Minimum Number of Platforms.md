25-09-2025  14:51

Status: #Revision 

Tags: [[Tags/DSA|DSA]] [[Greedy Algorithms]]

# Minimum Number of Platforms

https://www.naukri.com/code360/problems/minimum-number-of-platforms_799400

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