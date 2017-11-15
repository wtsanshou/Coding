# HR. Even Odd Query

### HackerRank

## Question

You are given an array A of size N. You are also given an integer Q. Can you figure out the answer to each of the Q queries?

Each query contains 2 integers x and y, and you need to find whether the value find(x,y) is Odd or Even:

```
find(int x,int y)
{
    if(x>y) return 1;
    ans = pow(A[x],find(x+1,y))
    return ans
}
```

**Note** : pow(a,b) = ab.

**Input Format**

The first line of the input contains an integer N. The next line contains N space separated non-negative integers(whole numbers less than or equal to 9).

The line after that contains a positive integer, Q , the denotes the number of queries to follow. Q lines follow, each line contains two positive integer x and y separated by a single space.

**Output Format**

For each query, display **'Even'** if the value returned is Even, otherwise display **'Odd'**.

**Constraints**

* 2 ≤ N ≤ 10<sup>5</sup> 
* 2 ≤ Q ≤ 10<sup>5</sup>  
* 1 ≤ x,y ≤ N 
* x ≤ y

Array is 1-indexed.

No 2 consecutive entries in the array will be zero.

**Sample Input**
```
3
3 2 7
2
1 2
2 3
```

**Sample Output**
```
Odd
Even
```

**Explanation**

* find(1,2) = 9, which is Odd 
* find(2,3) = 128, which is even

## Solutions
* Java1
```
public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        int N = sc.nextInt();
        int[] A = new int[N];
        for(int i=0; i<N; ++i)
            A[i] = sc.nextInt();
        int Q = sc.nextInt();
        for(int i=0; i<Q; ++i){
            int x = sc.nextInt();
            int y = sc.nextInt();
            if(x!=y && A[x]==0) System.out.println("Odd");
            else if( (A[x-1]%2) == 1) System.out.println("Odd");
            else System.out.println("Even");
        }
    }
```

## Explanation

At first, I was thinking using dp[i][j] to save find[i][j]. But, since **2 ≤ N ≤ 10<sup>5</sup>**, the size of dp might be too big. So, I realized this must be a wrong direction.

O(1) solution:
* The result is Odd if `A[x-1]` is Odd
* The result is Even if `A[x-1]` is Even
* **Corner case:** The result is Odd if the number next to `A[x-1]` is *0* (N<sup>0</sup> = 1)