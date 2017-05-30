# Restaurant

### HackerRank

## Question

Martha is interviewing at Subway. One of the rounds of the interview requires her to cut a bread of size `l×b` into smaller identical pieces such that each piece is a square having maximum possible side length with no left over piece of bread.

**Input Format**

The first line contains an integer T. T lines follow. Each line contains two space separated integers l and b which denote length and breadth of the bread.

**Constraints**
* 1 <= T <= 1000
* 1 <= l,b <= 1000
 
**Output Format**

T lines, each containing an integer that denotes the number of squares of maximum size, when the bread is cut as per the given condition.

**Sample Input**
```
2
2 2
6 9
```

**Sample Output**
```
1
6
```

**Explanation**

The 1<sup>st</sup> testcase has a bread whose original dimensions are `2×2`, the bread is uncut and is a square. Hence the answer is 1. 
The 2<sup>nd</sup> testcase has a bread of size `6×9`. We can cut it into 54 squares of size `1×1`, 6 of size `3×3`. For other sizes we will have leftovers. Hence, the number of squares of maximum size that can be cut is 6.

## Solution
* Java1
```bash
public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        int T = sc.nextInt();
        int l, b, gcd;
        for(int i=0; i<T; ++i){
            l = sc.nextInt(); 
            b = sc.nextInt();
            gcd = GCD(l, b);
            System.out.println((l*b)/(gcd*gcd));
        }  
    }

    private static int GCD(int a, int b){
        return b==0 ? a : GCD(b, a%b);
    }
```
