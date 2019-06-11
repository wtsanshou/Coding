# LC96. Unique Binary Search Trees

### LeetCode

## Question

Given n, how many structurally unique BST's (binary search trees) that store values 1...n?

**For example**
```
Given n = 3, there are a total of 5 unique BST's.
   1         3     3      2      1
    \       /     /      / \      \
     3     2     1      1   3      2
    /     /       \                 \
   2     1         2                 3
```

## Solutions 

### Solution 1

* C++ (Time Limit Exceeded)
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

Using recursive, for each node `i`, the number of BST of the node `i` is the number of its left BST child `numTrees(i-1)` multiply by the number of its right BST child `numTrees(n-i)`.

**Complexity:**

* **worst-case time complexity:** O(2<sup>n</sup>).
* **worst-case space complexity:** `O(n)`.

### Solution 2

* C++ (0ms) 
```
int numTrees(int n) {
    vector<int> dp(n+1);
    dp[0] = dp[1] = 1;
    for(int i=2; i<=n; ++i)
        for(int j=0; j<i; ++j)
            dp[i] += dp[j] * dp[i-j-1];
    return dp[n];
}
```

Using `dp[j]` to store the number of left child BST of node `i`, using `dp[i-j-1]` to store the number of right child BST of node `i`.

**Complexity:**

* **worst-case time complexity:** O(n<sup>2</sup>).
* **worst-case space complexity:** `O(n)`.