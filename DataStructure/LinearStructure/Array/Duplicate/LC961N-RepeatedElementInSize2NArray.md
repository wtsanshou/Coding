# LC961. N-Repeated Element in Size 2N Array

### LeetCode

## Question

In a array A of size 2N, there are N+1 unique elements, and exactly one of these elements is repeated N times.

Return the element repeated N times.

**Example 1:**
```
Input: [1,2,3,3]
Output: 3
```

**Example 2:**
```
Input: [2,1,2,5,3,2]
Output: 2
```

**Example 3:**
```
Input: [5,1,5,2,5,3,5,4]
Output: 5
``` 

**Note:**

* 4 <= A.length <= 10000
* 0 <= A[i] < 10000
* A.length is even

## Solutions

* Java1
```
public int repeatedNTimes(int[] A) {
    boolean[] map = new boolean[10000];
    for(int a : A){
        if(map[a]) return a;
        map[a] = true;
    }
    return A[0];
}
```

* Java2
```
public int repeatedNTimes(int[] A) {
    Set<Integer> map = new HashSet<>();
    for(int a : A){
        if(map.contains(a)) return a;
        map.add(a);
    }
    return 0;
}
```

## Explanation

Based on the Note, we can conclude that only the element repeated N times is duplicated. Therefore, the question become to find a element that is duplicated.

* **worst-case time complexity:** O(n)
* **worst-case space complexity:** O(1)

