# LC55. Jump Game

### LeetCode

## Question

Given an array of non-negative integers, you are initially positioned at the first index of the array.

Each element in the array represents your `maximum jump length` at that position.
Determine if you are able to reach the last index.

For example:


A = [2,3,1,1,4], return true.
A = [3,2,1,0,4], return false.

## Solutions

### Solution 1

* C++ (TLE)
```
class Solution {
public:
    bool canReachGoal(vector<int>& nums, vector<bool>& visited, int start, int& end)
    {
        if(start+nums[start] >=end-1) return true;
        visited[start] = true;
        bool res = false;
        for(int i=start+nums[start]; i>start; --i)
            if(visited[i]==false)
                res |= canReachGoal(nums, visited, i, end);
        return res;
    }
    bool canJump(vector<int>& nums) {
        int n = nums.size();
        vector<bool> visited(n);
        return canReachGoal(nums, visited, 0, n);
    }
};
```

Recursive way to visit all possible jump path.

**Complexity:**

* **worst-case time complexity:** `O(n<sup>2</sup>)`, where `n` is the length of the input `nums`.
* **worst-case space complexity:** `O(n)`, where `n` is the length of the input `nums`.

### Solution 2

* C++
```
bool canJump(vector<int>& nums) {
    int start = 0, maxJump = nums[0], len = nums.size();
    for(int i=1; i<len && i<=start+maxJump; ++i)
    {
        if(i-start+nums[i]>maxJump)
        {
            if(i+nums[i]>=len-1) return true;
            start = i;
            maxJump = nums[i];
        }
    }
    return start+maxJump>=len-1;
}
```

Notice Each element in the array represents your `maximum jump length` at that position. So always check the maximum reachable place. When found a longer reachable place, check if if you are able to reach the last index. Also update the maximum starting place and jump.

**Complexity:**

* **worst-case time complexity:** `O(n)`, where `n` is the length of the input `nums`.
* **worst-case space complexity:** `O(1)`.

### Solution 3

* Java
```
public boolean canJump(int[] nums){
    int lastId = nums.length-1;
    int maxReach = nums[0];

    for(int i=0; i<=lastId; i++){
        if(maxReach >= lastId) return true;
        if(nums[i] == 0 && maxReach<=i) return false;
        maxReach = Math.max(maxReach, i+nums[i]);
    }
    return maxReach >= lastId;
}
```

Always update the maximum reachable place. Only check possible unreachable when an element is `0` which means there is a chance you can not go further.

**Complexity:**

* **worst-case time complexity:** `O(n)`, where `n` is the length of the input `nums`.
* **worst-case space complexity:** `O(1)`.
