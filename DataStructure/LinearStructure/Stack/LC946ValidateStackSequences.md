# LC946. Validate Stack Sequences

### LeetCode

## Question

Given two sequences pushed and popped with distinct values, return true if and only if this could have been the result of a sequence of push and pop operations on an initially empty stack.

**Example 1:**
```
Input: pushed = [1,2,3,4,5], popped = [4,5,3,2,1]
Output: true
Explanation: We might do the following sequence:
push(1), push(2), push(3), push(4), pop() -> 4,
push(5), pop() -> 5, pop() -> 3, pop() -> 2, pop() -> 1
```

**Example 2:**
```
Input: pushed = [1,2,3,4,5], popped = [4,3,5,1,2]
Output: false
Explanation: 1 cannot be popped before 2.
``` 

**Note:**

* 0 <= pushed.length == popped.length <= 1000
* 0 <= pushed[i], popped[i] < 1000
* pushed is a permutation of popped.
* pushed and popped have distinct values.

## Solutions

### Solution 1

* Scala (372 ms, 48.5 MB)
```
def validateStackSequences(pushed: Array[Int], popped: Array[Int]): Boolean = {
    var stack = scala.collection.mutable.Stack[Int]() 
    var (i, j) = (0, 0)
    while(i < pushed.length){
        stack.push(pushed(i))
        i += 1
        while(j < popped.length && !stack.isEmpty && popped(j) == stack.top){
            j += 1
            stack.pop()
        }
    }
    j==popped.length
}
```

Simulate the process of the pushing and popping to a stack. If all values in the `pushed` and `popped` can be processed through the stack, it will be a Validate Stack Sequences.

**Note :** the stack will be empty finally if it is a Validate Stack Sequences.

* **worst-case time complexity:** `O(N)`, where `N` is the length of `pushed` or `popped`.
* **worst-case space complexity:** O(1), where `N` is the length of `pushed` or `popped`.
