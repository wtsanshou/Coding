# LC462. Minimum Moves to Equal Array Elements II

### LeetCode

## Question

Given a non-empty integer array, find the minimum number of moves required to make all array elements equal, where a move is incrementing a selected element by 1 or decrementing a selected element by 1.

You may assume the array's length is at most 10,000.

**Example:**
```
Input:
[1,2,3]

Output:
2

Explanation:
Only two moves are needed (remember each move increments or decrements one element):

[1,2,3]  =>  [2,2,3]  =>  [2,2,2]
```
## Solutions

### Solution 1

* C++ (19ms)
```
int minMoves2(vector<int>& nums) {
    int median = nums.size()/2, res = 0;
    nth_element(nums.begin(), nums.begin()+median, nums.end());
    for(int num : nums)
        res += abs(num - nums[median]);
    return res;
}
```

* Java (14ms)
```
public int minMoves2(int[] nums) {
    int res = 0;
    Arrays.sort(nums);
    int median = nums[nums.length/2];
    for(int num : nums)
        res += Math.abs(num- median);
    return res;
}
```

The idea is to find the `median value` in the array `nums`, then let all elements move to this `median value`.

* **worst-case time complexity:** `O(n*log(n))`, where `n` is the length of the `nums`.
* **worst-case space complexity:** `O(n*log(n))`, where `n` is the length of the `nums`.
