<span style="background:#fdbfff">Implement a first in first out (FIFO) queue using only two stacks. The implemented queue should support all the functions of a normal queue (`push`, `peek`, `pop`, and `empty`).</span>

Implement the `MyQueue` class:

- `void push(int x)` Pushes element x to the back of the queue.
- `int pop()` Removes the element from the front of the queue and returns it.
- `int peek()` Returns the element at the front of the queue.
- `boolean empty()` Returns `true` if the queue is empty, `false` otherwise.
<font color="#b2a2c7">example-</font>
![[Pasted image 20240129151531.png]]

### Solution - 
can be done with 2 stacks, 2 vectors and also this becomes super easy once a dequeue is used.

#### The 2 Stacks approach -
```cpp
class MyQueue {
    stack<int> s0, s1;
    int front=0;
public:
    MyQueue() {
        
    }
    
    void push(int x) {
        if (s0.empty()) front=x;
        s0.push(x);
    }
    
    int pop() {// amortized O(1)
        if (s1.empty()){
            while(!s0.empty()){
                int x=s0.top();
                s0.pop();
                s1.push(x);
            }
        }
        int x=s1.top();
        s1.pop();
        return x;
    }
    
    int peek() {
        if (!s1.empty()){
            front=s1.top();
        }
        return front;
    }
    
    bool empty() {
        return s0.empty() && s1.empty();
    }
};
```

#### Using 2 Vectors - 
```cpp
class MyQueue {
    vector<int> s0, s1;
    int front=0;
public:
    MyQueue() {
        
    }
    
    void push(int x) {
        if (s0.empty()) front=x;
        s0.push_back(x);
    }
    
    int pop() {// amortized O(1)
        if (s1.empty()){
            while(!s0.empty()){
                int x=s0.back();
                s0.pop_back();
                s1.push_back(x);
            }
        }
        int x=s1.back();
        s1.pop_back();
        return x;
    }
    
    int peek() {
        if (!s1.empty()){
            front=s1.back();
        }
        return front;
    }
    
    bool empty() {
        return s0.empty() && s1.empty();
    }
};
```


