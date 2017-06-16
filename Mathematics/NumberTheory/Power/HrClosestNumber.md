# Closest Number

### HackerRank

## Question
You are given 3 numbers a, b and x. You need to output the multiple of x which is closest to a<sup>b</sup>. If more than one answer exists , display the smallest one.

**Input Format**

The first line contains T, the number of testcases.
T lines follow, each line contains 3 space separated integers (a, b and x respectively)

**Constraints**

* 1 ≤ T ≤ 10<sup>5</sup>
* 1 ≤ x ≤ 10<sup>9</sup>
* 0 < a<sup>b</sup> ≤ 10<sup>9</sup>
* 1 ≤ a ≤ 10<sup>9</sup>
* -10<sup>9</sup> ≤ b ≤ 10<sup>9</sup>

**Output Format**

For each test case , output the multiple of x which is closest to a<sup>b</sup>

**Sample Input**
```
3
349 1 4
395 1 7
4 -2 2
```

**Sample Output**
```
348
392
0
```

**Explanation**

* The closest multiple of 4 to 349 is 348.
* The closest multiple of 7 to 395 is 392.
* The closest multiple of 2 to 1/16 is 0. 

## Solutions

* Java1
```
public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        int T = sc.nextInt();
        for(int i=0; i<T; ++i){
            int a = sc.nextInt();
            int b = sc.nextInt();
            int x = sc.nextInt();
            
            int val = (int)Math.pow(a, b);
            int mod = val % x;
            if(mod <= x/2){
                System.out.println((val/x) * x);
            }
            else{
                System.out.println((val/x + 1) * x);
            } 
        }
    }
    
    private static int my_pow(int a, int b){
        if(b==0) return 1;
        if(b==1) return a;
        if(b < 0) return 1/ my_pow(a, -b);
        int val = my_pow(a, b/2);
        if(b % 2 == 0) return val*val;
        return val*val*a;
    }
```