# LC453. Minimum Moves to Equal Array Elements

### LeetCode

## Question

Given a `non-empty` integer array of size `n`, find the minimum number of moves required to make all array elements equal, where `a move` is incrementing `n - 1 `elements by `1`.

**Example:**
```
Input:
[1,2,3]

Output:
3

Explanation:
Only three moves are needed (remember each move increments two elements):

[1,2,3]  =>  [2,3,3]  =>  [3,4,3]  =>  [4,4,4]
```

## Solutions

### Solution 1

* C++1 (63ms)
```
int minMoves(vector<int>& nums) {
    int minmum = INT_MAX, sum=0;
    for(int n : nums)
    {
        minmum = min(minmum, n);
        sum += n;
    }
    return sum - nums.size()*minmum;
}
```

* C++2 (69ms)
```
int minMoves(vector<int>& nums) {
    int minN = INT_MAX;
    int res = 0;
    for(int num : nums)
        minN = min(minN, num);
    
    for(int num : nums)
        res += num - minN;
    
    return res;
}
```

We can reverse thinking of the `a move is incrementing n - 1 elements by 1` as `a move is decrementing 1 element by 1`. Then that's easy to get the number of moves.

* **worst-case time complexity:** `O(n)`, where `n` is the length of the `nums`.
* **worst-case space complexity:** `O(1)`
