25-07-2025  15:22

Status: #Revision-03 

Tags: [[Tags/DSA]] [[Bit Manipulation]]

# L to R XOR

https://www.naukri.com/code360/problems/l-to-r-xor_8160412

## Brute Force

- Loop from L to R while finding xor.

```cpp
int xr = 0;

for(int i = L; i <= R; i++) {
	xr ^= i;
}

return xr;
```


| **Time Complexity** | **Space Complexity** |
| ------------------- | -------------------- |
| $O(R - L + 1)$      | $O(1)$               |


## Optimal ( 1 to N )

```
N = 1     ans = 1
N = 2     ans = 3
N = 3     ans = 0
N = 4     ans = 4

N = 5     ans = 1
N = 6     ans = 7
N = 7     ans = 0
N = 8     ans = 8
```


```cpp
if(n % 4 == 1) {
	return 1;
} else if(n % 4 == 2) {
	return n + 1;
} else if(n % 4 == 3) {
	return 0;
}

return n;
```


| **Time Complexity** | **Space Complexity** |
| ------------------- | -------------------- |
| $O(1)$              | $O(1)$               |


## Optimal ( L to R )

```
L = 3
R = 5

= (1 ^ 2) ^ (1 ^ 2 ^ 3 ^ 4 ^ 5)
= (3 ^ 4 ^ 5)
```


```cpp
int get1toN(int n) {
    if(n % 4 == 1) {
        return 1;
    } else if(n % 4 == 2) {
        return n + 1;
    } else if(n % 4 == 3) {
        return 0;
    }
	
    return n;
}

int findXOR(int L, int R){
    return get1toN(L - 1) ^ get1toN(R);
}
```


| **Time Complexity** | **Space Complexity** |
| ------------------- | -------------------- |
| $O(1)$              | $O(1)$               |


# References