# LC724. Find Pivot Index

### LeetCode

## Question

Given an array of integers nums, write a method that returns the "pivot" index of this array.

We define the pivot index as the index where the sum of the numbers to the left of the index is equal to the sum of the numbers to the right of the index.

If no such index exists, we should return -1. If there are multiple pivot indexes, you should return the left-most pivot index.

**Example 1:**

```
Input: 
nums = [1, 7, 3, 6, 5, 6]
Output: 3
```

**Explanation:** 

The sum of the numbers to the left of index 3 (nums[3] = 6) is equal to the sum of numbers to the right of index 3.

Also, 3 is the first index where this occurs.

**Example 2:**

```
Input: 
nums = [1, 2, 3]
Output: -1
```

**Explanation:**

There is no index that satisfies the conditions in the problem statement.

**Note:**

* The length of nums will be in the range [0, 10000].
* Each element nums[i] will be an integer in the range [-1000, 1000].

## Solutions

* C#1
```
public int PivotIndex(int[] nums) {
    int n = nums.Length;
    int[] leftSum = new int[n];
    int[] rightSum = new int[n];
    for(int i=1; i<n; ++i){
        leftSum[i] = leftSum[i-1] + nums[i-1];
        rightSum[n-i-1] = rightSum[n-i] + nums[n-i];
    }
    for(int i=0; i<n; ++i){
        if(leftSum[i] == rightSum[i])
            return i;
    }
    return -1;
}
```

## Explanation

Get the arrays left sum and right sum. Check from left to right to see if found the request.

**NOTE:** I found the same question in Codility <a>Codility Equi</a>

* **worst-case time complexity:** O(n)
* **worst-case space complexity:** O(n)