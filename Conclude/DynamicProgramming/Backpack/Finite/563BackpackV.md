# 563. Backpack V

### LintCode (Medium)

## Question

Given n items with size nums[i] which an integer array and all positive numbers. An integer target denotes the size of a backpack. Find the number of possible fill the backpack.

Each item may only be used once

**Example**
```
Given:
candidate items [1,2,3,3,7] and target 7,

return:
2

Explanation:
A solution set is: 
[7]
[1, 3, 3]
```

## Solutions

### Solution 1

1. `DFS`
2. `DFS` + `Memory Search`

### Solution 2

* Java
```
public int backPackV(int[] nums, int target) {
    int n = nums.length;
    int[][] dp = new int[n + 1][target + 1];
    dp[0][0] = 1;
    
    for (int i = 1; i <= n; i++) {
        for (int j = 0; j <= target; j++) {
            dp[i][j] = dp[i - 1][j];
            if (nums[i - 1] <= j)
                dp[i][j] += dp[i - 1][j - nums[i - 1]];
        }
    }
    
    return dp[n][target];
}
```

**State**

`dp[i][j]` is the maximum number of possible fill to target `j` with the first `i` numbers.

**Function**

if `nums[i - 1] <= j`

`dp[i][j] = dp[i - 1][j] + dp[i - 1][j - nums[i - 1]]`

where `dp[i - 1][j]` is the maximum number of possible fill to target `j` without using `nums[i - 1]` with the first `i - 1` elements; `dp[i - 1][j - nums[i - 1]]` is the maximum number of possible fill to target `j - nums[i - 1]` with first `i - 1` elements, so that these results plus `nums[i - 1]` will be target `j`.

else

`dp[i][j] = dp[i - 1][j]`

**Initialization**

`dp[0][0] = 1`, `0` number and target `0` is `1` possible fill target.

**Result**

`dp[n][target]`

**Complexity:**

* **worst-case time complexity:** `O(n * m)`, where `n` is the number of `nums`, `m` is the `target.
* **worst-case space complexity:**  `O(n * m)`, where `n` is the number of `nums`, `m` is the `target.

### Solution 3 (Roll Optimize)

* Java
```
public int backPackV(int[] nums, int target) {
    int n = nums.length;
    int[][] dp = new int[2][target + 1];
    dp[0][0] = 1;
    
    for (int i = 1; i <= n; i++) {
        for (int j = 0; j <= target; j++) {
            dp[i % 2][j] = dp[(i - 1) % 2][j];
            if (nums[i - 1] <= j)
                dp[i % 2][j] += dp[(i - 1) % 2][j - nums[i - 1]];
        }
    }
    
    return dp[n % 2][target];
}
```

**Function**

if `nums[i - 1] <= j`

```
dp[i][j] = dp[i - 1][j] + dp[i - 1][j - nums[i - 1]]
    ||
    ||
    \/
dp[i % 2][j] = dp[(i - 1) % 2][j] + dp[(i - 1) % 2][j - nums[i - 1]]    
```

else

```
dp[i][j] = dp[i - 1][j]
    ||
    ||
    \/
dp[i % 2][j] = dp[(i - 1) % 2][j]  
```

**Complexity:**

* **worst-case time complexity:** `O(n * m)`, where `n` is the number of `nums`, `m` is the `target.
* **worst-case space complexity:**  `O(m)`, where `m` is the `target.

### Solution 4 (Dimensionality Reduction)

* Java
```
 public int backPackV(int[] nums, int target) {
    int[] dp = new int[target + 1];
    dp[0] = 1;
    
    for (int i = 1; i <= nums.length; i++) {
        for (int j = target; j >= nums[i - 1]; j--) {
            dp[j] += dp[j - nums[i - 1]];
        }
    }
    
    return dp[target];
}
```

To reduce the dimension, we can change the second loop from big to small values.

**Complexity:**

* **worst-case time complexity:** `O(n * m)`, where `n` is the number of `nums`, `m` is the `target.
* **worst-case space complexity:**  `O(m)`, where `m` is the `target.
