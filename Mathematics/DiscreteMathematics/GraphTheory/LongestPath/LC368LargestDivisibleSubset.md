## LC368. Largest Divisible Subset

### LeetCode

## Question

Given a set of distinct positive integers, find the largest subset such that every pair (Si, Sj) of elements in this subset satisfies: Si % Sj = 0 **or** Sj % Si = 0.

If there are multiple solutions, return any subset is fine.

**Example 1:**

`nums: [1,2,3]`

`Result: [1,2] (of course, [1,3] will also be ok)`

**Example 2:**

`nums: [1,2,4,8]`

`Result: [1,2,4,8]`

## Solutions

* C++1
```
vector<int> largestDivisibleSubset(vector<int>& nums) {
        sort(nums.begin(), nums.end());
        int n=nums.size(), start=0, maxSize=0;
        vector<int> link(n), linkLen(n), res;
        for(int i=n-1; i>=0; --i)
        {
            for(int j=i; j<n; ++j)
            {
                if(nums[j]%nums[i]==0 && linkLen[i] < 1+linkLen[j])
                {
                    linkLen[i] = 1+linkLen[j];
                    link[i] = j;
                }
            }
            if(linkLen[i] > maxSize)
            {
                maxSize = linkLen[i];
                start = i;
            }
        }
        for(int i=0; i<maxSize; ++i)
        {
            res.push_back(nums[start]);
            start=link[start];
        }
/*
vector<int> res(maxSize);
        for(int i=0; i<maxSize; ++i)
        {
            res[i] = nums[start];
            start = link[divi];
        }
*/
        return res;
    }
```

## Explanation

1. Sort the array, so that we just need to check `largeNum` mod `smallNum`
2. Connect the satisfied pair by array `link`, and record the length of each satisfied path.
3. Record the `starting point` of the `longest path`.
4. Based on the created links, search from the recorded `starting point`, find `all elements` of the `longest path`.

