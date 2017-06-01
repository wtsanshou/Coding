# <sup>n</sup>C<sub>r</sub> table

### HackerRank

## Question

Jim is doing his discrete maths homework which requires him to repeatedly calculate <sup>n</sup>C<sub>r</sub>(n choose r) for different values of n. Knowing that this is time consuming, he goes to his sister June for help. June, being a computer science student knows how to convert this into a computer program and generate the answers quickly. She tells him, by storing the lower values of <sup>n</sup>C<sub>r</sub>(n choose r), one can calculate the higher values using a very simple formula.

If you are June, how will you calculate <sup>n</sup>C<sub>r</sub> values for different values of n?
Since <sup>n</sup>C<sub>r</sub> values will be large you have to calculate them modulo 10<sup>9</sup>.

**Input Format** 

The first line contains the number of test cases T. 

T lines follow each containing an integer n.

**Output Format** 

For each n output the list of nC0 to nCn each separated by a single space in a new line. If the number is large, print only the last 9 digits. i.e. modulo 10<sup>9</sup>

**Constraints** 

* 1<=T<=200 
* 1<=n< 1000

Sample Input

3
2
4
5

Sample Output

1 2 1
1 4 6 4 1
1 5 10 10 5 1

Explanation 

For 2 we can check <sup>2</sup>C<sub>0</sub> <sup>2</sup>C<sub>1</sub> and <sup>2</sup>C<sub>2</sub> are 1, 2 and 1 respectively. The other inputs' answer follow similar pattern.

## Solutions

* Java1
```
public static void main(String[] args) {
        int[][] dp = new int[1001][1001];
        Initialize(dp);
        Scanner sc = new Scanner(System.in);
        int T = sc.nextInt();
        for(int i=0; i<T; ++i){
            int n = sc.nextInt();
            for(int j=0; j<=n; ++j){
                System.out.print(dp[n][j] + " ");
            }
            System.out.println();
        }
    }
    
    private static void Initialize(int[][] dp){
        for(int i=1; i<=1000; ++i){
            for(int j=0; j<=1000; ++j){
                if(j==0 || i==j) dp[i][j]=1;
                else if(i>j)
                    dp[i][j] = (dp[i-1][j-1] + dp[i-1][j]) % 1000000000;
            }
        }
    }
```

## Explanation

```
    C(n, i)     =          C(n-1, i-1)             +            C(n-1, i)
n! / (i!*(n-i)!)  =    (n-1)! / (i-1)!*(n-i)!      +        (n-1)! / i!*(n-i-1)!
n! / (i!*(n-i)!)  =  i*(n-1)! / (i*(i-1)!*(n-i)!)  +  (n-1)!*(n-i) / (i!*(n-i-1)!*(n-i))
n! / (i!*(n-i)!)  =  (i*(n-1)!  +  (n-1)!*(n-i)) / (i!*(n-i-1)!*(n-i))
n! / (i!*(n-i)!)  =       ((i + (n-i)) * (n-1)!) / (i! * (n-i)!)
n! / (i!*(n-i)!)  =                           n! / (i!*(n-i)!)
```
