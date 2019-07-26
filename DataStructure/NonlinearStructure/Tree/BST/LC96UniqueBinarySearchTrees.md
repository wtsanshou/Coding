# LC96. Unique Binary Search Trees

### LeetCode

## Question

Given n, how many structurally unique BST's (binary search trees) that store values 1...n?

**For example**
```
Given n = 3

there are a total of 5 unique BST's.
   1         3     3      2      1
    \       /     /      / \      \
     3     2     1      1   3      2
    /     /       \                 \
   2     1         2                 3
```

## Solutions

### Solution 1

* C++ Time Limit Exceeded
```
int numTrees(int n) {
    if(n<=1) return 1;
    int res = 0;
    for(int i=1; i<=n; ++i)
    {
        int left = numTrees(i-1);
        int right = numTrees(n-i);
        res += left*right;
    }
    return res;
}
```

The number of structurally unique BST is fixed when the number of nodes is fixed. So, to get the number of structurally unique BST with root `i`, we just need to know how many `left` nodes and how many `right` nodes. Then the number of structurally unique BST with root `i` is `left*right`.

**Complexity:**

* **worst-case time complexity:** O(2<sup>n</sup>).
* **worst-case space complexity:** `O(n)`.

### Solution 2

* C++2 (0ms)
```
int numTrees(int n) {
    vector<int> dp(n + 1);
    dp[0] = dp[1] = 1;
    for(int i = 2; i <= n; ++i)
        for(int j = 0; j < i; ++j)
            dp[i] += dp[j] * dp[i - j - 1];
    return dp[n];
}
```

If we use DP, we need to figure out the sub question which can be re-used to get base question. The sum of all possible sub questions' combinations generate the result of the base quesiton.

We can keep the number of structurally unique BST of small number of nodes in `dp`, which can be re-used to calculate the number of structurally unique BST of bigger number of nodes.

**Complexity:**

* **worst-case time complexity:** O(n<sup>2</sup>).
* **worst-case space complexity:** `O(n)`.

