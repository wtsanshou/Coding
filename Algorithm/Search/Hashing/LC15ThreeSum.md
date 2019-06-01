# LC15. Three Sum

### LeetCode

## Question

Given an array S of n integers, are there elements a, b, c in S such that a + b + c = 0? Find all unique triplets in the array which gives the sum of zero.

**Note:** The solution set must not contain duplicate triplets.

**For example,** 
```
given array S = [-1, 0, 1, 2, -1, -4],

A solution set is:
[
  [-1, 0, 1],
  [-1, -1, 2]
]
```

## Solutions

### Solution 1

* C++
```
vector<vector<int>> threeSum(vector<int>& nums) {
    int n = nums.size();
    vector<vector<int>> res;
    
    if(n<3) return res; 
    vector<int> triplet(3);
    sort(nums.begin(), nums.end());
    
    for(int i1=0; i1<n-2; ++i1)
    {
        while(i1>0 && i1<n-2 && nums[i1]==triplet[0]) i1++;
        triplet[0] = nums[i1];
        int i=i1+1, j=n-1;
        while(i<j)
        {
            int sum = nums[i] + nums[j];
            if(sum == -triplet[0])
            {
                triplet[1] = nums[i++];
                triplet[2] = nums[j--];
                res.push_back(triplet);
                while(i<j && nums[i]==triplet[1]) i++;
                while(j>i && nums[j]==triplet[2]) j--;
            } 
            else if(sum < -triplet[0]) i++;
            else j--;
        }
    }
    return res;
}
```

* C++
```
vector<vector<int>> threeSum(vector<int>& nums) {
    vector<vector<int>> res;
    vector<int> arow(3);
    sort(nums.begin(), nums.end());
    int sum, left, right, target,n = nums.size();
    for(int i=0; i<n-2; ++i)
    {
        while(i>0 && i<n-2 && nums[i]==arow[0]) i++;
        target = -nums[i];
        if(target<0) return res;
        arow[0] = nums[i];
        left = i+1;
        right = n-1;
        while(left<right)
        {
            sum = nums[left] + nums[right];
            arow[1] = nums[left];
            arow[2] = nums[right];
            if(sum==target) 
            {
                res.push_back(arow);
                while(left<right && nums[++left]==arow[1]);
                while(left<right && nums[--right]==arow[2]);
            }
            else if(sum<target) 
            {
                while(left<right && nums[++left]==arow[1]); 
            }
            else 
            {
                while(left<right && nums[--right]==arow[2]);
            }
        }
    }
    return res;
}
```

1. Sort the `nums`
2. Based on the first element of the triplets, check if there are two numbers such that they add up to the target (see <a href="LC167TwoSumII-InputArrayIsSorted.md">LC167. Two Sum II - Input array is sorted</a>).

**Note** you need to skip the duplicated numbers.

**Complexity:**

* **worst-case time complexity:** O(n<sup>2</sup>), where `n` is the length of the input `nums`.
* **worst-case space complexity:** `O(log(n))`, where `n` is the length of the input `nums`.
