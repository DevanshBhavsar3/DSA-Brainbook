04-08-2025  16:24

Status: #Pending

Tags: [[Tags/DSA]]

# Number of NGEs to the right

https://www.geeksforgeeks.org/problems/number-of-nges-to-the-right/1

## Brute Force

- For every element, count the greater elements on its right.

```cpp
for(int i -> n) {
	for(int j = i + 1 -> n) {
		if(arr[j] > arr[i]) {
			ans[i]++;
		}
	}
}
```

| **Time Complexity** | **Space Complexity** |
| :-----------------: | :------------------: |
|      $O(N^2)$       |        $O(N)$        |

## Optimal

- Perform merge sort on the copy of the array of type pair<int, int>.
- When merging if the arr[i] < arr[j] then, increase the nge count to high - j.

| **Time Complexity** | **Space Complexity** |
| :-----------------: | :------------------: |
|    $O(N \log N)$    |        $O(N)$        |


# References

[[Next Greater Element I]]