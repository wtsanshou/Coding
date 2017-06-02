# Possible Path

### HackerRank

## Question

Adam is standing at point (a,b) in an infinite 2D grid. He wants to know if he can reach point (x,y or not. The only operation he can do is to move to point (a+b,b), (a-b, b), (a, b+a), or (a, b-a) from some point (a, b). It is given that he can move to any point on this 2D grid, i.e., the points having positive or negative X(or Y) co-ordinates.

Tell Adam whether he can reach (x, y) or not.

**Input Format**

The first line contains an integer, T, followed by T lines, each containing 4 space-separated integers i.e. a, b, x and y.

**Constraints**

* 1 <= T <= 1000
* 1 <= a, b, x, y <= 10<sup>18</sup>

**Output Format**

For each test case, display **YES** or **NO** that indicates if Adam can reach (x, y) or not.

**Sample Input**
```
3
1 1 2 3
2 1 2 3
3 3 1 1
```

**Sample Output**
```
YES
YES
NO
```

**Explanation**

* (1,1) -> (2,1) -> (2,3).

## Solutions

* Java1
```
public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        int T = sc.nextInt();
        long a, b, x, y;
        for(int i=0; i<T; ++i){
            a = sc.nextLong();
            b = sc.nextLong();
            x = sc.nextLong();
            y = sc.nextLong();
            System.out.println(CanReach(a, b, x, y));
        }
    }
    
    private static String CanReach(long a, long b, long x, long y){
        if(GCD(a,b) == GCD(x,y)) 
            return "YES";
        return "NO";
    }
    
    private static long GCD(long a, long b){
        return b==0 ? a : GCD(b, a%b);
    }
```

## Explanation

 GCD(a, b) = GCD(a + m * b, b) = GCD(a, b + n * a) = GCD(x, y)