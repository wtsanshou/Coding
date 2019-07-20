# Lint63. Search in Rotated Sorted Array II

Follow up for Search in Rotated Sorted Array:

What if duplicates are allowed?

Would this affect the run-time complexity? How and why?

Write a function to determine if a given target is in the array.

**Example 1:**
```
Input:
[]
1

Output:
false
```

**Example 2:**
```
Input:
[3,4,4,5,7,0,1,2]
4

Output:
true
```

## Solutions

### Solution 1

* Java
```
public class Solution {
    /**
     * @param A: an integer ratated sorted array and duplicates are allowed
     * @param target: An integer
     * @return: a boolean 
     */
    public boolean search(int[] A, int target) {
        return search(A, target, 0, A.length - 1);
    }
    
    private boolean search(int[] A, int target, int i, int j) {
        if (i > j) return false;
        
        int mid = i + (j - i) / 2;
        
        if (A[mid] == target)
            return true;
        else {
            if (A[mid] == A[i] && A[mid] == A[j]) {
                return search(A, target, i, mid - 1) || search(A, target, mid + 1, j);
            } else if (A[i] <= A[mid]) {
                if (A[i] <= target && target < A[mid])
                    return search(A, target, i, mid - 1);
                else
                    return search(A, target, mid + 1, j);
            } else {
                if (A[mid] < target && target <= A[j])
                    return search(A, target, mid + 1, j);
                else
                    return search(A, target, i, mid - 1);
            }
        }
    }
}
```

I am sure it's using binary search. But at the beginning, I did not think of recursive. I was tring to use iteration to solve it, but could not figure it out. So I came out the recursive solution first. 

I have to exclude the corner cases one by one:

**Corner Case 1**

`A[mid] == A[i] && A[mid] == A[j]`

```
Input:
[3, 1, 3, 3, 3]
1

Output:
true
```

```
Input:
[3, 3, 3, 1, 3]
1

Output:
true
```

After this case, we can sure at least one side of the `mid` point is ordered. Then we can use binary search to narrow down the searching range.

**Complexity:**

* **worst-case time complexity:** `O(log(n))`, where `n` is the length of the input `A`.
* **worst-case space complexity:** `O(1)`.

### Solution 2

* Java
```
public boolean search(int[] A, int target) {
    int i = 0, j = A.length - 1;
    while (i <= j) {
        int mid = i + (j - i) / 2;
        if (A[mid] == target) 
            return true;
        else {
            int left = mid;
            while (left > 0 && A[left] == A[left - 1]) left--;
            if (left == 0) {
                i = mid + 1;
                continue;
            }
            
            int right = mid;
            while (right < A.length - 1 && A[right] == A[right + 1]) right++;
            if (right == A.length - 1){
                j = mid - 1;
                continue;
            }
            
            if (A[i] <= A[mid]) {
                if (A[i] <= target && target < A[mid])
                    j = mid - 1;
                else
                    i = mid + 1;
            } else {
                if (A[mid] < target && target <= A[j])
                    i = mid + 1;
                else 
                    j = mid - 1;
            }
            
        }
    }
    
    return false;
}
```

* Java
```
public boolean search(int[] A, int target) {
    int i = 0, j = A.length - 1;
    while (i <= j) {
        int mid = i + (j - i) / 2;
        if (A[mid] == target) 
            return true;
        else {
            int left = mid;
            while (left > 0 && A[left] == A[left - 1]) left--;
            int right = mid;
            while (right < A.length - 1 && A[right] == A[right + 1]) right++;
            
            if (left == 0) {
                i = right + 1;
                continue;
            }
            
            if (right == A.length - 1){
                j = left - 1;
                continue;
            }
            
            if (A[i] <= A[mid]) {
                if (A[i] <= target && target < A[mid])
                    j = left - 1;
                else
                    i = right + 1;
            } else {
                if (A[mid] < target && target <= A[j])
                    i = right + 1;
                else 
                    j = left - 1;
            }
            
        }
    }
    
    return false;
}
```

Based on the idea of **Solution 1**, we can apply it by iteration. We just need to check the **Corner Case 1**.

**Complexity:**

* **worst-case time complexity:** `O(n)`, where `n` is the length of the input `A`.
* **worst-case space complexity:** `O(1)`.
