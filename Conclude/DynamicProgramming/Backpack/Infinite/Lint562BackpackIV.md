# Lint562. Backpack IV

### LintCode

## Question

Given an integer array nums[] which contains n unique positive numbers, num[i] indicate the size of ith item. An integer target denotes the size of backpack. Find the number of ways to fill the backpack.

Each item may be chosen unlimited number of times

**Example 1**
```
Input: 
nums = [2,3,6,7] and target = 7

Output: 
2

Explanation:
Solution sets are: 
[7]
[2, 2, 3]
```

**Example 2**
```
Input: 
nums = [2,3,4,5] and target = 7

Output: 
3

Explanation:
Solution sets are: 
[2, 5]
[3, 4]
[2, 2, 3]
```

## Solutions

### Soltuion 1

* Java
```
public int backPackIV(int[] nums, int target) {
    int[] dp = new int[target + 1];
    
    dp[0] = 1;
    
    for (int num : nums) {
        for (int i = num; i <= target; i++)
            dp[i] += dp[i - num];
    }
    
    return dp[target];
}
```

Infinite Backpack use loop from small to big.

**State**

`dp[i]` is the number of ways to fill target `i`.

**Function**

`dp[i] = dp[i] + dp[i - num]`

where the second `dp[i]` is from `dp[j - 1][i]`. It means without the current `num`, the number of ways to fill target `i`; `dp[i - num]` means without the current `num`, the number of ways to fill target `i - num`, those sum plus `num` could reach the target `i`.

**Initialization**

`dp[0] = 1`

 the number of ways to fill target `0` with `0` elements is `1`.

**Result**

`dp[target]`

**Complexity:**

* **worst-case time complexity:** `O(n)`, where `n` is the `target`.
* **worst-case space complexity:**  `O(n)`, where `n` is the `target`.