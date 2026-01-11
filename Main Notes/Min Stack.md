30-07-2025  16:55

Status: #Revision-03

Tags: [[Tags/DSA]] [[Stack]]

# Min Stack

https://leetcode.com/problems/min-stack/description/

### Better

```
|        |
|(10, 10)|
|(15, 12)|
|(12, 12)|
----------
```

- Store the value and minimum element till that element in stack.

```cpp
class MinStack {
public:
    stack<pair<int, int>> st;
	
    MinStack() {
        
    }
    
    void push(int val) {
        if(st.empty()) {
            st.push({val, val});
        } else {
            st.push({val, min(val, st.top().second)});
        }
    }
    
    void pop() {
        st.pop();
    }
    
    int top() {
        return st.top().first;
    }
    
    int getMin() {
        return st.top().second;
    }
};
```

| **Time Complexity** | **Space Complexity** |
| :-----------------: | :------------------: |
|       $O(1)$        |       $O(2N)$        |


### Optimal

- Whenever the new element is less than the min element,
	- Push 2 * newValue - currentMin to stack.
	- And the store the min in currentMin.
- When popping, if the top value is < min,
	- Swap min with 2 * currentMin - top
- When returning top, if it is < min,
	- Return min.


- The check top < min works because,
```
newValue < CurrentMin

newValue - CurrentMin < 0

newValue + newValue - CurrentMin < newValue

2 * newValue - CurrentMin < newValue
-------------------------   --------
      st.top()                min
```

```cpp
class MinStack {
public:
    stack<long long> st;
    long long min;
	
    MinStack() {
        min = LONG_LONG_MAX;
    }
    
    void push(int val) {
        if(st.empty()) {
            st.push(val);
            min = val;
        } else {
            if(val < min) {
                st.push((2 * (long long) val) - min);
                min = val;
            } else {
                st.push(val);
            }
        }
    }
    
    void pop() {
        if(st.empty()) {
            return;
        }
		
		// Store the old min value
        if(st.top() < min) {
            min = (2 * min) - st.top();
        }
		
        st.pop();
    }
    
    int top() {
        if(st.top() < min) {
            return min;
        }
		
        return (int) st.top();
    }
    
    int getMin() {
        return (int) min;
    }
};
```

| **Time Complexity** | **Space Complexity** |
| :-----------------: | :------------------: |
|       $O(1)$        |        $O(N)$        |





# References