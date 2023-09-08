# Implement Stack using Queues

https://leetcode.com/problems/implement-stack-using-queues/description/

Implement a last-in-first-out (LIFO) stack using only two queues. The implemented stack should support all the functions of a normal stack (push, top, pop, and empty).

Implement the MyStack class:

void push(int x) Pushes element x to the top of the stack.
int pop() Removes the element on the top of the stack and returns it.
int top() Returns the element on the top of the stack.
boolean empty() Returns true if the stack is empty, false otherwise.


## Approach 1

Use deque container

``` C++
class MyStack {
public:
    std::deque<int> dq;
    MyStack() {
        dq.clear();
    }
    
    void push(int x) {
        dq.push_back(x);
    }
    
    int pop() {
        int temp = dq.back();
        dq.pop_back();
        return temp;
    }
    
    int top() {
        return dq.back();
    }
    
    bool empty() {
        return dq.empty();
    }
};
```


## Follow-up Approach

Use only one queue

``` C++
class MyStack {
public:
    std::queue<int> q;

    MyStack() {
    }
    
    void push(int x) {
        q.push(x);
    }
    
    int pop() {
        int n = q.size();
        while (--n)
        {
            int temp = q.front();
            q.pop();
            q.push(temp);
        }
        int front = q.front();
        q.pop();
        return front;
    }
    
    int top() {
        return q.back();
    }
    
    bool empty() {
        return q.empty();
    }
};
```