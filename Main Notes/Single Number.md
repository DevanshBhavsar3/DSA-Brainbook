24-07-2025  13:12

Status: #Revision-02  

Tags: [[Tags/DSA]] [[Bit Manipulation]]

# Single Number

https://leetcode.com/problems/single-number/

## Brute Force

- Create a map.
- Insert every element into the map.
- Check which element appears only once.

```cpp
map<int, int> mp;

for(int i = 0; i < n; i++) {
	mp[nums[i]]++;
}

for(auto it: mp) {
	if(it.second == 1) {
		return it.first;	
	}
}
```

| **Time Complexity**                                                                                                         | **Space Complexity** |
| --------------------------------------------------------------------------------------------------------------------------- | -------------------- |
| $O(n \log m) + O(m)$ (Map), <br>$O(n+m)$ (Unordered map)<br>$O(n * m) + O(m)$ (Worst Case)<br><br>m = total elements in map | $O(m)$               |





## Optimal

- Perform bit-wise xor of all the element in the array.
- The result will be the ans.

```cpp
class Solution {
public:
    int singleNumber(vector<int>& nums) {
        int xr = 0;

        for(int i = 0; i < nums.size(); i++) {
            xr ^= nums[i];
        }

        return xr;
    }
};
```

| **Time Complexity** | **Space Complexity** |
| ------------------- | -------------------- |
| $O(n)$              | $O(1)$               |







# References