# LC204. Count Primes

### LeetCode

## Question

Description:

Count the number of prime numbers less than a non-negative number, n.

## Solutions

* C++1 (32ms)
```
class Solution {
public:
    void Clean(vector<int>& count, int prime)
    {
        for(int i=prime*prime; i<count.size(); i+=prime)
            count[i]=1;
    }
    int NextPrime(vector<int>& count, int prime)
    {
        for(int i=prime+1; i<count.size(); ++i)
            if(count[i]==0) return i;
        return INT_MAX;
    }
    int countPrimes(int n) {
        if(n<=2) return 0;
        vector<int> count(n, 0);
        count[0] = count[1] = 1;
        int prime = 2;
        int maxPrime = sqrt(n);
        while(prime <= maxPrime)
        {
            Clean(count, prime);
            prime = NextPrime(count, prime);
        }
        int primeNum = 0;
        for(int i=2; i<n; ++i)
        {
            if(count[i]==0)
                primeNum++;
        }
        return primeNum;
    }
};
```

* C++2 (16ms)
```
int countPrimes(int n) {
        if(--n < 2) return 0;
        int m = (n + 1)/2, count = m, k, u = (sqrt(n) - 1)/2;
        int notPrime[m] = {0}; //set as 0 save a lot of memory
        for(int i = 1; i <= u;i++)
            if(!notPrime[i])
              for(k = (i+ 1)*2*i; k < m;k += i*2 + 1)
                  if (!notPrime[k])
                  {
                      notPrime[k] = 1;
                      count--;
                  }
        return count;
}
```

* C++3 (12ms)
```
int countPrimes(int n) {
        if(n < 3) return 0;
        int m = n/2, count = m, k, u = (sqrt(n-1)-1)/2;
        bool notPrime[m] = {0}; //set as 0 save a lot of memory
    
        for(int i = 1; i <= u;i++)
            if(!notPrime[i])
              for(k = (i+1)*2*i; k < m;k += i*2 + 1)
                  if (!notPrime[k])
                  {
                      notPrime[k] = true;
                      count--;
                  }
        return count;
}
```

* Java1 (30ms)
```
public class Solution {
    public int countPrimes(int n) {
        if(n<2) return 0;
        int[] primes = new int[n];
        primes[0]=primes[1] = 1;
        int prime = 2;
        int m = (int)Math.sqrt(n);
        while(prime <= m)
        {
            cutOff(primes, prime);
            prime = nextPrime(primes, prime);
            if(prime >= n)
                break;
        }
        int res=0;
        for(int b : primes)
        {
            if(b==0) res++;
        }
        return res;
    }
    
    private void cutOff(int[] primes, int prime)
    {
        for(int i=prime*prime; i<primes.length; i+=prime)
            primes[i] = 1;
    }
    
    private int nextPrime(int[] primes, int prime)
    {
        prime++;
        while(prime<primes.length && primes[prime]==1)
            prime++;
        return prime;
    }
}
```

* Java2 (16ms)
```
public int countPrimes(int n) {
        if(--n < 2) return 0;
        int m = (n + 1)/2, count = m, k, u = (int)(Math.sqrt(n) - 1)/2;
        int[] notPrime = new int[m];
    
        for(int i = 1; i <= u;i++)
            if(notPrime[i]==0)
              for(k = (i+ 1)*2*i; k < m;k += i*2 + 1)
                  if (notPrime[k]==0)
                  {
                      notPrime[k] = 1;
                      count--;
                  }
        return count;
    }
```

## Explanation

1. Let's start with a isPrime function. To determine if a number is prime, we need to check if it is not divisible by any number less than n. The runtime complexity of isPrime function would be O(n) and hence counting the total prime numbers up to n would be O(n<sup>2</sup>). Could we do better?
2. As we know the number must not be divisible by any number > n / 2, we can immediately cut the total iterations half by dividing only up to n / 2. Could we still do better?
3. Let's write down all of 12's factors:
4. 2 × 6 = 12
5. 3 × 4 = 12
6. 4 × 3 = 12
7. 6 × 2 = 12
As you can see, calculations of 4 × 3 and 6 × 2 are not necessary. Therefore, we only need to consider factors up to √n because, if n is divisible by some number p, then n = p × q and since p ≤ q, we could derive that p ≤ √n.

Our total runtime has now improved to O(n<sup>1.5</sup>), which is slightly better. Is there a faster approach?

```
public int countPrimes(int n) {
   int count = 0;
   for (int i = 1; i < n; i++) {
      if (isPrime(i)) count++;
   }
   return count;
}

private boolean isPrime(int num) {
   if (num <= 1) return false;
   // Loop's ending condition is i * i <= num instead of i <= sqrt(num)
   // to avoid repeatedly calling an expensive function sqrt().
   for (int i = 2; i * i <= num; i++) {
      if (num % i == 0) return false;
   }
   return true;
}
```

8. The Sieve of Eratosthenes is one of the most efficient ways to find all prime numbers up to n. But don't let that name scare you, I promise that the concept is surprisingly simple.

![LC204. Count Primes](Images/LC204CountPrimes.gif)

Sieve of Eratosthenes: algorithm steps for primes below 121. "Sieve of Eratosthenes Animation" by SKopp is licensed under CC BY 2.0.

We start off with a table of n numbers. Let's look at the first number, 2. We know all multiples of 2 must not be primes, so we mark them off as non-primes. Then we look at the next number, 3. Similarly, all multiples of 3 such as 3 × 2 = 6, 3 × 3 = 9, ... must not be primes, so we mark them off as well. Now we look at the next number, 4, which was already marked off. What does this tell you? Should you mark off all multiples of 4 as well?

9. 4 is not a prime because it is divisible by 2, which means all multiples of 4 must also be divisible by 2 and were already marked off. So we can skip 4 immediately and go to the next number, 5. Now, all multiples of 5 such as 5 × 2 = 10, 5 × 3 = 15, 5 × 4 = 20, 5 × 5 = 25, ... can be marked off. There is a slight optimization here, we do not need to start from 5 × 2 = 10. Where should we start marking off?
10. In fact, we can mark off multiples of 5 starting at 5 × 5 = 25, because 5 × 2 = 10 was already marked off by multiple of 2, similarly 5 × 3 = 15 was already marked off by multiple of 3. Therefore, if the current number is p, we can always mark off multiples of p starting at p2, then in increments of p: p2 + p, p2 + 2p, ... Now what should be the terminating loop condition?
11. It is easy to say that the terminating loop condition is p < n, which is certainly correct but not efficient. Do you still remember Hint #3?
12. Yes, the terminating loop condition can be p < √n, as all non-primes ≥ √n must have already been marked off. When the loop terminates, all the numbers in the table that are non-marked are prime.

The Sieve of Eratosthenes uses an extra O(n) memory and its runtime complexity is O(n log(log(n)). For the more mathematically inclined readers, you can read more about its algorithm complexity on Wikipedia.

```
public int countPrimes(int n) {
   boolean[] isPrime = new boolean[n];
   for (int i = 2; i < n; i++) {
      isPrime[i] = true;
   }
   // Loop's ending condition is i * i < n instead of i < sqrt(n)
   // to avoid repeatedly calling an expensive function sqrt().
   for (int i = 2; i * i < n; i++) {
      if (!isPrime[i]) continue;
      for (int j = i * i; j < n; j += i) {
         isPrime[j] = false;
      }
   }
   int count = 0;
   for (int i = 2; i < n; i++) {
      if (isPrime[i]) count++;
   }
   return count;
}
```