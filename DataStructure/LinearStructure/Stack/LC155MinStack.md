# LC155. Min Stack

### LeetCode

## Question

Design a `stack` that supports `push`, `pop`, `top`, and retrieving the minimum element in constant time.

* `push(x)` -- Push element x onto stack.
* `pop()` -- Removes the element on top of the stack.
* `top()` -- Get the top element.
* `getMin()` -- Retrieve the minimum element in the stack.

**Example:**
```
MinStack minStack = new MinStack();
minStack.push(-2);
minStack.push(0);
minStack.push(-3);
minStack.getMin();   --> Returns -3.
minStack.pop();
minStack.top();      --> Returns 0.
minStack.getMin();   --> Returns -2.
```

## Solutions

```
/**
 * Your MinStack object will be instantiated and called as such:
 * MinStack obj = new MinStack();
 * obj.push(x);
 * obj.pop();
 * int param_3 = obj.top();
 * int param_4 = obj.getMin();
 */
```

* C++1 (32ms)
```
class MinStack {
private:
    stack<int> thisStack;
    stack<int> minStack;
public:
    /** initialize your data structure here. */
    MinStack() {
        
    }
    
    void push(int x) {
        if(thisStack.empty())
        {
            thisStack.push(x);
            minStack.push(x);
        }
        else
        {
            thisStack.push(x);
            if(x<minStack.top())
                minStack.push(x);
            else
                minStack.push(minStack.top());
        }
    }
    
    void pop() {
        thisStack.pop();
        minStack.pop();
    }
    
    int top() {
        return thisStack.top();
    }
    
    int getMin() {
        return minStack.top();
    }
};
```

* C++2 (56ms)
```
class MinStack {
private:
    stack<int> myStack;
    stack<int> myMin;
public:
    /** initialize your data structure here. */
    MinStack() {
        while(!myStack.empty()) myStack.pop();
        while(!myMin.empty()) myMin.pop();
    }
    
    void push(int x) {
        myStack.push(x);
        if(myMin.empty() || x<=myMin.top())
        {
            myMin.push(x);
        }
    }
    
    void pop() {
        if(myStack.empty() ||  myMin.empty()) return;
        if(myStack.top()==myMin.top())
        {
            myStack.pop();
            myMin.pop();
        }
        else
        {
            myStack.pop();
        }
    }
    
    int top() {
        if(myStack.empty()) return -1;
        return myStack.top();
    }
    
    int getMin() {
        if(myMin.empty()) return -1;
        return myMin.top();
    }
};
```

* Java1 (144ms)
```
public class MinStack {

    private Stack<Integer> stack;
    private Stack<Integer> minStack;

    /** initialize your data structure here. */
    public MinStack() {
        stack = new Stack<Integer>();
        minStack = new Stack<>();
    }
    
    public void push(int x) {
        stack.push(x);
        if(minStack.empty())
            minStack.push(x);
        else
            minStack.push(Math.min(minStack.peek(), x));
    }
    
    public void pop() {
        stack.pop();
        minStack.pop();
    }
    
    public int top() {
        return stack.peek();
    }
    
    public int getMin() {
        return minStack.peek();
    }
}
```

## Explanation

I met this question in a white board interview.

My idea is using an `additional stack` to remember each element's corresponding minimum value in the `stack`.

**Follow up:** Could you not use any additional space?

My answer is: for each call of the method `getMin()`, traverse the whole stack to find the minimum element.

* **worst-case time complexity:** O(1)
* **worst-case space complexity:** O(N), where `N` is the number of pushed elements.