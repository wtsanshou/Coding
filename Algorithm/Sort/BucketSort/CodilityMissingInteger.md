# Codility. Missing Integer

### Codility

## Question

Find the smallest positive integer that does not occur in a given sequence.

Task description

Write a function:

class Solution { public int solution(int[] A); }

that, given an array A of N integers, returns the smallest positive integer (greater than 0) that does not occur in A.

For example, given A = [1, 3, 6, 4, 1, 2], the function should return 5.

Given A = [1, 2, 3], the function should return 4.
Given A = [−1, −3], the function should return 1.

Assume that:

* N is an integer within the range [1..100,000];
* each element of array A is an integer within the range [−1,000,000..1,000,000].

Complexity:

* expected worst-case time complexity is O(N);
* expected worst-case space complexity is O(N), beyond input storage (not counting the storage required for input arguments).

Elements of input arrays can be modified.

## Solutions

* Java1
```
public int solution(int[] A) {
    int max = 100000;
    boolean[] occurs = new boolean[max];
    for(int a : A){
        if(a > 0 && a<=max) occurs[a-1] = true;   
    }
    for(int i=0; i<max; ++i){
        if(!occurs[i]) return i+1;   
    }
    return max+1;
}
```

* Java
```
public int solution(int[] A) {
    int n = A.length;
    boolean[] visit = new boolean[n+1];
    for(int a : A){
        if(a>0 && a<=n)
            visit[a] = true;
    }
    for(int i=1; i<=n; ++i)
        if(!visit[i]) return i;
    return n+1;
}
```

## Explanation

Complexity limitation are `time complexity is O(N)`, `space complexity is O(N)`.

**NOTE** N is an integer within the range `[1..100,000]`.

The element integer range is `[−1,000,000..1,000,000]`. If we use bucket sort directly, `1,000,000` is over the space complexity O(N).

But, the question ask to return the smallest positive integer (greater than 0). So the result must be in the range `[1, 100,001]`. If there are integers less than `0` or more than `100,000`, there must be at least one missed integer in the range `[1, 100,000]`. 

A corner case is A contains all positive integers from `1` to `100,000`. the result is `100,001`.

Therefore, the solution is just using a bucket with size of `100,000`. If found an integer in the bucket range, mark it. Then, check the bucket if any position is not marked.

## Testcase

a single element

minimal and maximal values

positive_only, shuffled sequence of 0...100 and then 102...200

negative_only, shuffled sequence -100 ... -1

chaotic sequences length=10005 (with minus)

chaotic + sequence 1, 2, ..., 40000 (without minus)

shuffled sequence 1, 2, ..., 100000 (without minus)

chaotic + many -1, 1, 2, 3 (with minus)



