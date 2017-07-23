# 645. Set Mismatch

### LeetCode

## Question

The set S originally contains numbers from 1 to n. But unfortunately, due to the data error, one of the numbers in the set got duplicated to another number in the set, which results in repetition of one number and loss of another number.

Given an array nums representing the data status of this set after the error. Your task is to firstly find the number occurs twice and then find the number that is missing. Return them in the form of an array.

**Example 1:**
```
Input: nums = [1,2,2,4]
Output: [2,3]
```

**Note:**

1.  The given array size will in the range [2, 10000].
2.  The given array's numbers won't have any order.

## Solutions

* C++1
```
vector<int> findErrorNums(vector<int>& nums) {
        int n = nums.size();
        vector<int> res(2), count(n);
        for(int num : nums)
            count[num-1]++;
        for(int i=1; i<=n; ++i)
        {
            if(count[i-1]==2) 
                res[0] = i;
            else if(count[i-1]==0)
                res[1] = i;
        }
        return res;
}
```

* Java1
```
public int[] findErrorNums(int[] nums) {
        int n = nums.length;
        int[] count = new int[n];
        int[] res = new int[2];
        for(int num : nums){
            count[num-1]++;
            if(count[num-1]==2)
                res[0] = num;
        }
        for(int i=0; i<n; ++i)
            if(count[i]==0){
                res[1] = i+1;
                break;
            }
        return res;
    }
```

## Explanation

* **worst-case time complexity:** O(n)
* **worst-case space complexity:** O(n)