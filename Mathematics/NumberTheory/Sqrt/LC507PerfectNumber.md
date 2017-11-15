# LC507. Perfect Number

### LeetCode

## Question

We define the Perfect Number is a positive integer that is equal to the sum of all its positive divisors except itself.

Now, given an integer n, write a function that returns true when it is a perfect number and false when it is not.

**Example:**

```
Input: 28
Output: True
```

**Explanation:** 28 = 1 + 2 + 4 + 7 + 14

**Note:** The input number n will not exceed 100,000,000. (1e8)

## Solutions

* C++1
```
bool checkPerfectNumber(int num) {
    int sum=1;
    for(int i=2; i<=sqrt(num); ++i)
    {
        if(num % i == 0)
        {
            sum += i;
            if(i != num/i) sum += num/i;
        }
    }
    return num!=1 && sum==num;
}
```

* C++2 (3ms)
```
bool checkPerfectNumber(int num) {
    return num==6 || num==28 || num==496 || num==8128 || num==33550336;
}
```

## Explanation

calculate the sum of all its positive divisors except itself.

* **worst-case time complexity:** O(log(n))
* **worst-case space complexity:** O(1)
