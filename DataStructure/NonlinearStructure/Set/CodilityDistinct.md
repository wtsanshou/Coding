# Codility. Distinct

### Codility

## Question

Write a function

`int solution(vector<int> &A);`

that, given a zero-indexed array A consisting of N integers, returns the number of distinct values in array A.

**Assume that:**

* N is an integer within the range [0..100,000];
* each element of array A is an integer within the range [−1,000,000..1,000,000].

For example, given array A consisting of six elements such that:

`A[0] = 2 A[1] = 1 A[2] = 1 A[3] = 2 A[4] = 3 A[5] = 1`

the function should return 3, because there are 3 distinct values appearing in array A, namely 1, 2 and 3.

**Complexity:**

* expected worst-case time complexity is O(N*log(N));
* expected worst-case space complexity is O(N), beyond input storage (not counting the storage required for input arguments).

Elements of input arrays can be modified.

## Solutions

### Solution 1

* C++
```
int solution(vector<int> &A) {
//unordered_set is better
    set<int> set;
    for(int a : A)
        set.insert(a);
    return set.size();
}
```

Set is the best datastructure to count the number of distinct elements.

## Testcase

extreme_empty 

empty sequence


extreme_single 

sequence of one element


extreme_two_elems 

sequence of three distinct elements


extreme_one_value 

sequence of 10 equal elements


extreme_negative 

sequence of negative elements, length=5


extreme_big_values 

sequence with big values, length=5


medium1 

chaotic sequence of value sfrom [0..1K], length=100


medium2 

chaotic sequence of value sfrom [0..1K], length=200


medium3 

chaotic sequence of values from [0..10], length=200


large1 

chaotic sequence of values from [0..100K], length=10K


large_random1 

chaotic sequence of values from [-1M..1M], length=100K


large_random2 

another chaotic sequence of values from [-1M..1M], length=100K

