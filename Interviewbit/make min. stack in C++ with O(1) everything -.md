Design a stack that supports push, pop, top, and retrieving the minimum element in constant time.  

- push(x) -- Push element x onto stack.
- pop() -- Removes the element on top of the stack.
- top() -- Get the top element.
- getMin() -- Retrieve the minimum element in the stack.

Note that all the operations have to be constant time operations.

<font color="#f79646">Questions to ask the interviewer :</font>

<font color="#f79646">Q: What should getMin() do on empty stack? </font>
<font color="#f79646">A: In this case, return -1.</font>

<font color="#f79646">Q: What should pop do on empty stack? </font>
<font color="#f79646">A: In this case, nothing. </font>

<font color="#f79646">Q: What should top() do on empty stack?</font>
<font color="#f79646">A: In this case, return -1</font>

```C++
stack<int> st;
int mn=INT_MAX;
MinStack::MinStack() {
     while(!st.empty()){st.pop();}
}
void MinStack::push(int x) {
    if(st.empty()){mn = x;}
    else if(mn>=x){
        st.push(mn);
        mn = x;
    }st.push(x);
}

void MinStack::pop() {
    if(!st.empty()){
        if(st.top()==mn){
            st.pop();
            if(!st.empty()){mn = st.top();st.pop();}
            return;
        }
        st.pop();
    }
}

int MinStack::top() {
    if(st.empty()){return -1;}
    return st.top();
}

int MinStack::getMin() {
    if(st.empty()){return -1;}
    return mn;
}
```

