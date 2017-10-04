# Sherlock and Permutations

### HackerRank

## Question
Watson asks Sherlock: 

Given a string S of N 0's and M 1's, how many unique permutations of this string start with 1?

Help Sherlock by printing the answer modulo (10<sup>9</sup>+7).

**Input Format** 

First line contains T, the number of test cases. 

Each test case consists of N and M separated by a space.

**Output Format** 

For each test case, print the answer modulo (10<sup>9</sup>+7).

**Constraints** 

* 1 ≤ T ≤ 200 
* 1 ≤ N,M ≤ 1000

**Sample Input**
```
2
1 1
2 3
```

**Sample Output**
```
1
6
```

**Explanation** 

* Test1: Out of all unique permutations ie. 01 and 10, only second permutation satisfies. Hence, output is 1. 
* Test2: Out of all unique permutations ie. 00111 01011 01101 01110 10011 10101 10110 11001 11010 11100, only 10011 10101 10110 11001 11010 11100 satisfy. Hence, output is 6.

## Solutions
* C++1
```
int CountPermutations(int N, int x){
    int C[N+1][x+1] = {0};
    for(int i=1; i<=N; ++i){
        for(int j=0; j<=x; ++j){
            if(j==0 || j==i) C[i][j] = 1;
            else if(i>j) C[i][j] = (C[i-1][j-1] + C[i-1][j]) % 1000000007;
        }
    }
    return C[N][x];
}

int main() {
    int T, N, M;
    cin>>T;
    for(int i=0; i<T; ++i){
        cin>>N>>M;
        cout<< CountPermutations(N+M-1, min(N, M-1))<< endl;
    }
    return 0;
}
```

* Java1
```
public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        int T = sc.nextInt();
        int N, M;
        for(int i=0; i<T; ++i){
            N = sc.nextInt();
            M = sc.nextInt();;
            System.out.println(combination(N+M-1, Math.min(N, M-1)));
        }
    }
    
    private static final int MOD = 1000000007;
    private static int combination(int N, int x){
        int[][] dp = new int[N+1][x+1];
        for(int i=1; i<=N; ++i){
            for(int j=0; j<=x; ++j){
                if(j==0 || i==j) dp[i][j] = 1;
                else if(i>j) dp[i][j] = (dp[i-1][j-1] + dp[i-1][j]) % MOD;
            }
        }
        return dp[N][x];
    }
```

## Explanation
This is a permutation and combination question.

Since the string start with 1, we could treate this question as select `N` 0's or **(M-1)** 1's, and put them in **(N+M-1)** positions. It's `C(N+M-1, min(N, M-1))` which equals `(N+M-1)! / (min(N, M-1))! * ((N+M-1)-min(N, M-1))!

The Constraints have `1 ≤ N,M ≤ 1000`. The result might be huge. To effectively solve the above fomular, we have to use dynamic programming.

We can use the equation:
```
    C(n, i)     =          C(n-1, i-1)             +            C(n-1, i)
n! / (i!*(n-i)!)  =    (n-1)! / (i-1)!*(n-i)!      +        (n-1)! / i!*(n-i-1)!
n! / (i!*(n-i)!)  =  i*(n-1)! / (i*(i-1)!*(n-i)!)  +  (n-1)!*(n-i) / (i!*(n-i-1)!*(n-i))
n! / (i!*(n-i)!)  =  (i*(n-1)!  +  (n-1)!*(n-i)) / (i!*(n-i-1)!*(n-i))
n! / (i!*(n-i)!)  =       ((i + (n-i)) * (n-1)!) / (i! * (n-i)!)
n! / (i!*(n-i)!)  =                           n! / (i!*(n-i)!)
```