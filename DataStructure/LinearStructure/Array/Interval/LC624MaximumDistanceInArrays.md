# LC624. Maximum Distance in Arrays

### LeetCode

## Question

Given m arrays, and each array is sorted in ascending order. Now you can pick up two integers from two different arrays (each array picks one) and calculate the distance. We define the distance between two integers a and b to be their absolute difference |a-b|. Your task is to find the maximum distance.

**Example 1:**

**Input:**
```
[[1,2,3],
 [4,5],
 [1,2,3]]
```

**Output:**
```
 4
```

**Explanation:** 

One way to reach the maximum distance 4 is to pick 1 in the first or third array and pick 5 in the second array.

**Note:**

* Each given array will have at least 1 number. There will be at least two non-empty arrays.
* The total number of the integers in all the m arrays will be in the range of [2, 10000].
* The integers in the m arrays will be in the range of [-10000, 10000].

## Solutions

* C++1
```
int maxDistance(vector<vector<int>>& arrays) {
        int minV=10001, maxV=-10001;
        int minId, maxId;
        int disMin=0, disMax=0;
        for(int i=0; i<arrays.size(); ++i)
        {
            if(arrays[i][0]<minV)
            {
                minV = arrays[i][0];
                minId = i;
            }
            if(arrays[i].back() > maxV)
            {
                maxV = arrays[i].back();
                maxId = i;
            }
        }
        for(int i=0; i<arrays.size(); ++i)
        {
            if(i!=minId)
                disMin = max(disMin, arrays[i].back()-minV);
            if(i!=maxId)
                disMax = max(disMax, maxV-arrays[i][0]);
        }
        return max(disMin, disMax);
    }
```

## Explanation

This question looks very simple, just to find the **maximum interval** i.e the minimum value and the maximum value in the arrays. but I did many mistakes:

1. I didn't notice the requirement `pick up two integers from two different arrays`.
2. Tried to find the results in one turn by checking which value can increase the **maximum interval** in an array. But I missed the corner case: both side value of a array may increase the same distances of the **maximum interval**.

Finally, I went to the correct way: find the maximum value and minimum value in the arrays. Record their index as well.

Based on the found maximum value and minimum value, check all the arrays to find the **maximum interval**.

## Lessons

1. Reading the question carefully
2. If cannot get right answer and have no idea in 15mins, go to next question. Come back later if I still have time.

