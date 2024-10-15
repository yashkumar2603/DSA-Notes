
# Implementation of Priority queues class - 
```C++
#include <vector>

class PriorityQueue {
	vector<int> pq;

	public :

	PriorityQueue() {

	}

	bool isEmpty() {
		return pq.size() == 0;
	}

	// Return the size of priorityQueue - no of elements present
	int getSize() {
		return pq.size();
	}

	int getMin() {
		if(isEmpty()) {
			return 0;		// Priority Queue is empty
		}
		return pq[0];
	}

};
```

# Insert an Element Implementation - 
```C++
#include <vector>

class PriorityQueue {
	vector<int> pq;

	public :

	PriorityQueue() {

	}

	bool isEmpty() {
		return pq.size() == 0;
	}

	// Return the size of priorityQueue - no of elements present
	int getSize() {
		return pq.size();
	}

	int getMin() {
		if(isEmpty()) {
			return 0;		// Priority Queue is empty
		}
		return pq[0];
	}

	void insert(int element) {
		pq.push_back(element);
		
		int childIndex = pq.size() - 1;

		while(childIndex > 0) {
			int parentIndex = (childIndex - 1) / 2;

			if(pq[childIndex] < pq[parentIndex]) {
				int temp = pq[childIndex];
				pq[childIndex] = pq[parentIndex];
				pq[parentIndex] = temp;
			}
			else {
				break;
			}
			childIndex = parentIndex;
		}
	}
};
```

# Remove Min. Function -
```C++
int removeMin() {
        if(isEmpty()) {
            return 0;       // Priority Queue is empty
        }
        int ans = pq[0];
        pq[0] = pq[pq.size() - 1];
        pq.pop_back();

        // down-heapify
        int parentIndex = 0;
        int leftChildIndex = 2 * parentIndex + 1;
        int rightChildIndx = 2 * parentIndex + 2;
        while(leftChildIndex < pq.size()) {
            int minIndex = parentIndex;
            if(pq[minIndex] > pq[leftChildIndex]) {
                minIndex = leftChildIndex;
            }
            
            if(rightChildIndx < pq.size() && pq[rightChildIndx] < pq[minIndex]) {
                minIndex = rightChildIndx;
            }

            if(minIndex == parentIndex) {
                break;
            }

            int temp = pq[minIndex];
            pq[minIndex] = pq[parentIndex];
            pq[parentIndex] = temp;
            parentIndex = minIndex;
            leftChildIndex = 2 * parentIndex + 1;
            rightChildIndx = 2 * parentIndex + 2;
        }
        return ans;
    }
```

# Inbuilt Priority queue - 
```C++
priority_queue<int> p;

p.push(100);
p.push(21);
p.push(7);
p.push(165);
p.push(78);
p.push(4);

cout << p.size() << endl;
cout << p.empty() << endl;
cout << p.top() << endl;

while(!p.empty()) {
	cout << p.top() << endl;
	p.pop();
```

# See Heapify method
[2.6.3 Heap - Heap Sort - Heapify - Priority Queues (youtube.com)](https://www.youtube.com/watch?v=HqPJF2L5h9U)


