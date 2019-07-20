# Lint74. First Bad Version

### LintCode

## Question

The code base version is an integer start from 1 to n. One day, someone committed a bad version in the code case, so it caused this version and the following versions are all failed in the unit tests. Find the first bad version.

You can call isBadVersion to help you determine which version is the first bad one. The details interface can be found in the code's annotation part.

**Example**
```
Given n = 5:

    isBadVersion(3) -> false
    isBadVersion(5) -> true
    isBadVersion(4) -> true

Here we are 100% sure that the 4th version is the first bad version.
```

**Challenge**

* You should call isBadVersion as few as possible.

**Notice**

* Please read the annotation in code area to get the correct way to call isBadVersion in different language. For example, Java is SVNRepo.isBadVersion(v)

## Soluitons

### Solution 1

* Java
```
public int findFirstBadVersion(int n) {
    int i = 1, j = n;
    
    while (i < j) {
        int mid = i + (j - i) / 2;
        if (SVNRepo.isBadVersion(mid))
            j = mid;
        else
            i = mid + 1;
    }
    
    return i;
}
```

Straight forward binary search. **NOTE** here is `i < j` no equal included.

**Complexity:**

* **worst-case time complexity:** `O(log(n))`.
* **worst-case space complexity:** `O(1)`.
