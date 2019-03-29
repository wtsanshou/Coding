# Codility. Frog River One

### Codility

## Question

A small frog wants to get to the other side of a river. The frog is initially located on one bank of the river (position 0) and wants to get to the opposite bank (position X+1). Leaves fall from a tree onto the surface of the river.

You are given a zero-indexed array A consisting of N integers representing the falling leaves. A[K] represents the position where one leaf falls at time K, measured in seconds.

The goal is to find the earliest time when the frog can jump to the other side of the river. The frog can cross only when leaves appear at every position across the river from 1 to X (that is, `we want to find the earliest moment when all the positions from 1 to X are covered by leaves`). You may assume that the speed of the current in the river is negligibly small, i.e. the leaves do not change their positions once they fall in the river.

For example, you are given integer X = 5 and array A such that:

`A[0] = 1 A[1] = 3 A[2] = 1 A[3] = 4 A[4] = 2 A[5] = 3 A[6] = 5 A[7] = 4`

In second 6, a leaf falls into position 5. This is the earliest time when leaves appear in every position across the river.

Write a function:

`int solution(int X, vector<int> &A);`

that, given a non-empty zero-indexed array A consisting of N integers and integer X, returns the earliest time when the frog can jump to the other side of the river.

If the frog is never able to jump to the other side of the river, the function should return −1.

For example, given X = 5 and array A such that:

`A[0] = 1 A[1] = 3 A[2] = 1 A[3] = 4 A[4] = 2 A[5] = 3 A[6] = 5 A[7] = 4`

the function should return 6, as explained above.

**Assume that:**

* N and X are integers within the range [1..100,000];
* each element of array A is an integer within the range [1..X].

**Complexity:**

* expected worst-case time complexity is O(N);
* expected worst-case space complexity is O(X), beyond input storage (not counting the storage required for input arguments).

Elements of input arrays can be modified.

## Solutions

### Solution 1

* C++
```
int solution(int X, vector<int> &A) {
    // write your code in C++14 (g++ 6.2.0)
    vector<bool> bucket(X+1);
    int count=0, n = A.size();
    for(int i=0; i<n; ++i)
    {
        if(bucket[A[i]] == false)
        {
            bucket[A[i]] = true;
            count++;
            if(count == X)
                return i;
        }
    }
    return -1;
}
```

Starting from second `0`, count the unique leaves. When count reach number of `X`, the frog can pass the river.

* **worst-case time complexity:** O(N)
* **worst-case space complexity:** O(X)

### Solution 2

* Java
```
public frogRiverOne(int X, int[] A){
    int n = A.length;
    int[] minFall = new int[n+1];
    Arrays.fill(minFall, -1);
    for(int i=0; i<n; ++i)
        minFall[A[i]] = minFall[A[i]]==-1 ? i : Math.min(i, minFall[A[i]]);
    int res = -1;
    for(int mf : minFall){
        if(mf == -1) return -1;
        res = Math.max(res, mf);
    }
    return res;
}
```

Using an array to record the minimum fall time of each leaf. 

1. If missing a leaf, return `-1`
2. else, the final falling leaf when the first time all the positions from 1 to X are covered by leaves. The result if the time of the final falling leaf.

* **worst-case time complexity:** O(N)
* **worst-case space complexity:** O(X)


