# LC456. 132 Pattern

### LeetCode

## Question

Given a sequence of n integers a1, a2, ..., an, a 132 pattern is a subsequence ai, aj, ak such that i < j < k and ai < ak < aj. Design an algorithm that takes a list of n numbers as input and checks whether there is a 132 pattern in the list.

**Note:** n will be less than 15,000.

**Example 1:**
```
Input: [1, 2, 3, 4]

Output: False

Explanation: There is no 132 pattern in the sequence.
```

**Example 2:**
```
Input: [3, 1, 4, 2]

Output: True

Explanation: There is a 132 pattern in the sequence: [1, 4, 2].
```

**Example 3:**
```
Input: [-1, 3, 2, 0]

Output: True

Explanation: There are three 132 patterns in the sequence: [-1, 3, 2], [-1, 3, 0] and [-1, 2, 0].
```

## Solutions

* C++1
```
bool find132pattern(vector<int>& nums) {
    int s3 = INT_MIN;
    stack<int> minHeap;
    for(int i=nums.size()-1; i>=0; --i)
    {
        if(nums[i] < s3) return true;
        else
        {
            while(!minHeap.empty() && nums[i] > minHeap.top()) 
            {
                s3 = minHeap.top(); //the largest s3 which is less than nums[i]
                minHeap.pop();
            }
            minHeap.push(nums[i]);
        }
    }
    return false;
}
```

## Explanation

Traverse from back of the input vector `nums`. Using a stack to remember all numbers which are larger or equals `s3`. The elements in the stack is in order, just like a minHeap because any elements which are less than current number `nums[i]` will be `poped` from the stack.

When found a `s2`, search in the stack and found the maximum number (the new `s3`) which is less than the `s2`.

Once found a `s1` which is less than `s3`, the `132 pattern` is found.

* **worst-case time complexity:** O(N), where `N` is the size of the input vector `nums`.
* **worst-case space complexity:** O(N), where `N` is the size of the input vector `nums`.