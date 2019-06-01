# LC532. K-diff Pairs in an Array

### LeetCode

## Question

Given an array of integers and an integer k, you need to find the number of unique k-diff pairs in the array. Here a k-diff pair is defined as an integer pair (i, j), where i and j are both numbers in the array and their absolute difference is k.

**Example 1:**
```
Input: [3, 1, 4, 1, 5], k = 2
Output: 2
Explanation: There are two 2-diff pairs in the array, (1, 3) and (3, 5).
Although we have two 1s in the input, we should only return the number of unique pairs.
```

**Example 2:**
```
Input:[1, 2, 3, 4, 5], k = 1
Output: 4
Explanation: There are four 1-diff pairs in the array, (1, 2), (2, 3), (3, 4) and (4, 5).
```

**Example 3:**

```
Input: [1, 3, 1, 5, 4], k = 0
Output: 1
Explanation: There is one 0-diff pair in the array, (1, 1).
```

**Note:**

1.	The pairs (i, j) and (j, i) count as the same pair.
2.	The length of the array won't exceed 10,000.
3.	All the integers in the given input belong to the range: [-1e7, 1e7].

## Solutions

### Solution 1

* C++ (39ms)
```
int findPairs(vector<int>& nums, int k) {
    if(k<0) return 0;
    unordered_map<int, int> map;
    int res = 0;
    for(auto num : nums)
        map[num]++;
    for(auto num : nums)
    {
        if(k==0)
        {
            if(map[num]>1) res++;
        }
        else if(map[num] > 0)
        {
            if(map[num-k]>0) res++;
            if(map[num+k]>0) res++;
        }
        map[num]=0;
    }
    return res;
}
```

Note the question is asking for `unique k-diff pairs`.

Corner cases: `k<0` and `k==0`

1. Count the numbers of `nums` in a map.
2. Check `num-k` and `num+k` in the map.
3. Don't forget to remove the `num` in the map after checking it.

**Complexity:**

* **worst-case time complexity:** `O(n)`, where `n` is the length of the input `nums`.
* **worst-case space complexity:** `O(n)`, where `n` is the length of the input `nums`.
