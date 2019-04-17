# Codility. Abs Distinct

### Codility

## Question

A non-empty zero-indexed array A consisting of N numbers is given. The array is sorted in non-decreasing order. The absolute distinct count of this array is the number of distinct absolute values among the elements of the array.

For example, consider array A such that:

`A[0] = -5 A[1] = -3 A[2] = -1 A[3] = 0 A[4] = 3 A[5] = 6`

The absolute distinct count of this array is 5, because there are 5 distinct absolute values among the elements of this array, namely 0, 1, 3, 5 and 6.

**Write a function:**

`int solution(vector<int> &A);`

that, given a non-empty zero-indexed array A consisting of N numbers, returns absolute distinct count of array A.

For example, given array A such that:

`A[0] = -5 A[1] = -3 A[2] = -1 A[3] = 0 A[4] = 3 A[5] = 6`

the function should return 5, as explained above.

**Assume that:**

* N is an integer within the range [1..100,000];
* each element of array A is an integer within the range [−2,147,483,648..2,147,483,647];
* array A is sorted in non-decreasing order.

Complexity:

•	expected worst-case time complexity is O(N);
•	expected worst-case space complexity is O(N), beyond input storage (not counting the storage required for input arguments).

Elements of input arrays can be modified.

## Solutions

* C++
```
#include<climits> //for INT_MIN
int solution(vector<int> &A) {
    int INT_MIN = -2147483648;
    unordered_set<int> set;
    int extreMin = 0;
    for(int a : A)
    {
        if(a == INT_MIN) extreMin = 1;
        else set.insert(abs(a));
    }
    return set.size() + extreMin;
}
```

Set is the best datastructure to count the number of distinct elements.

**Note:** abs(-2147483648) is exceeded INT_MAX. We have to count -2147483648 separately.

**Complexity:**

* **worst-case time complexity:** `O(N)`, where `N` is length of `A`.
* **worst-case space complexity:** `O(N)`, where `N` is length of `A`.

## Testcase

one_element


two_elements


same_elements


simple


simple_no_zero


simple_no_same


simple_no_negative


simple_no_positive


arith_overlow


medium_chaotic1


medium_chaotic2


long_sequence_no_negative


long_sequence_no_positive


long_sequence

