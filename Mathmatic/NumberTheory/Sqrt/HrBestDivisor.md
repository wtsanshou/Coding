# Best Divisor

### HackerRank

## Question

Kristen loves playing with and comparing numbers. She thinks that if she takes two different positive numbers, the one whose digits sum to a larger number is better than the other. If the sum of digits is equal for both numbers, then she thinks the smaller number is better. For example, Kristen thinks that 13 is better than 31 and that 12 is better than 11.

Given an integer, n, can you find the divisor of n that Kristin will consider to be the best?

**Input Format**

A single integer denoting n.

**Constraints**

* 0 <= n <= 10<super>5</super>

**Output Format**

Print an integer denoting the best divisor of n.

**Sample Input**
```
12
```

**Sample Output**
```
6
```

**Explanation**

The set of divisors of 12 can be expressed as {1,2,3,4,6,12}. The divisor whose digits sum to the largest number is 6 (which, having only one digit, sums to itself). Thus, we print 6 as our answer.

## Solutions
* Java1
```bash
public static void main(String[] args) {
        Scanner in = new Scanner(System.in);
        int n = in.nextInt();
        int res = 1;
        int s = (int)Math.sqrt(n);
        for(int i=1; i<=s; ++i){
            if(n%i == 0) {
                res = compare(res, i);
                if(n/i != i)
                   res = compare(res, n/i);
            }
        }
        System.out.println(res);
    }
    
    private static int compare(int a, int b){
        int sumA = SumDigit(a);
        int sumB = SumDigit(b);
        if(sumA==sumB) return Math.min(a, b);
        return sumA>sumB ? a : b;
    }
    
    private static int SumDigit(int x) {
        int res = 0;
        while(x>0){
            res += x%10;
            x /= 10;
        }
        return res;
    }

```

## Explanation

This question is to find the `best` number from the divisors of a number **n**.

**Note:** `1` and `n` itself are included.

The most straightforward way is to check from 1 to n. This will take O(n) time.

A O(log(n)) solution is just checking from `1` to `sqrt(n)`. For each divisor `i` in the range, we check `n/i` as well. After `sqrt(n)`, all divisors of `n` will be checked. Because `n/i` will be less than `sqrt(n)`, when `i` is larger than `sqrt(n)`.
