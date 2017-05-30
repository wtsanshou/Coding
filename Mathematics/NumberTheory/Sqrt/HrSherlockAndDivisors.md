# Sherlock and Divisors

### HackerRank

## Question

Watson gives an integer N to Sherlock and asks him: What is the number of divisors of N that are divisible by 2?.

**Input Format** 

First line contains T, the number of testcases. This is followed by T lines each containing an integer N.

**Output Format** 

For each testcase, print the required answer in one line.

**Constraints** 

* 1 <= T <= 100
* 1 <= N <=109

**Sample Input**
```
2
9
8
```

**Sample Output**
```
0
3
```

**Explanation** 

* 9 has three divisors 1, 3 and 9 none of which is divisible by 2. 
* 8 has four divisors 1,2,4 and 8, out of which three are divisible by 2.

## Solutions
* Java1
```
public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        int T = sc.nextInt();
        int N;
        for(int i=0; i<T; ++i){
            N = sc.nextInt();
            System.out.println(CountDivisors(N));
        }
    }
    
    private static int CountDivisors(int n){
        int s = (int)Math.sqrt(n);
        int res = 0;
        for(int i=1; i<=s; ++i){
            if(n%i == 0){
                if(i%2==0) res++;
                if(n/i != i && (n/i)%2 == 0) res++; 
            }
        }
        return res;
    }
```
