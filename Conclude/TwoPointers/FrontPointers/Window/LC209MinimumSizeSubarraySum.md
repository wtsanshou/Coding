# LC209. Minimum Size Subarray Sum

### LeetCode

## Question

Given an array of n positive integers and a positive integer s, find the minimal length of a contiguous subarray of which the `sum ≥ s`. If there isn't one, return 0 instead.

**For example,** 
```
given the array [2,3,1,2,4,3] and s = 7,
the subarray [4,3] has the minimal length under the problem constraint.
```

**More practice:**

* If you have figured out the O(n*log(n) solution, try coding another solution of which the time complexity is O(n).

## Solutions

### Solution 1

* C++ 
```
int minSubArrayLen(int s, vector<int>& nums) {
    int n = nums.size();
    if(n==0 || s==0) return 0;
    int res = n+1;
    int sum = 0; //?
    for(int i=0; i<n; ++i)
        sum[i+1] = sum[i]+nums[i]; //?
    for(int i=0; i<n; ++i)
    {
        int left = i+1;
        int right = n;
        while(left <= right)
        {
            int mid = left + (right-left)/2;
            if(sum[mid]-sum[i] >= s)
            {
                res = min(res, mid-i);
                right = mid-1;
            }
            else 
                left = mid+1;
        }
    }
    return res==n+1 ? 0 : res;
}
```

1. Get the prefix sums
2. Using binary search to find the minimum length of a contiguous subarray of which the `sum ≥ s` starting from each location of element.

**Complexity:**

* **worst-case time complexity:** O(n*log(n)), where `n` is length of `nums`.
* **worst-case space complexity:** `O(1)`.

### Solution 2

* C++
```
int minSubArrayLen(int s, vector<int>& nums) {
    int sum =0, start=0, minLen = INT_MAX;
    for(int i=0; i<nums.size(); ++i)
    {
        sum+=nums[i];
        while(sum>=s)
        {
            minLen = min(minLen, i-start+1);
            sum -= nums[start++];
        }
    }
    return minLen==INT_MAX ? 0:minLen;
}
```

Check the minimum length of a contiguous subarray of which the `sum ≥ s` when getting the prefix sums. 

when `sum ≥ s`, minus the front elements in the sum until `sum < s`. Make it ready for next check.

**Complexity:**

* **worst-case time complexity:** O(n), where `n` is length of `nums`.
* **worst-case space complexity:** `O(1)`.

### Solution 3

* Java1 O(n*log(n))
public class Solution {
    public int minSubArrayLen(int s, int[] nums) {
        int i = 1, j = nums.length, min = 0;
        while (i <= j) {
            int mid = (i + j) / 2;
            if (windowExist(mid, nums, s)) {
                j = mid - 1;
                min = mid;
            } else i = mid + 1;
        }
        return min;
    }

//check if has sum with sum >= s in array nums
    private boolean windowExist(int size, int[] nums, int s) {
        int sum = 0;
        for (int i = 0; i < nums.length; i++) {
            if (i >= size) sum -= nums[i - size];
            sum += nums[i];
            if (sum >= s) return true;
        }
        return false;
    }
}

Using `mid` to represent the size of checked window. 

If found a window with size `mid` who has `sum ≥ s`, then check the smaller size (from `i` to `j = mid - 1`).

If not found a window with size `mid` who has `sum ≥ s`, then check the larger size (from `i = mid + 1` to `j`).

**Complexity:**

* **worst-case time complexity:** O(n*log(n)), where `n` is length of `nums`.
* **worst-case space complexity:** `O(1)`.

### Solution 4

* Java
```
public int minimumSize(int[] nums, int s) {
    int minSize = Integer.MAX_VALUE;
    
    for (int i = 0; i < nums.length; i++) {
        for (int j = i + 1; j <= nums.length; j++) {
            int sum = 0;
            for (int mid = i; mid < j; mid++) {
                sum += nums[mid];
                if (sum >= s) {
                    minSize = Math.min(minSize, j - i);
                    break;
                }
            }
        }
    }
    
    return minSize == Integer.MAX_VALUE ? -1 : minSize;
}
```

The brute force solution, check all possible sub array.

**Complexity:**

* **worst-case time complexity:** O(n<sup>3</sup>)), where `n` is length of `nums`.
* **worst-case space complexity:** `O(1)`.

### Solution 5

* Java
```
public int minimumSize(int[] nums, int s) {
    int minSize = Integer.MAX_VALUE;
    
    for (int i = 0; i < nums.length; i++) {
        for (int j = i + 1; j <= nums.length; j++) {
            int sum = 0;
            for (int mid = i; mid < j && sum < s; mid++) {
                sum += nums[mid];
            }
            if (sum >= s) {
                minSize = Math.min(minSize, j - i);
                break;
            }
        }
    }
    
    return minSize == Integer.MAX_VALUE ? -1 : minSize;
}
```

Base on **Solution 4**, when get `sum >= s`, there is no need to add more element into the `sum`.

**Complexity:**

* **worst-case time complexity:** O(n<sup>2</sup>)), where `n` is length of `nums`.
* **worst-case space complexity:** `O(1)`.

### Solution 6

* Java
```
public int minimumSize(int[] nums, int s) {
    int sum = 0, j = 0;
    int minSize = Integer.MAX_VALUE;
    for (int i = 0; i < nums.length; i++) {
        while (sum < s && j < nums.length)
            sum += nums[j++];
        
        if (sum >= s)
            minSize = Math.min(minSize, j - i);
        
        sum -= nums[i];
    }
    
    return minSize == Integer.MAX_VALUE ? -1 : minSize;
}
```

Finally, we can find that there is no need to re-calculate the element from `i + 1` to `j`. We don't need to put `j` back.

So, we can use the template:

```
for (int i = 0; i < n; i++) {
    while (j < n) {
        if (meet the condition) {
            j++;
            update state;
        } else {
            break;
        }
    }

    update state;
}
```

**Complexity:**

* **worst-case time complexity:** O(n), where `n` is length of `nums`.
* **worst-case space complexity:** `O(1)`.