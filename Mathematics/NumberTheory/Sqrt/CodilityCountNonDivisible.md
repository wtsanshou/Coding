# Codility. Count Non Divisible

### Codility

## Question

You are given a non-empty zero-indexed array A consisting of N integers.
For each number A[i] such that 0 ≤ i < N, we want to count the number of elements of the array that are not the divisors of A[i]. We say that these elements are non-divisors.

**For example, consider integer N = 5 and array A such that:**

```
A[0] = 3 
A[1] = 1 
A[2] = 2 
A[3] = 3 
A[4] = 6
```

**For the following elements:**

* A[0] = 3, the non-divisors are: 2, 6,
* A[1] = 1, the non-divisors are: 3, 2, 3, 6,
* A[2] = 2, the non-divisors are: 3, 3, 6,
* A[3] = 3, the non-divisors are: 2, 6,
* A[4] = 6, there aren't any non-divisors.

**Write a function:**

vector<int> solution(vector<int> &A);

that, given a non-empty zero-indexed array A consisting of N integers, returns a sequence of integers representing the amount of non-divisors.

**The sequence should be returned as:**

* a structure Results (in C), or
* a vector of integers (in C++), or
* a record Results (in Pascal), or
* an array of integers (in any other programming language).

**For example, given:**

```
A[0] = 3 
A[1] = 1 
A[2] = 2 
A[3] = 3 
A[4] = 6
```

the function should return [2, 4, 3, 2, 0], as explained above.

**Assume that:**

* N is an integer within the range [1..50,000];
* each element of array A is an integer within the range [1..2 * N].

**Complexity:**

* expected worst-case time complexity is O(N*log(N));
* expected worst-case space complexity is O(N), beyond input storage (not counting the storage required for input arguments).

Elements of input arrays can be modified.

## Solutions

* C++1
```
vector<int> solution(vector<int> &A) {
    unordered_map<int, int> count;
    for(int a : A)
        count[a]++;
    int n = A.size();
    vector<int>res;
    for(int a : A)
    {
        int div = (a==1) ? count[a] : count[a] + count[1];
        int sq = sqrt(a);
        for(int i=2; i<=sq; ++i)
        {
            if(a%i == 0)
                div += count[i] + ((i*i==a) ? 0 : count[a/i]);
        }
        res.push_back(n - div);
    }
    return res;
}
```

* Java
```
class Solution {
    public int[] solution(int[] A) {
        int n = A.length;
        Map<Integer, Integer> map = new HashMap<>();
        int[] res = new int[n];
        
        for(int a : A){
            if(!map.containsKey(a))
                map.put(a, 0);
            map.put(a, map.get(a)+1);
        }
        
        for(int i=0; i<n; i++){
            int divisors = getDivisors(A[i], map);
            res[i] = n - divisors;
        }
        return res;
    }
    
    private int getDivisors(int a, Map<Integer, Integer> map){
        int count = 0;
        int n = (int)Math.sqrt((double)a);
        for(int i=1; i<=n; i++){
            if(a % i == 0){
                if(map.containsKey(i)) count += map.get(i);
                if(a/i != i && map.containsKey(a/i))
                    count += map.get(a/i);
            }
        }
        return count;
    }
}

```

## Explanation

1. count the amount of numbers and store them into a map
2. check how many divisors of A[i] in the array
3. n - the amount of A[i]'s divisors

**NOTE:** 

1. `1` is divisors of any positive numbers
2. The number is divisors of itself
3. The amount of the same number's non-divisors should be the same. (Might be able to remove some work using another map)

## Testcase

extreme_simple  extreme simple

double  two elements

simple  simple tests

primes  prime numbers

small_random  small, random numbers, length = 100

medium_random  medium, random numbers length = 5,000

large_range  1, 2, ..., N, length = ~20,000

large_random  large, random numbers, length = ~30,000

large_extreme  large, all the same values, length = 50,000
