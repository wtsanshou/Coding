# LC18. Four Sum

### LeetCode

## Question

Given an array S of n integers, are there elements a, b, c, and d in S such that a + b + c + d = target? Find all unique quadruplets in the array which gives the sum of target.

**Note:** The solution set must not contain duplicate quadruplets.

**For example** 
```
given array S = [1, 0, -1, 0, -2, 2], and target = 0.

A solution set is:
[
  [-1,  0, 0, 1],
  [-2, -1, 1, 2],
  [-2,  0, 0, 2]
]
```

## Solutions

### Solution 1

* C++
```
vector<vector<int>> fourSum(vector<int>& nums, int target) {
    vector<vector<int>> res;
    int size= nums.size();
    if(size < 4) return res;
    sort(nums.begin(), nums.end());
    int aRow[4] = {nums[0], nums[1],nums[2],nums[3]};
    for(int i1=0; i1<size-3;++i1)
    {
        while(i1!=0 && i1<size-3 && nums[i1]==aRow[0]) i1++;
        aRow[0] = nums[i1];
        aRow[1] = nums[i1+1];
        for(int i2=i1+1; i2<size-2; ++i2)
        {
            while(i2!=i1+1 && i2<size-2 && nums[i2]==aRow[1]) i2++;
            aRow[1] = nums[i2];
            int i3=i2+1, i4=size-1;
            while(i3<i4)
            {
                int sum = nums[i1] + nums[i2] +nums[i3] + nums[i4];
                if(sum == target)
                {
                    aRow[2] = nums[i3];
                    aRow[3] = nums[i4];
                    res.push_back(vector<int>(aRow, aRow+4));
                    while(i3<size-1 && nums[i3]==aRow[2]) i3++;
                    while(i4>i2+1 && nums[i4]==aRow[3]) i4--;
                }
                else if(sum < target) i3++;
                else i4--;
            }
        }
    }
    return res;
}
```

* C++
```
vector<vector<int>> fourSum(vector<int>& nums, int target) {
    vector<vector<int>> res;
    vector<int> arow(4);
    sort(nums.begin(),nums.end());
    int sum, third, fouth, n = nums.size();
    for(int first=0; first<n-3; ++first)
    {
        while(first>0 && nums[first]==arow[0]) ++first;
        arow[0] = nums[first];
        if(nums[first]+nums[first+1]+nums[first+2]+nums[first+3]>target) break;
        if(nums[first]+nums[n-3]+nums[n-2]+nums[n-1]<target) continue;
        for(int second=first+1; second<n-2; ++second)
        {
            while(second>first+1 && nums[second]==arow[1]) ++second;
            arow[1] = nums[second];
            if(nums[first]+nums[second]+nums[second+1]+nums[second+2]>target) break;
            if(nums[first]+nums[second]+nums[n-2]+nums[n-1]<target) continue;
            third = second+1;
            fouth = n-1;
            while(third<fouth)
            {
                sum = nums[first]+nums[second]+ nums[third]+nums[fouth];
                arow[2] = nums[third];
                arow[3] = nums[fouth];
                if(sum==target)
                {
                    res.push_back(arow);
                    while(third<fouth && nums[++third]==arow[2]);
                    while(third<fouth && nums[--fouth]==arow[3]);
                }
                else if(sum<target) ++third;
                else --fouth;
            }
        }
    }
    return res;
}
```

Similar with the Question <a href="LC15ThreeSum.md">LC15. Three Sum</a>, just add one more layer.

**Complexity:**

* **worst-case time complexity:** O(n<sup>3</sup>), where `n` is the length of the input `nums`.
* **worst-case space complexity:** `O(log(n))`, where `n` is the length of the input `nums`.