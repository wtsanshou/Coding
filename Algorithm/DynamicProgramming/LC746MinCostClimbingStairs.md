# LC746. Min Cost Climbing Stairs

### LeetCode

## Question

On a staircase, the i-th step has some non-negative cost cost[i] assigned (0 indexed).

Once you pay the cost, you can either climb one or two steps. You need to find minimum cost to reach the top of the floor, and you can either start from the step with index 0, or the step with index 1.

**Example 1:**

```
Input: cost = [10, 15, 20]
Output: 15
```

**Explanation:** 

Cheapest is start on cost[1], pay that cost and go to the top.

**Example 2:**

```
Input: cost = [1, 100, 1, 1, 1, 100, 1, 1, 100, 1]
Output: 6
```

**Explanation:** 

Cheapest is start on cost[0], and only step on 1s, skipping cost[3].

**Note:**

* cost will have a length in the range [2, 1000].
* Every cost[i] will be an integer in the range [0, 999].

## Solutions

* C#1 (202ms)
```
public int MinCostClimbingStairs(int[] cost) {
    int n = cost.Length;
    int[] dp = new int[n];
    dp[0] = cost[0];
    dp[1] = cost[1];
    for(int i=2; i<n; ++i)
        dp[i] = cost[i] + Math.Min(dp[i-1], dp[i-2]);
    return Math.Min(dp[n-1], dp[n-2]);
}
```

* C#2 (168ms)
```
public int MinCostClimbingStairs(int[] cost) {
    int a = cost[0], b = cost[1];
    for(int i=2; i<cost.Length; ++i){
        int min = cost[i] + Math.Min(a, b);
        a = b;
        b = min;
    }
    return Math.Min(a, b);
}
```

## Explanation

It's quite like the question * <a href="Mathematics/NumberTheory/Fibonacci/LC70ClimbingStairs.md">LC70. Climbing Stairs</a>, but we need to consider the climbing cost this time. 

Only the final two steps are able to reach the top, so we can use Dynamic Programming to calculate the minimum climbing cost of each step. Finally, the minimum cost of the final two steps is the result.

Normally, the Dynamic Programming algorithm will cost O(n) space. In this question, for each step, we just consider previous two steps. Therefore, we can just use two integers to save the two steps' minimum climbing costs.

* **worst-case time complexity:** O(n)

**C#1**

* **worst-case space complexity:** O(n)

**C#2**

* **worst-case space complexity:** O(1)
