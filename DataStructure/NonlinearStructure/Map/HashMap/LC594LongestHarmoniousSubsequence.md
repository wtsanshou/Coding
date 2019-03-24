# LC594. Longest Harmonious Subsequence

### LeetCode

## Question

We define a harmonious array is an array where the difference between its maximum value and its minimum value is exactly 1.

Now, given an integer array, you need to find the length of its longest harmonious subsequence among all its possible subsequences.

**Example 1:**
```
Input: [1,3,2,2,5,2,3,7]
Output: 5
Explanation: The longest harmonious subsequence is [3,2,2,2,3].
```

**Note:** The length of the input array will not exceed 20,000.

## Solutions 

### Solution 1

* C++
```
int findLHS(vector<int>& nums) {
    map<int, int> count;
    int res=0;
    for(int num : nums)
        count[num]++;
    for(auto c : count)
        if(count.count(c.first + 1) > 0)
            res = max(res, c.second + count[c.first + 1]);
    return res;
}
```

* C++
```
int findLHS(vector<int>& nums) {
    map<int, int> count;
    int res=0;
    for(int num : nums)
        count[num]++;
    for(auto c = count.begin(); c!=count.end(); ++c)
        if(count.count(c->first + 1) > 0)
            res = max(res, c->second + count[c->first + 1]);
    return res;
}
```

Using a hashmap to count the number of each number in the `nums`.

Find the maximum sum of the count of adjacent number in the map.

* **worst-case time complexity:** `O(n)`, where `n` is the length of the `nums`.
* **worst-case space complexity:** `O(n)`, where `n` is the length of the `nums`.