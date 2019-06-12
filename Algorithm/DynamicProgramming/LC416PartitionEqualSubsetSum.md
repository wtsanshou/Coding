# LC416. Partition Equal Subset Sum

### LeetCode

## Question

Given a non-empty array containing only positive integers, find if the array can be partitioned into two subsets such that the sum of elements in both subsets is equal.

**Note:**

1.	Each of the array element will not exceed 100.
2.	The array size will not exceed 200.

**Example 1:**

```
Input: [1, 5, 11, 5]

Output: true

Explanation: The array can be partitioned as [1, 5, 5] and [11].
```

**Example 2:**

```
Input: [1, 2, 3, 5]

Output: false

Explanation: The array cannot be partitioned into equal sum subsets.
```

## Solutions

### Solution 1

* C++ (49ms)
```
bool canPartition(vector<int>& nums) {
    int sum = accumulate(nums.begin(), nums.end(), 0);
    if(sum%2 != 0) return false;
    sum /= 2;
    vector<bool> dp(sum+1);
    dp[0] = true;
    for(auto num : nums) 
        for(int i = sum; i >= num; i--)
            dp[i] = dp[i] || dp[i - num];
    return dp[sum];
}
```

If the array can be partitioned, you must be able to find a subset whose sum is the half of the whole array's sum.

To figure out if we can find this kind of subset, we can use `dp` to store if we can reach the number between the subset's `sum` and the `num` in the `nums`.

The final result is stored at the `dp[sum]`.

**Complexity:**

* **worst-case time complexity:** `O(n * sum/2)`, where `n` is the length of the input `nums`, `sum` is the sum of the input `nums`.
* **worst-case space complexity:** `O(sum/2)`, where `sum` is the sum of the input `nums`.

### Solution 2

* C++ ( 9ms)
```
bool canPartition(vector<int>& nums) {
    bitset<5001> bits(1);
    int sum = accumulate(nums.begin(), nums.end(), 0);
    for(auto num : nums) bits |= bits << num;
    return !(sum & 1) && bits[sum>>1];
}
```

Based on the `Note`, the sum of the whole array will not more than `5000`. We can use bitset with size `5001`. Each bit represents the possible `sum` of a subset in the `nums`. Using `bits |= bits << num` to mark all possible `sum`.

Finally, is `sum` of the `nums` is even, and the bit at the location `sum/2` is `1`, we can sure it can be partitioned.

**Complexity:**

* **worst-case time complexity:** `O(n)`, where `n` is the length of the input `nums`.
* **worst-case space complexity:** `O(5001)`, where `sum` is the sum of the input `nums`.