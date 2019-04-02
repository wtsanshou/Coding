# Codility. Flood Depth

### Codility 

## Question

You are helping a geologist friend investigate an area with mountain lakes. A recent heavy rainfall has flooded these lakes and their water levels have reached the highest possible point. Your friend is interested to know the maximum depth in the deepest part of these lakes.

We simplify the problem in 2-D dimensions. The whole landscape can be divided into small blocks and described by an array A of length N. Each element of A is the altitude of the rock floor of a block (i.e. the height of this block when there is no water at all). After the rainfall, all the low-lying areas (i.e. blocks that have higher blocks on both sides) are holding as much water as possible. You would like to know the maximum depth of water after this entire area is flooded. You can assume that the altitude outside this area is zero and the outside area can accommodate infinite amount of water.

For example, consider array A such that:
```
A[0] = 1 A[1] = 3 A[2] = 2 A[3] = 1 A[4] = 2 A[5] = 1 A[6] = 5 A[7] = 3 A[8] = 3 A[9] = 4 A[10] = 2
```

The following picture illustrates the landscape after it has flooded:

The gray area is the rock floor described by the array A above and the blue area with dashed lines represents the water filling the low-lying areas with maximum possible volume. Thus, blocks 3 and 5 have a water depth of 2 while blocks 2, 4, 7 and 8 have a water depth of 1. Therefore, the maximum water depth of this area is 2.

**Write a function:**

`int solution(vector<int> &A);`

that, given a non-empty zero-indexed array A consisting of N integers, returns the maximum depth of water.

Given array A shown above, the function should return 2, as explained above.
For the following array:

`A[0] = 5 A[1] = 8`

the function should return 0, because this landscape cannot hold any water.
Assume that:

* N is an integer within the range [1..100,000];
* each element of array A is an integer within the range [1..100,000,000].

**Complexity:**

* expected worst-case time complexity is O(N);
* expected worst-case space complexity is O(N), beyond input storage (not counting the storage required for input arguments).

Elements of input arrays can be modified.

## Solutions

### Solution 1

* C++
```
int solution(vector<int> &A) {
    int n = A.size(), res = 0;
    vector<int> depths(n);
    int wall = A[0];
    for(int i=1; i<n-1; ++i)
    {
        if(A[i] > wall) wall = A[i];
        else depths[i] = wall - A[i];
    }
    
    wall = A[n-1];
    for(int i= n-2; i>0; --i)
    {
        if(A[i] > wall) 
        {
            wall = A[i];
            depths[i] = 0;
        }
        else depths[i] = min(wall-A[i], depths[i]);
        
        res = max(res, depths[i]);
    }
    return res;
}
```

1. travesal from left to right, with left highest wall as the reference, remember the depths of all possible lakes.
2. travesal from right to left, with right highest wall as the reference, update the depths of all possible lakes.

* **worst-case time complexity:** `O(n)`, where `n` is the length of the `A`.
* **worst-case space complexity:** `O(n)`, where `n` is the length of the `A`.

## Testcase

boundary 

max-min values and some random tests, N <= 15


triple_permutation 

all permutations of three elements [1, 2, 3]


small_functional 

small functional tests, N <= 15


small_random 

small random tests, N <= 100


multiple_valleys 

many small valleys, N <= 100


small_valley 

one small valley, N <= 100


medium_tests 

medium tests, N <= 600


big_random 

random arrays, N ~= 100,000


increasing_decreasing 

randomized values which grow when distance from the center decreases, N ~= 100,000


many_multiple_valleys 

many small valleys, N ~= 100,000


big_valley 

one big valley, N ~= 100,000


big_jagged 

one big valley with jagged slopes, N ~= 100,000

