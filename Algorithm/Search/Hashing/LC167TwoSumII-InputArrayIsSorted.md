# LC167. Two Sum II - Input array is sorted 

### LeetCode

## Question

Given an array of integers that is already sorted in ascending order, find two numbers such that they add up to a specific target number.

The function twoSum should return indices of the two numbers such that they add up to the target, where index1 must be less than index2. Please note that your returned answers (both index1 and index2) are not zero-based.

You may assume that each input would have exactly one solution and you may not use the same element twice.

```
Input: numbers={2, 7, 11, 15}, target=9
Output: index1=1, index2=2
```

## Solution

### Solution 1

* C++ (6ms)
```
vector<int> twoSum(vector<int>& numbers, int target) {
    vector<int> res(2);
    int i=0, j=numbers.size()-1;
    while(i<j)
    {
        int sum = numbers[i] + numbers[j];
        if(sum == target)
        {
            res[0] = i+1;
            res[1] = j+1;
            return res;
        }
        else if(sum > target) j--;
        else i++;
    }
    return res;
}
```

If the sum of minimum and maximum is smaller than the target, the minimum is useless for the reulst.

If the sum of minimum and maximum is larger than the target, the maximum is useless for the reulst.

**Complexity:**

* **worst-case time complexity:** `O(n)`, where `n` is the length of the input `numbers`.
* **worst-case space complexity:** `O(1)`.

### Solution 2

Could be solved by Hashing as well.

**Complexity:**

* **worst-case time complexity:** `O(n)`, where `n` is the length of the input `numbers`.
* **worst-case space complexity:** `O(n)`, where `n` is the length of the input `numbers`.