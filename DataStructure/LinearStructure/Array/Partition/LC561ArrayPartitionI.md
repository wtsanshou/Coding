# LC561. Array Partition I

### LeetCode

## Question

Given an array of 2n integers, your task is to group these integers into n pairs of integer, say (a1, b1), (a2, b2), ..., (an, bn) which makes sum of min(ai, bi) for all i from 1 to n as large as possible.

**Example 1:**
```
Input: [1,4,3,2]

Output: 4
Explanation: n is 2, and the maximum sum of pairs is 4.
```

**Note:**

1.	n is a positive integer, which is in the range of [1, 10000].
2.	All the integers in the array will be in the range of [-10000, 10000].

## Solutions

### Solution 1

* C++
```
int arrayPairSum(vector<int>& nums) {
    int res = 0;
    sort(nums.begin(), nums.end());
    for(int i=0; i<nums.size(); ++i)
        if(i % 2 == 0)
            res += nums[i];
    return res;
}
```

To get the maximum sum of pairs min(ai, bi), the largest integer is not possible selected, but the second largest integer is very helpful to maximum the result. Therefore, we pair the (largest, second largest). For the rest integers, we adopt the same strategy, always select the second largest integer.

So the result is to select the even `i` position's `nums[i]` in the sorted `nums`.

* **worst-case time complexity:** `O(n*log(n))`, where `n` is the length of the `nums`.
* **worst-case space complexity:** `O(log(n))`, where `n` is the length of the `nums`.

