# LC643. Maximum Average Subarray I

### LeetCode

## Question

Given an array consisting of n integers, find the contiguous subarray of given length k that has the maximum average value. And you need to output the maximum average value.

**Example 1:**

```
Input: [1,12,-5,-6,50,3], k = 4
Output: 12.75
```

Explanation: Maximum average is (12-5-6+50)/4 = 51/4 = 12.75

**Note:**

1.  1 <= k <= n <= 30,000.
2.  Elements of the given array will be in the range [-10,000, 10,000].

## Solutions

* C++1

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

* Java1

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

## Explanation

* **worst-case time complexity:** O(n)
* **worst-case space complexity:** O(1)