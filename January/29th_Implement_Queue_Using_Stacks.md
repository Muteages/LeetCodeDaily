# Implement Queue using Stacks

Implement a first in first out (FIFO) queue using only two stacks. The implemented queue should support all the functions of a normal queue (push, peek, pop, and empty).

Implement the MyQueue class:

void push(int x) Pushes element x to the back of the queue.
int pop() Removes the element from the front of the queue and returns it.
int peek() Returns the element at the front of the queue.
boolean empty() Returns true if the queue is empty, false otherwise.
Notes:

You must use only standard operations of a stack, which means only push to top, peek/pop from top, size, and is empty operations are valid.
Depending on your language, the stack may not be supported natively. You may simulate a stack using a list or deque (double-ended queue) as long as you use only a stack's standard operations.


## Approach 

``` C++
    std::stack<int> fakeQueue, temp;
public:
    MyQueue() {
        
    }
    
    void push(int x) {
        while (!fakeQueue.empty())
        {
            temp.push(fakeQueue.top());
            fakeQueue.pop();
        }
        fakeQueue.push(x);
        while (!temp.empty())
        {
            fakeQueue.push(temp.top());
            temp.pop();
        }
    }
    
    int pop() {
        int num = fakeQueue.top();
        fakeQueue.pop();
        return num;
    }
    
    int peek() {
        return fakeQueue.top();
    }
    
    bool empty() {
        return fakeQueue.empty();
    }
```

## Approach 2

``` C++
    int front;
    std::stack<int> fakeQueue, sub;
public:
    MyQueue() 
    : front(0){
        
    }
    
    void push(int x) {
        if (sub.empty())
        {
            front = x;
        }
        sub.push(x);
    }
    
    int pop() {
        if (fakeQueue.empty())
        {
            while (!sub.empty())
            {
                fakeQueue.push(sub.top());
                sub.pop();
            }
        }

        int num = fakeQueue.top();
        fakeQueue.pop();
        return num;
    }
    
    int peek() {
        if (!fakeQueue.empty())
        {
            return fakeQueue.top();
        }
        return front;
    }
    
    bool empty() {
        return fakeQueue.empty() && sub.empty();
    }
```