# Codility. Flags

### Codility

## Question

A non-empty zero-indexed array A consisting of N integers is given.

A peak is an array element which is larger than its neighbours. More precisely, it is an index P such that 0 < P < N − 1 and A[P − 1] < A[P] > A[P + 1].

For example, the following array A:

```
A[0] = 1 
A[1] = 5 
A[2] = 3 
A[3] = 4 
A[4] = 3 
A[5] = 4 
A[6] = 1 
A[7] = 2 
A[8] = 3 
A[9] = 4 
A[10] = 6 
A[11] = 2
```

has exactly four peaks: elements 1, 3, 5 and 10.

You are going on a trip to a range of mountains whose relative heights are represented by array A, as shown in a figure below. You have to choose how many flags you should take with you. The goal is to set the maximum number of flags on the peaks, according to certain rules.

Flags can only be set on peaks. What's more, if you take K flags, then the distance between any two flags should be greater than or equal to K. The distance between indices P and Q is the absolute value |P − Q|.

For example, given the mountain range represented by array A, above, with N = 12, if you take:

* two flags, you can set them on peaks 1 and 5;
* three flags, you can set them on peaks 1, 5 and 10;
* four flags, you can set only three flags, on peaks 1, 5 and 10.

You can therefore set a maximum of three flags in this case.

Write a function:

int solution(vector<int> &A);

that, given a non-empty zero-indexed array A of N integers, returns the maximum number of flags that can be set on the peaks of the array.

For example, the following array A:

```
A[0] = 1 
A[1] = 5 
A[2] = 3 
A[3] = 4 
A[4] = 3 
A[5] = 4 
A[6] = 1 
A[7] = 2 
A[8] = 3 
A[9] = 4 
A[10] = 6 
A[11] = 2
```

the function should return 3, as explained above.

**Assume that:**

* N is an integer within the range [1..400,000];
* each element of array A is an integer within the range [0..1,000,000,000].

**Complexity:**

* expected worst-case time complexity is O(N);
* expected worst-case space complexity is O(N), beyond input storage (not counting the storage required for input arguments).

Elements of input arrays can be modified.

## Solutions

* C++1
```
int solution(vector<int> &A) {
    vector<int> peaks;
    for(unsigned int i=1; i<A.size()-1; ++i)
    {
        if(A[i-1] < A[i] && A[i] > A[i+1])
            peaks.push_back(i);
    }
    int pSize = peaks.size();
    if(pSize<2) return pSize;
    int maxF = sqrt(peaks.back() - peaks[0])+1;
    int res = 1;
    for(int k=maxF; k>=2 && k>res; --k)
    {
        int lastFlag = peaks[0];
        int used = 1;
        for(int j = 1; j<pSize && used<k; ++j)
        {
            if(peaks[j] - lastFlag >= k)
            {
                lastFlag = peaks[j];
                used++;
            }
        }
        if(used > res) res = used;
    }
    return res;
}
```

## Testcase

single  extreme min test

triple  three elements

extreme_without_peaks  test without peaks

simple1  first simple test

simple2  second simple test

medium_many_peaks  medium test with 100 peaks

WRONG ANSWER  got 25 expected 28

medium_random  chaotic medium sequences, length = ~10,000

WRONG ANSWER  got 95 expected 97

packed_peaks  possible to set floor(sqrt(N))+1 flags

large_random  chaotic large sequences, length = ~100,000

WRONG ANSWER  got 315 expected 316

large_little_peaks  large test with 20-800 peaks

WRONG ANSWER  got 361 expected 437

large_many_peaks  large test with 10,000 - 25,000 peaks

WRONG ANSWER  got 309 expected 313

large_anti_slow  large test anti slow solutions

WRONG ANSWER  got 315 expected 316

large_anti_slow2  large test anti slow solutions

extreme_max  extreme test, maximal number of elements

extreme_max2  extreme test, maximal number of elements

## Explanation

1. Find all peaks
2. Because `the distance between any two flags should be greater than or equal to K, The distance between indices P and Q is the absolute value |P − Q|.`, the maximum distance is `peaks.back() - peaks[0]`. So the maximum flags number is `sqrt(peaks.back() - peaks[0])+1`.
3. Try K from the maximum flags number, put flags in the peaks. Find the maximum number of flags that can be set on the peaks of the array.

