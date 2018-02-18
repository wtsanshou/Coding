# LC740. Delete and Earn

### LeetCode

## Question

Given an array nums of integers, you can perform operations on the array.

In each operation, you pick any nums[i] and delete it to earn nums[i] points. After, you must delete every element equal to nums[i] - 1 or nums[i] + 1.

You start with 0 points. Return the maximum number of points you can earn by applying such operations.

**Example 1:**
```
Input: nums = [3, 4, 2]
Output: 6
```

**Explanation:**

Delete 4 to earn 4 points, consequently 3 is also deleted.
Then, delete 2 to earn 2 points. 6 total points are earned.

**Example 2:**
```
Input: nums = [2, 2, 3, 3, 3, 4]
Output: 9
```

**Explanation: **

Delete 3 to earn 3 points, deleting both 2's and the 4.
Then, delete 3 again to earn 3 points, and 3 again to earn 3 points.
9 total points are earned.

**Note:**

* The length of nums is at most 20000.
* Each element nums[i] is an integer in the range [1, 10000].

## Solutions

* Java1
```
public int deleteAndEarn(int[] nums) {
    int[] dp = new int[10001];
    for(int x : nums)
        dp[x] += x;
    int prepreV=0, preV=0, pre=-1;
    for(int i=0; i<=10000; ++i){
        if(dp[i] == 0) continue;
        int prepreMax = Math.max(prepreV, preV);
        preV = dp[i] + (i-1==pre ? prepreV : prepreMax);
        prepreV = prepreMax;
        pre = i;
    }
    return Math.max(prepreV, preV);
}
```

## Explanation

1. Count the sum of each integer
2. Travel the `dp` 
3. If the current number has a continous previous number, we cannot use prevois maximum sum but `prepreV`
4. If the current number has no continous previous number, we can use prevois maximum sum

* **worst-case time complexity:** O(n), where n is the length of nums
* **worst-case space complexity:** O(m), where m is the integer range of nums[i]