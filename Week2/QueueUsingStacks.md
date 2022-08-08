[Problem Statement](https://leetcode.com/problems/implement-queue-using-stacks)

## Approach 1 [Using 2 stacks] :- In this approach, we'll perform push, pop, peek and check empty by following conditions.
First we'll create two stacks s1 and s2.
- Push operation - To perform push operation, pop the elements until s1 is empty then push new element and push all elements of s2 to s1.
- Pop operation - store the top and pop the element and return the top.
- Peek operation - return the top.
- Empty - check the emptiness as usual.

```cpp
// Time Complexity - O(n)            Space Complexity - O(n)
class MyQueue {
public:
     stack<int> s1;
     stack<int> s2;
    MyQueue() {
        
    }
    
    void push(int x) {
        while(!s1.empty())
        {
            s2.push(s1.top());
            s1.pop();
        }
        s1.push(x);
        while(!s2.empty())
        {
            s1.push(s2.top());
            s2.pop();
        }
    }
    
    int pop() {
        int curr = s1.top();
        s1.pop();
        return curr;
    }
    
    int peek() {
        return s1.top();
    }
    
    bool empty() {
        return s1.empty();
    }
};
```

## Approach 2 [Using 2 stacks] :- In this approach , we'll perform push,pop,peek and empty by following conditions.
First we'll create 2 stacks s1 and s2.
- Push operation - In this, simply push it in s1.
- Pop operation - In this, [if s2 is empty] -> [Pop the element from s1 and push it in s2 , then store the top and pop from s2,then return it] ,else -> store the top and pop from s2,then return it.
- Peek operation - In this, [if s2 is empty] -> [Pop the element from s1 and push it in s2 , then return the top from s2] ,else -> return top from s2.
- Empty :- In this, if both stacks are empty return true else false.

```cpp
// Time Complexity - O(1) {amortised time complexity}       Space Complexity - O(n)
class MyQueue {
public:
    stack<int> s1;
    stack<int> s2;
    MyQueue() {
        
    }
    
    void push(int x) {
        s1.push(x);
    }
    
    int pop() {
        int curr;
        if(s2.empty())
        {
            while(!s1.empty())
            {
                s2.push(s1.top());
                s1.pop();
            }
        }
        curr = s2.top();
        s2.pop();
        return curr;
    }
    
    int peek() {
        if(s2.empty())
        {
            while(!s1.empty())
            {
                s2.push(s1.top());
                s1.pop();
            }
        }
        return s2.top();
    }
    
    bool empty() {
        return s1.empty() and s2.empty();
    }
};

```
