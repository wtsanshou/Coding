# LC53. Maximum Subarray

### LeetCode

## Question

Find the contiguous subarray within an array (containing at least one number) which has the largest sum.

**For example**
```
given the array [-2,1,-3,4,-1,2,1,-5,4],
the contiguous subarray [4,-1,2,1] has the largest sum = 6.
```

**More practice:**

* If you have figured out the O(n) solution, try coding another solution using the divide and conquer approach, which is more subtle.

## Solutions

### Solution 1

* Java
```
public int maxSubArray(int[] nums) {
    int n = nums.length;
    int dp[] = new int[n];
    int curMax = dp[0] = nums[0];

    for(int i=1; i<n; ++i){
        dp[i] = Math.max(dp[i-1]+nums[i], nums[i]);
        curMax = Math.max(curMax, dp[i]);
    }

    return curMax;
}
```

`dp[i]` store the maximum sum of the Maximum Subarray left of `i`.

* **worst-case time complexity:** `O(n)`, where `n` is the length of the `nums`.
* **worst-case space complexity:** `O(n)`, where `n` is the length of the `nums`.

* Java (Roll Optimize)
```
public int maxSubArray(int[] nums) {
    int n = nums.length;
    int dp[] = new int[2];
    int curMax = dp[0] = nums[0];

    for(int i = 1; i < n; ++i){
        dp[i % 2] = Math.max(dp[(i - 1) % 2] + nums[i], nums[i]);
        curMax = Math.max(curMax, dp[i % 2]);
    }

    return curMax;
}
```

**State**

`dp[i]` is the maximum sum of contiguous subarray left of `i`.

**Function**

```
dp[i] = Math.max(dp[(i - 1)] + nums[i], nums[i])

        ||
        ||  Roll Optimize
        \/

dp[i % 2] = Math.max(dp[(i - 1) % 2] + nums[i], nums[i])
```

**Initialization**

`dp[0] = nums[0]`

**Result**

`max(dp[i])`

**Complexity:**

* **worst-case time complexity:** `O(n)`, where `n` is the length of the `nums`.
* **worst-case space complexity:** `O(1)`.

### Solution 2

* C++ (12ms)
```
int maxSubArray(vector<int>& nums) {
    int preMax = nums[0], curMax = nums[0];
    for(int i=1; i<nums.size(); ++i)
    {
        preMax = max(preMax+nums[i], nums[i]);
        curMax = max(preMax, curMax); //save the maximum sum
    }
    return curMax;
}
```

* C++ (15ms)
```
int maxSubArray(vector<int>& nums) {
    int maxCur=0, maxSub=INT_MIN;
    for(int num : nums)
    {
        maxCur = max(maxCur + num, num);
        maxSub = max(maxSub, maxCur);
    }
    return maxSub;
}
```

Because `i-1` is needed, so we can save the `O(n)` space.

* **worst-case time complexity:** `O(n)`, where `n` is the length of the `nums`.
* **worst-case space complexity:** `O(1)`

### Solution 3 (divide and conquer)

divide and conquer make it complex, we have to consider the max value of left, right and cross part.

## Follow up

* What if we want to return the subArray?
* What if the subArray is not continous?

Using `dp`, we can know where the subArray is located.

If the subArray is not continous, it will make the question easier. The `maxSubArray` is the sum of all positive numbers in the `nums`.
