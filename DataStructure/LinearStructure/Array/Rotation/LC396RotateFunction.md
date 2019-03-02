# LC396. Rotate Function

## LeetCode

## Question

Given an array of integers A and let n to be its length.

Assume Bk to be an array obtained by rotating the array A k positions clock-wise, we define a "rotation function" F on A as follow:

`F(k) = 0 * Bk[0] + 1 * Bk[1] + ... + (n-1) * Bk[n-1].`

Calculate the maximum value of F(0), F(1), ..., F(n-1).

**Note:**

* n is guaranteed to be less than 105.

**Example:**
```
A = [4, 3, 2, 6]

F(0) = (0 * 4) + (1 * 3) + (2 * 2) + (3 * 6) = 0 + 3 + 4 + 18 = 25
F(1) = (0 * 6) + (1 * 4) + (2 * 3) + (3 * 2) = 0 + 4 + 6 + 6 = 16
F(2) = (0 * 2) + (1 * 6) + (2 * 4) + (3 * 3) = 0 + 6 + 8 + 9 = 23
F(3) = (0 * 3) + (1 * 2) + (2 * 6) + (3 * 4) = 0 + 2 + 12 + 12 = 26

So the maximum value of F(0), F(1), F(2), F(3) is F(3) = 26.
```

## Solutions

### Solution 1

* C++
```
int maxRotateFunction(vector<int>& A) {
    int sum=0, F=0, n=A.size();
    for(int i=0; i<n; ++i)
    {
        sum += A[i];
        F += i*A[i];
    }
    int res = F;
    for(int i=1; i<n; ++i)
    {
        F += sum - n*A[n-i];
        res = max(res, F);
    }
    return res;
}
```

The value of each rotation `=` previous function value `+` the sum of original numbers `-` (previous last number * n).

```
sum = 4 + 3 + 2 + 6 = 15 
F(0) = (0 * 4) + (1 * 3) + (2 * 2) + (3 * 6) = 0 + 3 + 4 + 18 = 25
                 
F(1) = (0 * 6) + (1 * 4) + (2 * 3) + (3 * 2) = 0 + 4 + 6 + 6 = 16           
                 (1 * 4) + (1 * 3) + (1 * 2) + (1 * 6)       = sum      = 15
               + (0 * 4) + (1 * 3) + (2 * 2) + (3 * 6)       = F(0)     = 25
               -                               (4 * 6)       = n*A[n-i] = 24
```

* **worst-case time complexity:** `O(N)`, where `N` is the size of the input `A`.
* **worst-case space complexity:** `O(1)`