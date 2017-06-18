# LC611. Valid Triangle Number

### LeetCode

## Question

Given an array consists of non-negative integers, your task is to count the number of triplets chosen from the array that can make triangles if we take them as side lengths of a triangle.

**Example 1:**

**Input:** 
```
[2,2,3,4]
```

**Output:** 
```
3
```

**Explanation:**

Valid combinations are: 
```
2,3,4 (using the first 2)
2,3,4 (using the second 2)
2,2,3
```

**Note:**

* The length of the given array won't exceed 1000.
* The integers in the given array are in the range of [0, 1000].

## Solutions

* C++1
```
int triangleNumber(vector<int>& nums) {
        sort(nums.begin(), nums.end());
        int res = 0, n = nums.size();
        for(int i=0; i<n-2; ++i)
        {
            if(nums[i] == 0) continue;
            int a = nums[i];
            for(int j=i+1; j<n-1; ++j)
            {
                int aAddb = a + nums[j];
                int L = j+1, R = n;
                while(L < R)
                {
                    int mid = L + (R-L)/2;
                    if(aAddb > nums[mid])
                        L = mid+1;
                    else
                        R = mid;
                }
                res += L-j-1;
            }
        }
        return res;
    }
```

## Explanation

This question is similar with the question <a>3Sum</a> which is to find `a+b+c=0`.

The key knowledge here is: `if the sum of two small edges a & b is larger than the largest edge c, we can see a, b, and c can be a triangle`

We can sort the array. So that, we can compare the sum of two small deges and the larger edge. 

Because the array is sorted, for the third edge, all possible avaible third edge are in the left of the array. So, we can use Binary Search to find the boundary point. The values left of the boundary point are we need to count.

* **worst-case time complexity:** O(n<sup>2</sup>log(n))
* **worst-case space complexity:** O(n)