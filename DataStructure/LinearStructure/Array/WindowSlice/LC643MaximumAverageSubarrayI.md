# LC643. Maximum Average Subarray I

### LeetCode

## Question

Given an array consisting of n integers, find the contiguous subarray of given length k that has the maximum average value. And you need to output the maximum average value.

**Example 1:**
```
Input: [1,12,-5,-6,50,3], k = 4
Output: 12.75
Explanation: Maximum average is (12-5-6+50)/4 = 51/4 = 12.75
```

**Note:**

1.	1 <= k <= n <= 30,000.
2.	Elements of the given array will be in the range [-10,000, 10,000].

## Solutions

### Solution 1

* C++
```
double findMaxAverage(vector<int>& nums, int k) {
    double res=0, sum=0;
    for(int i=0; i<k; ++i)
        sum += nums[i];
    res = sum;
    for(int i=0, j=k; j<nums.size(); i++, j++)
    {
        sum = sum - nums[i] + nums[j];
        res = max(res, sum);
    }
    return res/k;
}
```

* Java
```
public double findMaxAverage(int[] nums, int k) {
    double res=0, sum=0;
    for(int i=0; i<k; ++i)
        sum += nums[i];
    res = sum;
    for(int i=0, j=k; j<nums.length; ++i, ++j){
        sum = sum - nums[i] + nums[j];
        res = Math.max(res, sum);
    }
    return res/k;
}
```

We just need to get the sum of a window slice whith length `k`, and move it from left to end to find the contiguous subarray of given length k that has the maximum sum value.

* **worst-case time complexity:** O(n), where `n` is the length of the `nums`.
* **worst-case space complexity:** O(1)

### Solution 2

* Java (8 ms,  41.8 MB)
```
public double findMaxAverage(int[] nums, int k) {
    for(int i=1; i<nums.length; ++i)
        nums[i] += nums[i-1];
    
    double maxSum = nums[k-1];
    for(int i=k; i<nums.length; ++i)
        maxSum = Math.max(maxSum, (double)(nums[i]-nums[i-k]));
    
    return maxSum/k;
}
```

The question of `finding the contiguous subarray of given length k that has the maximum average value` can be splited to `finding the contiguous subarray of given length k that has the maximum sum value` first.

The idea is to sum all left numbers of `nums[i]`, then it's very easy to get the `sum` of the contiguous subarray of given length k.

Finally, we just need to find out the maximum `sum` and divided by `k`.

* **worst-case time complexity:** O(n), where `n` is the length of the `nums`.
* **worst-case space complexity:** O(1)
