# K Candy Store

### HackerRank

## Question

Jim enters a candy shop which has N different types of candies, each candy is of the same price. Jim has enough money to buy K candies. In how many different ways can he purchase K candies if there are infinite candies of each kind?

**Input Format** 

The first line contains an integer T, the number of tests. 

This is followed by 2T lines which contain T tests: 

The first line (of each testcase) is an integer N and the second line (of each testcase) is an integer K.

**Output Format** 

For each testcase, print the number of ways Jim can buy candies from the shop in a newline. If the answer has more than 9 digits, print the last 9 digits.

**Note:** This problem may expect you to have solved nCr Table

**Constraints** 

* 1 <= T <= 200 
* 1 <= N < 1000 
* 1 <= K < 1000

**Sample Input**
```
2
4
1
2
3
```

**Sample Output**
```
4
4
```

**Explanation** 

There are 2 testcases, for the first testcase we have N = 4 and K = 1, as Jim can buy only 1 candy, he can choose to buy any of the 4 types of candies available. Hence, his answer is 4. For the 2nd testcase, we have N = 2 and K = 3, If we name two chocolates as a and b, he can buy `aaa bbb aab abb` chocolates, hence 4.

## Solutions

* Java1
```
public static void main(String[] args) {
        int[][] C = new int[2001][1001];
        Initialize(C);
        Scanner sc = new Scanner(System.in);
        int T = sc.nextInt();
        for(int i=0; i<T; ++i){
            int N = sc.nextInt();
            int K = sc.nextInt();
            System.out.println(C[N+K-1][N-1]);
        }
    }
    
    private static void Initialize(int[][] C){
        for(int i=1; i<=2000; ++i){
            for(int j=0; j<=1000; ++j){
                if(j==0 || i==j) C[i][j]=1;
                else if(i>j)
                    C[i][j] = (C[i-1][j-1] + C[i-1][j]) % 1000000000;
            }
        }
    }
```

## Explanation

**Combinations with Repetition**

Given a set of n elements, the combinations with repetition are different groups formed by the k elements of a subset such that:

The order of the elements does not matter.

The elements are repeated.

C<sup>'</sup>(n, r) = C(n+r−1, n−1) = (n+r−1)! / (n−1)r!
