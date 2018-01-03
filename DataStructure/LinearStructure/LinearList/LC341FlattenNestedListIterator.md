# LC341. Flatten Nested List Iterator

### LeetCode

## Question

Given a nested list of integers, implement an iterator to flatten it.
Each element is either an integer, or a list -- whose elements may also be integers or other lists.

**Example 1:**

`Given the list [[1,1],2,[1,1]],`

By calling next repeatedly until hasNext returns false, the order of elements returned by next should be: `[1,1,2,1,1]`.

**Example 2:**

`Given the list [1,[4,[6]]],`

By calling next repeatedly until hasNext returns false, the order of elements returned by next should be: `[1,4,6]`.

## Solutions

```
/**
 * // This is the interface that allows for creating nested lists.
 * // You should not implement it, or speculate about its implementation
 * class NestedInteger {
 *   public:
 *     // Return true if this NestedInteger holds a single integer, rather than a nested list.
 *     bool isInteger() const;
 *
 *     // Return the single integer that this NestedInteger holds, if it holds a single integer
 *     // The result is undefined if this NestedInteger holds a nested list
 *     int getInteger() const;
 *
 *     // Return the nested list that this NestedInteger holds, if it holds a nested list
 *     // The result is undefined if this NestedInteger holds a single integer
 *     const vector<NestedInteger> &getList() const;
 * };
 */
```

```
/**
 * Your NestedIterator object will be instantiated and called as such:
 * NestedIterator i(nestedList);
 * while (i.hasNext()) cout << i.next();
 */
```

* C++1 (19ms)
```
class NestedIterator {
public:
    stack<NestedInteger> myList;

    NestedIterator(vector<NestedInteger> &nestedList) {
        PushListIntoStack(nestedList);
    }

    void PushListIntoStack(vector<NestedInteger> &nestedList)
    {
        for(int i=nestedList.size()-1; i>=0; --i)
            myList.push(nestedList[i]);
    }

    int next() {
        NestedInteger top = myList.top();
        myList.pop();
        return top.getInteger();
    }

    bool hasNext() {
        if(myList.empty()) return false;
        NestedInteger top = myList.top();
        if(top.isInteger()) return true;
        myList.pop();
        PushListIntoStack(top.getList());
        return hasNext();
    }
};
```

* Java1 (10ms)
```
public class NestedIterator implements Iterator<Integer> {
    
    private Stack<NestedInteger> stk;
    
    public NestedIterator(List<NestedInteger> nestedList) {
        stk = new Stack<NestedInteger>();
        pushListToStack(nestedList);
    }

    private void pushListToStack(List<NestedInteger> nestedList){
        for(int i=nestedList.size()-1; i>=0; --i)
            stk.push(nestedList.get(i));
    }

    @Override
    public Integer next() {
        return stk.pop().getInteger();
    }

    @Override
    public boolean hasNext() {
        while(!stk.empty())
        {
            NestedInteger top = stk.peek();
            if(top.isInteger())
                return true;
            stk.pop();
            List<NestedInteger> openList = top.getList();
            pushListToStack(openList);
        }
        return false;
    }
}
```

## Testcase:

**Case 1:**

* Testcase: [[1,1],[6,7],[2,3]]
* Result: [1,1,6,7,2,3]

**Case 2:**

* Testcase: [[-1,-1],[[[]]],[2,3]]
* Result: [-1,-1,2,3]

## Explanation

Using a stack to push these nested lists in from end to front.

When check hasNext:

1. If it's an integer, leave it.
2. If it's a nested list, push all elements of this nested list into the stack from end to front.

* **worst-case time complexity:** O(n)
* **worst-case space complexity:** O(n)

