29-07-2025  18:32

Status: #Revision-02 

Tags:[[Tags/DSA]] [[Queue]]

# Queue Intro

## Queue (FIFO)
#### -> First in First out

![[Pasted image 20250729174450.png]]

Example,
```cpp
queue<int> q;
q.push(3);
q.pop();
q.size();
```

#### Implementation in Arrays

```cpp
#include <bits/stdc++.h>

class Queue {
  public:
  int start = -1;
  int end = -1;
  int size = 4;
  int cur_size = 0;
  int queue[4];

  // O(1)
  void push(int value) {
    if(cur_size >= size) {
      return;
    }
	
    if(cur_size == 0) {
      start = 0;
      end = 0;
    } else {
      end = (end + 1) % size;
    }
	
    queue[end] = value;
    cur_size++;
  }

  // O(1)
  void pop() {
    if(cur_size == 0) {
      return;
    }
	
    if(cur_size == 1) {
      start = -1;
      end = -1;
    } else {
      start = (start + 1) % size;
    }
	
    cur_size--;
  }

  // O(1)
  int top() {
    if(cur_size == 0) {
      return -1;
    }
	
    return queue[start];
  }

  // O(1)
  int q_size() {
    return cur_size;
  }
};

int main(void) {
  Queue *q = new Queue();

  q->push(3);
  q->push(6);
  q->push(9);
  std::cout << q->top() << std::endl;
  q->pop();
  q->pop();
  q->push(1);
  q->push(2);
  q->pop();
  q->pop();
  q->pop();
  std::cout << q->q_size() << std::endl;
}
```


#### Implementation in Linked List

```cpp
#include <bits/stdc++.h>

struct Node {
  int value;
  Node* next;

  Node(int value, Node* next) {
    this->value = value;
    this->next = next;
  }
};

class Queue {
  public:
  Node* start = NULL;
  Node* end = NULL;
  int size = 0;

  // O(1)
  void push(int value) {
    Node* newNode = new Node(value, NULL); 
    
    if(size == 0) {
      start = newNode;
      end = newNode;
    } else {
      end->next = newNode;
      end = end->next;
    }
	
    size++;
  }

  // O(1)
  void pop() {
    if(start == NULL) {
      return;
    }
	
    size--;
	
    Node* tmp = start;
    start = start->next;
    delete tmp;
  }

  // O(1)
  int top() {
    if(start == NULL) {
      return -1;
    }
	
    return start->value;
  }

  // O(1)
  int q_size() {
    return size;
  }
};

int main(void) {
  Queue *q = new Queue();

  q->push(3);
  q->push(6);
  q->push(9);
  std::cout << q->top() << std::endl;
  q->pop();
  q->pop();
  q->push(1);
  q->push(2);
  q->pop();
  q->pop();
  q->pop();
  std::cout << q->q_size() << std::endl;
}
```


#### Implementation using Stack

https://leetcode.com/problems/implement-queue-using-stacks/

##### Approach 1
###### Push (Expensive)
- Time Complexity: $O(2N)$
- Copy everything to stack 2.
- Add new element to stack 1.
- Copy back everything to stack 1 from stack 2.

```cpp
#include <bits/stdc++.h>

class Queue {
  public:
  std::stack<int> st1;
  std::stack<int> st2;

  // O(2N)
  void push(int value) {
    for(int i = 0; i < st1.size(); i++) {
        st2.push(st1.top());
        st1.pop();
    } 
	
    st1.push(value);
	
    for(int i = 0; i < st2.size(); i++) {
        st1.push(st2.top());
        st2.pop();
    } 
  }

  // O(1)
  void pop() {
    return st1.pop();
  }

  // O(1)
  int top() {
   return st1.top(); 
  }

  // O(1)
  int q_size() {
    return st1.size();
  }
};

int main(void) {
  Queue *q = new Queue();

  q->push(3);
  q->push(6);
  q->push(9);
  std::cout << q->top() << std::endl;
  q->pop();
  q->pop();
  q->push(1);
  q->push(2);
  q->pop();
  q->pop();
  q->pop();
  std::cout << q->q_size() << std::endl;
}
```


##### Approach 2
###### Push (Optimal)
- Time Complexity: $O(1)$
- Add it to stack 1.
###### Top (Expensive)
- Time Complexity: $O(N)$
- If the stack 2 is not empty just return the top.
- Else copy the stack 1 to stack 2.
- Return top.
###### Pop (Expensive)
- Time Complexity: $O(N)$
- If the stack 2 is not empty just return pop.
- Else copy the stack 1 to stack 2.
- Pop from stack 2.

```cpp
#include <bits/stdc++.h>

class Queue {
  public:
  std::stack<int> st1;
  std::stack<int> st2;

  // O(1)
  void push(int value) {
    st1.push(value);
  }

  // O(N)
  void pop() {
    if(!st2.empty()) {
      return st2.pop(); 
    }
	
    while(!st1.empty()) {
      st2.push(st1.top());
      st1.pop();
    }
	
    return st2.pop(); 
  }

  // O(N)
  int top() {
    if(!st2.empty()) {
      return st2.top(); 
    }
	
    while(!st1.empty()) {
      st2.push(st1.top());
      st1.pop();
    }
	
    return st2.top(); 
  }

  // O(1)
  int q_size() {
    return st1.size();
  }
};

int main(void) {
  Queue *q = new Queue();

  q->push(3);
  q->push(6);
  q->push(9);
  std::cout << q->top() << std::endl;
  q->pop();
  q->pop();
  q->push(1);
  q->push(2);
  q->pop();
  q->pop();
  q->pop();
  std::cout << q->q_size() << std::endl;
}

```





# References