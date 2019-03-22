# LC494. Target Sum

### LeetCode

## Question

You are given a list of non-negative integers, a1, a2, ..., an, and a target, S. Now you have 2 symbols `+` and `-`. For each integer, you should choose one from `+` and `-` as its new symbol.

Find out how many ways to assign symbols to make sum of integers equal to target S.

**Example 1:**
```
Input: nums is [1, 1, 1, 1, 1], S is 3. 
Output: 5
Explanation: 

-1+1+1+1+1 = 3
+1-1+1+1+1 = 3
+1+1-1+1+1 = 3
+1+1+1-1+1 = 3
+1+1+1+1-1 = 3

There are 5 ways to assign symbols to make the sum of nums be target 3.
```

**Note:**

1.	The length of the given array is positive and will not exceed 20.
2.	The sum of elements in the given array will not exceed 1000.
3.	Your output answer is guaranteed to be fitted in a 32-bit integer.

## Solutions

### Solution 1

* C++ (386ms)
```
class Solution {
public:
    int TargetSum(vector<int>& nums, int S, int i)
    {
        if(i == nums.size())
            return S==0 ? 1 : 0;
        int res = 0;
        res += TargetSum(nums, S+nums[i], i+1);
        res += TargetSum(nums, S-nums[i], i+1);
        return res;
    }
    int findTargetSumWays(vector<int>& nums, int S) {
        return TargetSum(nums, S, 0);
    }
};
```

The brute force approach is based on recursion. We need to check all possible combinations which sum to target `S`.

* **worst-case time complexity:** O(2<sup>n</sup>), where `n` is the length of the `nums`.
* **worst-case space complexity:** O(n), where `n` is the length of the `nums`.

### Solution 2

* C++ (3ms) DP
```
class Solution {
public:
    int subsetSum(vector<int>& nums, int target)
    {
        vector<int>dp(target+1);
        dp[0]=1;
        for(auto num : nums)
            for(int i=target; i>=num; --i)
                dp[i] += dp[i-num];
        return dp[target];
    }
    int findTargetSumWays(vector<int>& nums, int S) {
        int sum = accumulate(nums.begin(), nums.end(), 0);
        return (sum<S || (sum+S)%2 != 0) ? 0 : subsetSum(nums, (sum+S)/2);
    }
};
```

The original problem statement is equivalent to:

Find a subset of nums that need to be positive, and the rest of them negative, such that the sum is equal to target

Let P be the positive subset and N be the negative subset

**For example:**
```
Given nums = [1, 2, 3, 4, 5] and target = 3 then one possible solution is +1-2+3-4+5 = 3
Here positive subset is P = [1, 3, 5] and negative subset is N = [2, 4]
```

Then let's see how this can be converted to a subset sum problem:

```
                  sum(P) - sum(N) = target
sum(P) + sum(N) + sum(P) - sum(N) = target + sum(P) + sum(N)
                       2 * sum(P) = target + sum(nums)
```

So the original problem has been converted to a subset sum problem as follows:

Find a subset P of nums such that `sum(P) = (target + sum(nums)) / 2`

Note that the above formula has proved that `target + sum(nums)` must be even

Then using `dp` to find the possible ways of subset's sum of new target `(target + sum(nums)) / 2`

`dp[i]` store the possible ways of subset which sum to `i`.

* **worst-case time complexity:** O(n<sup>2</sup>), where `n` is the length of the `nums`.
* **worst-case space complexity:** O(n), where `n` is the length of the `nums`.
