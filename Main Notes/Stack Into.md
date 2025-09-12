29-07-2025  17:42

Status: #Revision-02 

Tags: [[Tags/DSA]] [[Stack]]

# Stack Into

## Stack (LIFO)
#### -> Last in First out

![[Pasted image 20250729174416.png]]

Example,
```cpp
stack<int> st;

st.push(3);
st.pop();
st.top();
st.size();
```

#### Implementation in Arrays
```cpp
#include <bits/stdc++.h>

class Stack {
  public:
  int top = -1;  
  int stack[10];

  // O(1)
  void push(int value) {
    if(top + 1 >= 10) {
      return;
    }
	
    stack[++top] = value;
  }

  // O(1)
  void pop() {
    if(top == -1) {
      return;
    }
	
    stack[top--] = 0;
  }

  // O(1)
  int s_top() {
    if(top == -1) {
      return 0;
    }

    return stack[top];
  }
  
  // O(1)
  int size() {
    return top + 1;
  }
};

int main(void) {
  Stack *st = new Stack();

  std::cout << st->s_top() << std::endl;
  st->push(3);
  st->push(6);
  std::cout << st->s_top() << std::endl;
  st->pop();
  st->push(9);
  std::cout << st->size() << std::endl;
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

class Stack {
  public:
  Node* top = NULL;  
  int size = 0;
  
  // O(1)
  void push(int value) {
    Node* node = new Node(value, top);
    top = node;
    size++;
  }

  // O(1)
  void pop() {
    if(top == NULL) {
      return;
    }
    
    Node* tmp = top;
    top = top->next;
    delete tmp;
	
    size--;
  }

  // O(1)
  int s_top() {
    if(top == NULL) {
      return -1;
    }
	
    return top->value;
  }

  // O(1)
  int s_size() {
    return size;
  }
};

int main(void) {
  Stack *st = new Stack();

  std::cout << st->s_top() << std::endl;
  st->push(3);
  st->push(6);
  std::cout << st->s_top() << std::endl;
  st->pop();
  st->push(9);
  std::cout << st->s_size() << std::endl;
  std::cout << st->s_top() << std::endl;
}
```


#### Implementation using Queue

https://leetcode.com/problems/implement-stack-using-queues/description/

##### Push:
- Time Complexity: $O(N)$
- For pushing to the queue, get the size of the initial queue.
- Push the new element.
- Move all the prev elements after new element. 

```cpp
#include <bits/stdc++.h>

class Stack {
  public:
  std::queue<int> q;
  
  // O(N)
  void push(int value) {
    int s = q.size();
    q.push(value);
	
    for(int i = 0; i < s; i++) {
      q.push(q.front());
      q.pop();
    }
  }

  // O(1)
  void pop() {
    if(q.empty()) {
      return;
    }
	
    q.pop();
  }

  // O(1)
  int s_top() {
    if(q.empty()) {
      return -1;
    }
	
    return q.front(); 
  }

  // O(1)
  int s_size() {
    return q.size();
  }
};

int main(void) {
  Stack *st = new Stack();

  std::cout << st->s_top() << std::endl;
  st->push(3);
  st->push(6);
  std::cout << st->s_top() << std::endl;
  st->pop();
  st->push(9);
  std::cout << st->s_size() << std::endl;
  std::cout << st->s_top() << std::endl;
}
```





# References