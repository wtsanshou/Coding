# Leonardo's Prime Factors

### HackerRank

## Question

Leonardo loves primes and created q queries where each query takes the form of an integer, n. For each n, he wants you to count the maximum number of unique prime factors of any number in the inclusive range [1,n] and then print this value on a new line.

**Note:** Recall that a prime number is only divisible by 1 and itself, and 1 is not a prime number.

**Input Format**

The first line contains an integer, q, denoting the number of queries. 
Each line i of the j subsequent lines contains a single integer, n.

**Constraints**

* 1 <= q <= 10<sup>18</sup>
* 1 <= n <= 10<sup>18</sup>

**Output Format**

For each query, print the maximum number of unique prime factors for any number in the inclusive range [1,n] on a new line.

**Sample Input**

6

1

2

3

500

5000

10000000000

**Sample Output**

0

1

1

4

5

10

**Explanation**

1.  The maximum number of unique prime factors of any number in the inclusive range [1,1] is 0, because 1 is not prime and its only factor is itself.
2.  The maximum number of unique prime factors of any number in the inclusive range [1,2] is 1. We already know that the number 1 has 0 prime factors, but 2 has 1 prime factor (itself).
3.  The maximum number of unique prime factors of any number in the inclusive range [1,3] is 1. The number 3 has 1 prime factor (itself), and we already know that the number 2 has 1 prime factor and the number 1 has 0 prime factors.
4.  The maximum number of unique prime factors in the inclusive range [1,500] is 4. The product of our first four unique primes is 2×3×5×7=210, and there are no additional unique primes we can multiply that number by that results in a value <=500.

## Solutions
* Java1
```bash
public static void main(String[] args) {
        String[] primes = new String[] {"1","2","3","5","7","11","13","17","19","23","29","31","37","41","43","47","53"};
        BigInteger[] sumPrimes = new BigInteger[17];
        sumPrimes[0] = new BigInteger(primes[0]);
        for(int i=1; i<17; ++i){
            sumPrimes[i] = new BigInteger(primes[i]);
            sumPrimes[i] = sumPrimes[i].multiply(sumPrimes[i-1]);
        }
        
        Scanner sc = new Scanner(System.in);
        int q = sc.nextInt();
        BigInteger n;
        for(int i=0; i<q; ++i){
            n = sc.nextBigInteger();
            for(int j=0; j<17; ++j){
                int res = n.compareTo(sumPrimes[j]);
                if(res == 0 || res==-1){
                    System.out.println( (res == 0) ? j : j-1);
                    break;
                }                   
            }
        }
    }
```

## Explanation

The `maximum number of unique prime factors` makes me misunderstanding. I thought it is to count the unique number of N's prime factors. That could be difficult because N could be 10<sup>18</sup>.

After seeing the **explanation 4**, I understand it. 

To get the `maximum number of unique prime factors`, we should use as many small primes as possible. 

I saw the result of 10000000000 is just 10. So, I can guess the result of 10<sup>18</sup> shouldn't be too large. As I guessed, when I multiply primes from 2 to 53, the result is larger than 10<sup>18</sup>. It just involves 16 primes.

To reduce duplicated primes multiply operations, I use an array to save the results of each product range. 

So that, I just need to compare N with the these product ranges from the beginning of the array. When we found a product is equal or larger than N, we can return the index of the array as output.

**Note:** For the specific case `N=1`, I put `1` at the begining of the array.

**return**
* j, if equal
* j-1, if product > N

