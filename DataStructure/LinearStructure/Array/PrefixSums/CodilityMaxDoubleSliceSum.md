# Codility. Max Double Slice Sum

### Codility

## Question

A non-empty zero-indexed array A consisting of N integers is given.

A triplet (X, Y, Z), such that 0 ≤ X < Y < Z < N, is called a double slice.
The sum of double slice (X, Y, Z) is the total of A[X + 1] + A[X + 2] + ... + A[Y − 1] + A[Y + 1] + A[Y + 2] + ... + A[Z − 1].

For example, array A such that:

`A[0] = 3 A[1] = 2 A[2] = 6 A[3] = -1 A[4] = 4 A[5] = 5 A[6] = -1 A[7] = 2`

contains the following example double slices:

* double slice (0, 3, 6), sum is 2 + 6 + 4 + 5 = 17,
* double slice (0, 3, 7), sum is 2 + 6 + 4 + 5 − 1 = 16,
* double slice (3, 4, 5), sum is 0.

The goal is to find the maximal sum of any double slice.

**Write a function:**

`int solution(vector<int> &A);`

that, given a non-empty zero-indexed array A consisting of N integers, returns the maximal sum of any double slice.

**For example, given:**
```
A[0] = 3 A[1] = 2 A[2] = 6 A[3] = -1 A[4] = 4 A[5] = 5 A[6] = -1 A[7] = 2

the function should return 17, because no double slice of array A has a sum of greater than 17.
```

**Assume that:**

* N is an integer within the range [3..100,000];
* each element of array A is an integer within the range [−10,000..10,000].


•	expected worst-case time complexity is O(N);
•	expected worst-case space complexity is O(N), beyond input storage (not counting the storage required for input arguments).

Elements of input arrays can be modified.

## Solutions

### Solution 1

* C++
```
int solution(vector<int> &A) {
    int n = A.size();
    A[0] = A[n-1] = 0;
    vector<int> lSum(n-2);
    vector<int> rSum(n-2);
    for(int i=1; i<n-2; ++i)
    {
        lSum[i] = max(lSum[i-1]+A[i], 0);
        rSum[n-i-3] = max(rSum[n-i-2]+A[n-i-1], 0);
    }
    int res = 0;
    for(int i=0; i<n-2; ++i)
        res = max(res, lSum[i]+rSum[i]);
    return res;
}
```

* Java
```
public int solution(int[] A) {
    int n = A.length;
    int[] lSum = new int[n];
    int[] rSum = new int[n];
    for(int i=1; i<n-2; i++) //only left: skip the most two right
        lSum[i] = Math.max(lSum[i-1]+A[i], 0);
    
    for(int i=n-2; i>1; i--) //only right: skip the most two left
        rSum[i] = Math.max(rSum[i+1]+A[i], 0);
    
    int res = 0;
    for(int i=0; i<n-2; i++){
        res = Math.max(res, lSum[i]+rSum[i+2]);
    }
    return res;
}
```

Using two array, one for memorying the maximum sum of left elements `lSum`; one for memorying the maximum sum of right elements `rSum`.

**Complexity:**

* **worst-case time complexity:** `O(N)`, where `N` is length of `A`.
* **worst-case space complexity:** `O(N)`, where `N` is length of `A`.

## Testcase

simple3 

third simple test


negative 

all negative numbers


positive 

all positive numbers


extreme_triplet 

three elements


small_random1 

random, numbers form -10**4 to 10**4, length = 70


small_random2 

random, numbers from -30 to 30, length = 300


medium_range 

-1000, ..., 1000


large_ones 

random numbers from -1 to 1, length = ~100,000


large_random 

random, length = ~100,000


extreme_maximal 

all maximal values, length = ~100,000   be careful it could be overflow if values are bigger


large_sequence 

many the same small sequences, length = ~100,000

