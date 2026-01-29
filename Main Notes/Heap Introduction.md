28-01-2026  14:34

Status:

Tags: [[Tags/DSA|DSA]] [[Heaps]]

# Heap Introduction

## What is Priority Queue?
Priority queue is just a simple queue, but all the elements of the queue have some priority based on which they are processed instead of FIFO.


## Binary Heaps
Binary Heap is a Binary Tree that satisfies 2 conditions:
1. It is a Complete BT,
2. It is satisfies the Heap Property.

### Heap Property
There are 2 types of Heap Property:
1. Min Heap
2. Max Heap

#### 1. Min Heap
For every node in BT, the node's value is less than its children. The root value is always the minimum value in the Min Heap.

![[Pasted image 20260128150645.png]]

#### 2. Max Heap
For every node in BT, the node's value is greater than its children. The root value is always the maximum value in the Max Heap.

![[Pasted image 20260128150709.png]]


## Min Heap Implementation

```cpp
class MinHeap {
private:
	vector<int> container;
	int size;
	int capacity;
	
private:
	int parent(int node) { return (node - 1) / 2; }
	
	int leftChild(int node) { return (2 * node) + 1; }
	
	int rightChild(int node) { return (2 * node) + 2; }
	
public:
	MinHeap(int capacity) {
		container.resize(capacity);
		this->capacity = capacity;
		size = 0;
	}
	
	// O(log N)
	void insert(int value) {
		if (size == capacity) {
		    cout << "Min Heap Overflow.\n";
		    return;
		}
		
		container[size] = value;
		
		int curr = size;
		
		while (curr != 0 && container[curr] < container[parent(curr)]) {
		    swap(container[curr], container[parent(curr)]);
		    curr = parent(curr);
		}
		
		size++;
	}
	
	// O(log N)
	void heapify(int idx) {
	    int left = leftChild(idx);
	    int right = rightChild(idx);
	    int smallest = idx;
		
	    if (left < size && container[smallest] > container[left]) {
		    smallest = left;
	    }
		
		if (right < size && container[smallest] > container[right]) {
		    smallest = right;
	    }
		
	    if (smallest != idx) {
		    swap(container[idx], container[smallest]);
		    heapify(smallest);
		}
	}
	
	// O(1)
	int getMin() {
		if (size == 0) {
			return INT_MAX;
		}
		
		return container[0];
	}
	
	// O(log N)
	int extractMin() {
		if (size <= 0) {
		    return INT_MAX;
		} else if (size == 1) {
		    size = 0;
			return container[0];
		}
		
		int mini = container[0];
		
		size--;
		container[0] = container[size];
		
		heapify(0);
		
		return mini;
	}
	
	// O(log N)
	void decreaseKey(int idx, int value) {
		if (idx < 0 || idx >= size) {
		    return;
		}
		
		container[idx] = value;
		int curr = idx;
		
		while (curr != 0 && container[curr] < container[parent(curr)]) {
		    swap(container[curr], container[parent(curr)]);
		    curr = parent(curr);
		}
	}
	
	// O(2 * log N)
	void deleteElement(int idx) {
		decreaseKey(idx, INT_MIN);
		extractMin();
	}
	
	void print() {
		for (int i = 0; i < size; i++) {
			cout << container[i];
		}
	}
};
```


## Max Heap Implementation

```cpp
class MaxHeap {
private:
    vector<int> container;
    int capacity, size;
	
private:
    int parent(int idx) { return (idx - 1) / 2; }
	
    int leftChild(int idx) { return (2 * idx) + 1; }
	
    int rightChild(int idx) { return (2 * idx) + 2; }
    
public:
    MaxHeap(int capacity) {
        container.resize(capacity);
        this->capacity = capacity;
        size = 0;
    }
	
	// O(log N)
    void insert(int value) {
        if (size >= capacity) {
            cout << "Max Heap Overflow\n";
            return;
        }
		
        container[size] = value;
        int curr = size;
		
        while (curr != 0 && container[curr] > container[parent(curr)]) {
            swap(container[curr], container[parent(curr)]);
            curr = parent(curr);
        }
		
        size++;
    }
	
	// O(log N)
    void increaseKey(int idx, int value) {
        if (idx < 0 || idx >= size) {
            return;
        }
		
        container[idx] = value;
        int curr = idx;
		
        while (curr != 0 && container[curr] > container[parent(curr)]) {
            swap(container[curr], container[parent(curr)]);
            curr = parent(curr);
        }
    }
	
	// O(log N)
    void heapify(int idx) {
        int left = leftChild(idx);
        int right = rightChild(idx);
        int largest = idx;
		
        if (left < size && container[left] > container[largest]) {
            largest = left;
        }
		
        if (right < size && container[right] > container[largest]) {
            largest = right;
        }
		
        if (largest != idx) {
            swap(container[idx], container[largest]);
            heapify(largest);
        }
    }
	
	// O(log N)
    int extractMax() {
        if (size <= 0) {
            return INT_MIN;
        } else if (size == 1) {
            size = 0;
            return container[0];
        }
		
        int maxi = container[0];
		
        size--;
        container[0] = container[size];
		
        heapify(0);
		
        return maxi;
    }
	
	// O(2 * log N)
    void deleteElement(int idx) {
        increaseKey(idx, INT_MAX);
        extractMax();
    }
	
	// O(1)
    int getMax() {
        if (size <= 0) {
            return INT_MIN;
        }
		
        return container[0];
    }
	
    void print() {
        for (int i = 0; i < size; i++) {
            cout << container[i] << endl;
        }
    }
};
```





# References