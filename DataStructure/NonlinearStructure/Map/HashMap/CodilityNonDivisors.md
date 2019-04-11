# Codility. Non Divisors

### Codility

## Question

You are given an array A consisting of N integers.

For each number A[i] such that 0 ≤ i < N, we want to count the number of elements of the array that are not the divisors of A[i]. We say that these elements are non-divisors.

For example, consider integer N = 5 and array A such that:

`A[0] = 3 A[1] = 1 A[2] = 2 A[3] = 3 A[4] = 6`

For the following elements:

* A[0] = 3, the non-divisors are: 2, 6,
* A[1] = 1, the non-divisors are: 3, 2, 3, 6,
* A[2] = 2, the non-divisors are: 3, 3, 6,
* A[3] = 3, the non-divisors are: 2, 6,
* A[4] = 6, there aren't any non-divisors.

**Write a function:**

class Solution { public int[] solution(int[] A); }
that, given an array A consisting of N integers, returns a sequence of integers representing the amount of non-divisors.

Result array should be returned as an array of integers.

For example, given:

`A[0] = 3 A[1] = 1 A[2] = 2 A[3] = 3 A[4] = 6`

the function should return [2, 4, 3, 2, 0], as explained above.

Write an efficient algorithm for the following `assumptions`:

* N is an integer within the range [1..50,000];
* each element of array A is an integer within the range [1..2 * N].

## Solutions

### Solution 1

* Java
```
import java.util.*;

class Solution {
    public int[] solution(int[] A) {
        int n = A.length;
        int[] res = new int[n];
        Map<Integer, Integer> map = new HashMap<>();
        for(int a : A){
            if(!map.containsKey(a))
                map.put(a, 0);
            map.put(a, map.get(a)+1);
        }
        
        for(int i=0; i<n; i++){
            res[i] = getNumberOfNonDivisors(A[i], map);
        }
        return res;
    }
    
    private int getNumberOfNonDivisors(int a, Map<Integer, Integer> map){
        int count = 0;
        for(Map.Entry<Integer, Integer> m : map.entrySet())
            if(m.getKey() >a || (m.getKey()!=a && a % m.getKey() != 0))
                count += m.getValue();
        return count;
    }
}
```

Find non-divisors in the map.

**Complexity:**

* **worst-case time complexity:** O(N<sup>2</sup>), where `N` is the size of the input `A`.
* **worst-case space complexity:** `O(N)`, where `N` is the size of the input `A`.

### Solution 2

* Java
```
import java.util.*;

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

Find divisors in the map.

**Complexity:**

* **worst-case time complexity:** `O(N * log(N))`, where `N` is the size of the input `A`.
* **worst-case space complexity:** `O(N)`, where `N` is the size of the input `A`.