# LC625. Minimum Factorization

### LeetCode

## Question

Given a positive integer a, find the smallest positive integer b whose multiplication of each digit equals to a.

If there is no answer or the answer is not fit in 32-bit signed integer, then return 0.

**Example 1**

**Input:**
```
48 
```

**Output:**
```
68
```

**Example 2**

**Input:**
```
15
```

**Output:**
```
35
```

## Solutions

* C++1
```
int smallestFactorization(int a) {
        if(a == 1) return 1;
        vector<int> digits;
        int d = 9;
        while(d > 1)
        {
            if(a % d == 0)
            {
                digits.push_back(d);
                a /= d;
            }
            else
                d--;
        }
        if(a>9 || digits.size()>10) return 0;
        sort(digits.begin(), digits.end());
        long res = 0;
        for(int x : digits)
            res = res*10 + x;
        if(res > INT_MAX) return 0;
        return res;
    }
```

* Java1
```
public int smallestFactorization(int a) {
        if(a==1) return 1;
        List<Integer> digits = new LinkedList();
        int d = 9;
        while(d > 1)
        {
            if(a%d == 0){
                digits.add(d);
                a /= d;
            }
            else
                d--;
        }
        if(a > 9 || digits.size()>10) return 0;
        Integer[] arr = digits.toArray(new Integer[digits.size()]);
        Arrays.sort(arr);
        long res = 0;
        for(int i=0; i<arr.length; ++i)
            res = res*10 + arr[i];
        if(res > Integer.MAX_VALUE) return 0;
        return (int)res;
    }
```

## Explanation

**From the Question, we can get:**

1. 1 <= `a` <= 2147483647
2. 1 <= `b` <= 2147483647
3. `b` whose multiplication of each digit equals to a.
4. Return the smallest positive integer `b`.

**We can conclude:**

1. Integer `a` can be divided to 1 by `([2-9],)*`.
2. Integer `a` should be divided from 9 to 2 to get the shortest divisors. Save the divisors.
3. Sort the divisors to get the smallest positive integer `b`.

**Corner cases:** a equals 1

**No answer cases:**

1. Integer `a` cannot be divided to 1 by `([2-9],)*`.
2. The the smallest positive integer `b` is larger than 2147483647.
* `b` is 10 digits, but is larger than 2147483647
* `b` is more than 10 digits

* **worst-case time complexity:** O(1)
* **worst-case space complexity:** O(1)



