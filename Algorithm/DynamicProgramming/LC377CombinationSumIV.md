# LC377. Combination Sum IV

### LeetCode

## Question

Given an integer array with all positive numbers and no duplicates, find the number of possible combinations that add up to a positive integer target.

**Example:**
```
nums = [1, 2, 3]
target = 4

The possible combination ways are:
(1, 1, 1, 1)
(1, 1, 2)
(1, 2, 1)
(1, 3)
(2, 1, 1)
(2, 2)
(3, 1)

Note that different sequences are counted as different combinations.

Therefore the output is 7.
```

**Follow up:**

* What if negative numbers are allowed in the given array?
* How does it change the problem?
* What limitation we need to add to the question to allow negative numbers?

## Solutions

### Solution 1
* C++ (12ms)
```
int combinationSum4(vector<int>& nums, int target) {
    int dp[target+1] = {0};
    dp[0] = 1;
    for(int i=1; i<=target; ++i)
        for(int num : nums)
            if(i >= num)
                dp[i] += dp[i - num];
    return dp[target];
}
```

Any combined number `i-num` can be `i` by adding `num`, where `num` is in the `nums`.

So the number of combination `dp[i - num]` is part of the number of combination `dp[i]`.

**Complexity:**

* **worst-case time complexity:** `O(t * n)`, where `t` is the target, `n` is the size of `nums`.
* **worst-case space complexity:** `O(t)`, where `t` is the target.

### Solution 2

* C++ (3ms)
```
int combinationSum4(vector<int>& nums, int target) {
    int comb[target+1] = {0};
    comb[0] = 1;
    sort(nums.begin(), nums.end());
    for(int i=1; i<=target; ++i)
        for(int j=0;j<nums.size() && nums[j]<=i; ++j)
            comb[i] += comb[i-nums[j]];
    return comb[target];
}
```

Sorting the `nums`, so we can avoid checking `nums[j]` who is larger than `i`.

**Complexity:**

* **worst-case time complexity:** `O(t * n)`, where `t` is the target, `n` is the size of `nums`.
* **worst-case space complexity:** `O(t)`, where `t` is the target.
