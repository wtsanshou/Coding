# LC232. Implement Queue using Stacks

### LeetCode

## Question

Implement the following operations of a `queue` using `stacks`.

* `push(x)` -- Push element `x` to the back of queue.
* `pop()` -- Removes the element from in front of queue.
* `peek()` -- Get the front element.
* `empty()` -- Return whether the queue is empty.

**Notes:**

You must use only standard operations of a `stack` -- which means only push to top, peek/pop from top, size, and is empty operations are valid.

* Depending on your language, `stack` may not be supported natively. You may simulate a stack by using a list or deque (double-ended queue), as long as you use only standard operations of a stack.
* You may assume that all operations are valid (for example, no pop or peek operations will be called on an empty queue).

```
/**
 * Your MyQueue object will be instantiated and called as such:
 * MyQueue obj = new MyQueue();
 * obj.push(x);
 * int param_2 = obj.pop();
 * int param_3 = obj.peek();
 * bool param_4 = obj.empty();
 */
```

## Solutions

* C++1 (3ms)
```
class MyQueue {
private:
    stack<int> inputStack;
    stack<int> outputStack;
public:
    /** Initialize your data structure here. */
    MyQueue() {
        
    }
    
    /** Push element x to the back of queue. */
    void push(int x) {
        inputStack.push(x);
    }
    
    /** Removes the element from in front of queue and returns that element. */
    int pop() {
        int res = peek();
        outputStack.pop();
        return res;
    }
    
    /** Get the front element. */
    int peek() {
        if(outputStack.empty())
        {
            while(!inputStack.empty())
            {
                outputStack.push(inputStack.top());
                inputStack.pop();
            }
        }
        return outputStack.top();
    }
    
    /** Returns whether the queue is empty. */
    bool empty() {
        return outputStack.empty() && inputStack.empty();
    }
};
```

* C++2 (0ms)
```
class Queue {
public:
    stack<int> s;
    stack<int> sub;
    
    void aStackb(stack<int>& a, stack<int>& b)
    {
        while(!a.empty())
        {
            b.push(a.top());
            a.pop();
        }
    }
    
    // Push element x to the back of queue.
    void push(int x) {
        aStackb(s, sub);
        s.push(x);
        aStackb(sub, s);
    }

    // Removes the element from in front of queue.
    void pop(void) {
        s.pop();
    }

    // Get the front element.
    int peek(void) {
        return s.top();
    }

    // Return whether the queue is empty.
    bool empty(void) {
        return s.empty();
    }
};
```

* Java1 (120ms)
```
class MyQueue {
    private Stack<Integer> input = new Stack();
    private Stack<Integer> output = new Stack();
    // Push element x to the back of queue.
    public void push(int x) {
        input.push(x);
    }

    // Removes the element from in front of queue.
    public void pop() {
        peek();
        output.pop();
    }

    // Get the front element.
    public int peek() {
        if(output.empty())
        {
            while(!input.empty())
            {
                output.push(input.pop());
            }
        }
        return output.peek();
    }

    // Return whether the queue is empty.
    public boolean empty() {
        return input.empty() && output.empty();
    }
}
```

* Java2 (117ms)
```
class MyQueue {
    private Stack<Integer> input = new Stack();
    private Stack<Integer> output = new Stack();
    
    void aStackb(Stack<Integer> a, Stack<Integer> b)
    {
        while(!a.empty())
        {
            b.push(a.pop());
        }
    }
    
    // Push element x to the back of queue.
    public void push(int x) {
        aStackb(output, input);
        output.push(x);
        aStackb(input, output);
    }

    // Removes the element from in front of queue.
    public void pop() {
        output.pop();
    }

    // Get the front element.
    public int peek() {
        return output.peek();
    }

    // Return whether the queue is empty.
    public boolean empty() {
        return output.empty();
    }
}
```

## Explanation

**Solution1**: Using two stacks, `inputStack` for `push`, `outputStack` for `pop`. When `outputStack` becomes empty, put elements from `inputStack` to `outputStack`.

`push()` :  **worst-case time complexity:** O(1)

`pop()` :  **worst-case time complexity:** O(N), where `N` is the length of the list.

`peek()` :  **worst-case time complexity:** O(N), where `N` is the length of the list.

`empty()` :  **worst-case time complexity:** O(1)

**Solution1**: Using two stacks, `inputStack` for `push`, `outputStack` for `pop`. Before `push` a new element, put all elements from `outputStack` to `inputStack`. Then `push` the new element. Finally, put all elements from `inputStack` to `outputStack`.

`push()` :  **worst-case time complexity:** O(N), where `N` is the length of the list.

`pop()` :  **worst-case time complexity:** O(1)

`peek()` :  **worst-case time complexity:** O(1)

`empty()` :  **worst-case time complexity:** O(1)

* **worst-case space complexity:** O(N)