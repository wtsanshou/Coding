# LC525. Contiguous Array

### LeetCode

## Question

Given a binary array, find the maximum length of a contiguous subarray with equal number of 0 and 1.

**Example 1:**

```
Input: [0,1]
Output: 2
Explanation: [0, 1] is the longest contiguous subarray with equal number of 0 and 1.
```

**Example 2:**
```
Input: [0,1,0]
Output: 2
Explanation: [0, 1] (or [1, 0]) is a longest contiguous subarray with equal number of 0 and 1.
```

**Note:** The length of the given binary array will not exceed 50,000.

## Solutions

### Solution 1

* C++ (189ms)
```
int findMaxLength(vector<int>& nums) {
    for(int i=0; i<nums.size(); ++i)
        if(nums[i]==0) nums[i]=-1;
    unordered_map<int, int> sumToIndex;
    sumToIndex[0]=-1; //important
    int maxL=0, sum=0;
    for(int i=0; i<nums.size(); ++i)
    {
        sum += nums[i];
        if(sumToIndex.count(sum)>0)
            maxL = max(maxL, i-sumToIndex[sum]);
        else
            sumToIndex[sum] = i;
    }
    return maxL;
}
```

If we convert all `0` to `-1`, the sum of `a contiguous subarray with equal number of 0 and 1` will be 0.

If we calculate the prefix sum from left to right, `a contiguous subarray with equal number of 0 and 1` will make the prefix sum back to a previous prefix sum value.

So we just need to use a map to store the location of each first appeared previous prefix sum value. When found a prefix sum back to a previous prefix sum value, check the length of the `a contiguous subarray with equal number of 0 and 1`.

**Note** the prefix sum could back to the most left element of the `nums`, so we need to set `sumToIndex[0]=-1`

**Exampl 1**

```
binary       1   0   0
convert      1   -1  -1
prefix   0   1   0   -1
```

**Exampl 2**

```
binary      1   1   0
convert     1   1   -1
prefix  0   1   2   1
```

**Complexity:**

* **worst-case time complexity:** `O(n)`, where `n` is the length of the input `nums`.
* **worst-case space complexity:** `O(n)`, where `n` is the length of the input `nums`.

