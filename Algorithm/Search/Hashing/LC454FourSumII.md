# LC454. Four Sum II

### LeetCode

## Question

Given four lists A, B, C, D of integer values, compute how many tuples (i, j, k, l) there are such that A[i] + B[j] + C[k] + D[l] is zero.

To make problem a bit easier, all A, B, C, D have same length of N where 0 ≤ N ≤ 500. All integers are in the range of -2<sup>28</sup> to 2<sup>28</sup> - 1 and the result is guaranteed to be at most 2<sup>31</sup> - 1.

**Example:**
```
Input:
A = [ 1, 2]
B = [-2,-1]
C = [-1, 2]
D = [ 0, 2]

Output:
2
```

**Explanation:**

The two tuples are:

1. (0, 0, 0, 1) -> A[0] + B[0] + C[0] + D[1] = 1 + (-2) + (-1) + 2 = 0
2. (1, 1, 0, 0) -> A[1] + B[1] + C[0] + D[0] = 2 + (-1) + (-1) + 0 = 0

## Solutions

### Solution 1

* C++ (399ms)
```
int fourSumCount(vector<int>& A, vector<int>& B, vector<int>& C, vector<int>& D) {
    unordered_map<int, int> sumAB;
    int res = 0;
    for(auto a : A)
        for(auto b : B)
            sumAB[a+b]++;
    for(auto c : C)
        for(auto d : D)
            res += sumAB[-(c+d)];
    return res;
} 
```

1. Put all possible `TwoSum1` of two lists (maximum 2500 in total) into a map.
2. Check the possible `TwoSum2` of another two lists, find if (-`TwoSum2`) in the map.

**Complexity:**

* **worst-case time complexity:** O(N<sup>2</sup>), where `N` is the length of the input `A`.
* **worst-case space complexity:** O(N<sup>2</sup>), where `N` is the length of the input `A`.


