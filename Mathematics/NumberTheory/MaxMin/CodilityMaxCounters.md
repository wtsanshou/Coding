# Codility Max Counters

### Codility

## Question

You are given N counters, initially set to 0, and you have two possible operations on them:

* increase(X) − counter X is increased by 1,
* max counter − all counters are set to the maximum value of any counter.

A non-empty zero-indexed array A of M integers is given. This array represents consecutive operations:

* if A[K] = X, such that 1 ≤ X ≤ N, then operation K is increase(X),
* if A[K] = N + 1 then operation K is max counter.

For example, given integer N = 5 and array A such that:

`A[0] = 3 A[1] = 4 A[2] = 4 A[3] = 6 A[4] = 1 A[5] = 4 A[6] = 4`

the values of the counters after each consecutive operation will be:
```
(0, 0, 1, 0, 0) (0, 0, 1, 1, 0) (0, 0, 1, 2, 0) (2, 2, 2, 2, 2) (3, 2, 2, 2, 2) (3, 2, 2, 3, 2) (3, 2, 2, 4, 2)
```

The goal is to calculate the value of every counter after all operations.

**Write a function:**

`vector<int> solution(int N, vector<int> &A);`

that, given an integer N and a non-empty zero-indexed array A consisting of M integers, returns a sequence of integers representing the values of the counters.

The sequence should be returned as:

* a structure Results (in C), or
* a vector of integers (in C++), or
* a record Results (in Pascal), or
* an array of integers (in any other programming language).

For example, given:

`A[0] = 3 A[1] = 4 A[2] = 4 A[3] = 6 A[4] = 1 A[5] = 4 A[6] = 4`

the function should return [3, 2, 2, 4, 2], as explained above.

**Assume that:**

* N and M are integers within the range [1..100,000];
* each element of array A is an integer within the range [1..N + 1].

**Complexity:**

* expected worst-case time complexity is O(N+M);
* expected worst-case space complexity is O(N), beyond input storage (not counting the storage required for input arguments).

Elements of input arrays can be modified.

## Solutions

### Solution 1

* Java (Time Limit Exceeded)
```
public int[] solution(int N, int[] A) {
    int[] res = new int[N];
    int max = 0;
    for(int a : A){
        if(a == N+1)
            Arrays.fill(res, max);
        else{
            res[a-1]++;
            max = Math.max(max, res[a-1]);
        }
    }
    return res;
}
```

Like the question said: when found `N+1` fill the `max` to all elements.

* **worst-case time complexity:** O(N<sup>2</sup>)
* **worst-case space complexity:** O(N)

### Solution 2

* C++
```
vector<int> solution(int N, vector<int> &A) {
    vector<int> res(N);
    int preMax=0, curMax=0;
    for(int a : A)
    {
        if(a > N)   preMax = curMax;
        else
        {
            if(res[a-1] < preMax) res[a-1] = preMax+1;
            else  res[a-1]++;
            
            if(curMax<res[a-1]) curMax = res[a-1];
        }
    }
    for(int i=0; i<N; ++i)
        if(res[i]<preMax)
            res[i] = preMax;
    return res;
}
```

Delay the update, using `preMax` to remember the previous maximum value when need to do `max counter`. 

When update an element, check if it is smaller than the `preMax`. If so, update to `preMax + 1`.

Keep recording the current maximum value `curMax` int the result.

In the final step, remember to update all elements to at least `preMax`.

* **worst-case time complexity:** `O(N+M)`, where where `M` is the length of the array `A`. 
* **worst-case space complexity:** `O(N)`

## Testcase

extreme_small 

all max_counter operations

single 

only one counter


small_random1 

small random test, 6 max_counter operations


small_random2 

small random test, 10 max_counter operations


medium_random1 

medium random test, 50 max_counter operations


medium_random2 

medium random test, 500 max_counter operations


large_random1 

large random test, 2120 max_counter operations


large_random2 

large random test, 10000 max_counter operations


extreme_large 

all max_counter operations

