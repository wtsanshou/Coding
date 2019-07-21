# Lint229. Stack Sorting

### LintCode

## Question

Sort a stack in ascending order (with biggest terms on top).

You may use at most one additional stack to hold items, but you may not copy the elements into any other data structure (e.g. array).

You don't need to return a new stack, just sort elements in the given parameter stack.

**Example**
```
Given stack =
| |
|3|
|1|
|2|
|4|
 -

After sort, the stack should become:
| |
|4|
|3|
|2|
|1|
 -

The data will be serialized to [4,2,1,3]. The last element is the element on the top of the stack.
```

**Notice**

* O(n^2) time is acceptable.

## Solutions

### Solution 1

* Java
```
public void stackSorting(Stack<Integer> stk) {
    int n = stk.size();
    Stack<Integer> temp = new Stack<>();
    for (int i = 0; i < n; i++) {
        int max = Integer.MIN_VALUE;
        for (int j = n - i; j > 0; j--) {
            int top = stk.pop();
            max = Math.max(max, top);
            temp.push(top);
        }
        boolean first = true;
        for (int j = n - i; j > 0; j--) {
            int tempTop = temp.pop();
            if (tempTop == max && first) {
                first = false;
                continue;
            }
            stk.push(tempTop);
        }
        temp.push(max);
    }
    while (!temp.isEmpty()) 
        stk.push(temp.pop());
}
```

The question is asking to use an additional stack. So I was thinking to use select sort to solve this problem. The main idea is to select the maximum value in the `stk` and push it to the `temp` stack in each round. After select all elements and push them all to `temp` stack, we can push all elements from `temp` to `stk` to get a sorted `stk`.

**NOTE** elements in `stk` could include duplicates, so make sure only select and push one maximum value `boolean first = true` in each round. 

**Complexity:**

* **worst-case time complexity:** O(n<sup>2</sup>), where `n` is the length of the input `stk`.
* **worst-case space complexity:** `O(n)`, where `n` is the length of the input `stk`.  
