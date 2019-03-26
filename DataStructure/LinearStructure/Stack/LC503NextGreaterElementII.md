# LC503. Next Greater Element II

### LeetCode

## Question

Given a circular array (the next element of the last element is the first element of the array), print the Next Greater Number for every element. The Next Greater Number of a number x is the first greater number to its traversing-order next in the array, which means you could search circularly to find its next greater number. If it doesn't exist, output -1 for this number.

**Example 1:**
```
Input: [1,2,1]
Output: [2,-1,2]
Explanation: The first 1's next greater number is 2; 
The number 2 can't find next greater number; 
The second 1's next greater number needs to search circularly, which is also 2.
```

**Note:** The length of given array won't exceed 10000.

## Solutions

### Solution 1

* C++ (385ms) 
```
vector<int> nextGreaterElements(vector<int>& nums) {
    int n = nums.size();
    vector<int>res(n, INT_MIN);
    for(int i=0; i<n; ++i)
    {
        for(int j=i+1; j<=n+i; ++j)
        {
            int next = j%n;
            if(nums[next] > nums[i])
            {
                res[i] = nums[next];
                break;
            }
        }
        if(res[i]==INT_MIN) res[i] = -1;
    }
    return res;
}
```

The Brute-force approach is just traveling the `nums` to find the next grate elements of each element.

* **worst-case time complexity:** O(n<sup>2</sup>), where `n` is the length of the `nums`.
* **worst-case space complexity:** O(n), where `n` is the length of the `nums`.

### Solution 2

* C++ (113ms)
```
vector<int> nextGreaterElements(vector<int>& nums) {
    int n = nums.size();
    vector<int>res(n, -1);
    stack<int> sta;
    for(int i=n-1; i>=0; --i)
        sta.push(i);
    for(int i=n-1; i>=0; --i)
    {
        while(!sta.empty() && nums[sta.top()]<= nums[i])
            sta.pop();
        if(!sta.empty()) res[i] = nums[sta.top()];
        sta.push(i);
    }
    return res;
}
```

This idea is to find the next grate elements of each element from right to left. 

Using a stack to push all elements in first. Check each element from right to left, pop the smaller elements until find the grater elements in the stack, so all left elements can find their next greater element in the stack.

* **worst-case time complexity:** `O(n)`, where `n` is the length of the `nums`.
* **worst-case space complexity:** `O(n)`, where `n` is the length of the `nums`.
