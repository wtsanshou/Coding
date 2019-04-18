# Codility. Min Avg Two Slice

### Codility

### Question

A non-empty zero-indexed array A consisting of N integers is given. A pair of integers (P, Q), such that 0 ≤ P < Q < N, is called a slice of array A (notice that the slice contains at least two elements). The average of a slice (P, Q) is the sum of A[P] + A[P + 1] + ... + A[Q] divided by the length of the slice. To be precise, the average equals (A[P] + A[P + 1] + ... + A[Q]) / (Q − P + 1).

For example, array A such that:

`A[0] = 4 A[1] = 2 A[2] = 2 A[3] = 5 A[4] = 1 A[5] = 5 A[6] = 8`

contains the following example slices:

* slice (1, 2), whose average is (2 + 2) / 2 = 2;
* slice (3, 4), whose average is (5 + 1) / 2 = 3;
* slice (1, 4), whose average is (2 + 2 + 5 + 1) / 4 = 2.5.

The goal is to find the starting position of a slice `whose average is minimal`.

**Write a function:**

`int solution(vector<int> &A);`

that, given a non-empty zero-indexed array A consisting of N integers, returns the starting position of the slice with the minimal average. If there is more than one slice with a minimal average, you should return the smallest starting position of such a slice.

For example, given array A such that:

`A[0] = 4 A[1] = 2 A[2] = 2 A[3] = 5 A[4] = 1 A[5] = 5 A[6] = 8`

the function should return 1, as explained above.

**Assume that:**

* N is an integer within the range [2..100,000];
* each element of array A is an integer within the range [−10,000..10,000].

**Complexity:**

* expected worst-case time complexity is O(N);
* expected worst-case space complexity is O(N), beyond input storage (not counting the storage required for input arguments).

Elements of input arrays can be modified.

## Solutions

### Solution 1

* Java
```
public int solution(int[] A) {
    int n = A.length;
    int[] accSum = new int[n+1];
    for(int i=1; i<=n; ++i)
        accSum[i] = accSum[i-1] + A[i-1];
    
    double minAve = Integer.MAX_VALUE;
    int res = 0;
    for(int i=0; i<n-1; ++i){
        for(int j=i+2; j<=n; ++j){
            double ave = (double)(accSum[j] - accSum[i]) / (double)(j-i);
            if(ave < minAve){
                minAve = ave;
                res = i;
            }
        }
    }
    return res;
}
```

Count the prefix sum of each element in the `A`. (**Note:** the sum value could be beyond the `Integer.MAX_VALUE`.) 

Check all possible average to find the minimum average.

* **worst-case time complexity:** O(N<sup>2</sup>), where `N` is length of `A`.
* **worst-case space complexity:** `O(N)`.

### Solution 2

* Java (Improve)
```
public int solution(int[] A) {
    int n = A.length;
    int[] accSum = new int[n+1];
    for(int i=1; i<=n; ++i){
        accSum[i] = accSum[i-1] + A[i-1];
    }
    
    double minAve = Integer.MAX_VALUE;
    int res = 0;
    for(int i=0; i<n-1; ++i){
        for(int j=i+2; j<=n && j<=i+3; ++j){
            double ave = (double)(accSum[j] - accSum[i]) / (double)(j-i);
            if(ave < minAve){
                minAve = ave;
                res = i;
            }
        }
    }
    return res;
}
```

Check only 2 or 3 number of average to find the minimum average.

* **worst-case time complexity:** `O(N)`, where `N` is length of `A`.
* **worst-case space complexity:** `O(N)`.

### Solution 3

* C++ (100%)
```
int solution(vector<int> &A) {
    int n=A.size();
    vector<double> sum2(n);
    for(int i=0; i<n-1; ++i)
    {
        sum2[i] = (double)(A[i]+A[i+1])/2; 
        if(i+2<n) sum2[i] = min(sum2[i], (double)(A[i]+A[i+1]+A[i+2])/3);
    }
    double minA=10001, start=-1;
    for(int i=0; i<n-1; ++i)
    {
        if(sum2[i] < minA)
        {
            minA = sum2[i];
            start = i;
        }
    }
    return start;
}
```

Only record the minimum of 2 or 3 number of average in each element in `A`.

Then find the minimum average.

* **worst-case time complexity:** `O(N)`, where `N` is length of `A`.
* **worst-case space complexity:** `O(N)`.

### Solution 4

* C++2 (O(1)space)
```
int solution(vector<int> &A) {
    int n=A.size();
    float minA=10001, start=-1;
    for(int i=0; i<n-1; ++i)
    {
        float temp = (float)(A[i]+A[i+1])/2; 
        if(i+2<n) temp = min(temp, (float)(A[i]+A[i+1]+A[i+2])/3);
        
        if(temp < minA)
        {
            minA = temp;
            start = i;
        }
    }
    return start;
}
```

Only check the minimum of 2 or 3 number of average in each element in `A`.

Keep checking the minimum average.

* **worst-case time complexity:** `O(N)`, where `N` is length of `A`.
* **worst-case space complexity:** `O(1)`.

## Testcase

double_quadruple 

two or four elements


simple1 

simple test, the best slice has length 3


simple2 

simple test, the best slice has length 3


small_random 

random, length = 100


medium_range 

increasing, decreasing (legth = ~100) and small functional


medium_random 

random, N = ~700


large_ones 

numbers from -1 to 1, N = ~100,000


large_random 

random, N = ~100,000


extreme_values 

all maximal values, N = ~100,000


large_sequence 

many seqeneces, N = ~100,000

