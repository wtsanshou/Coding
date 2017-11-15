# HR. Russian Peasant Exponentiation

### HackerRank

## Question

We all know how to calculate ab using b operations by multiplying 1 by a a total of b times. The drawback to this method is that b can be large, which makes exponentiation very slow.

There is a well known method called Russian Peasant Multiplication that you can read about <a href="http://lafstern.org/matt/col3.pdf">here</a>. Now let's use this to raise some `complex numbers` to powers!

You're given q queries where each query consists of four integers: a, b, k, and m. For each query, calculate (a + b·i)<sup>k</sup> = c + d·i (where i is an imaginary unit) and then print the respective values of c mod m and d mod m as two space-separated integers on a new line.

**Input Format**

The first line contains a single integer, q, denoting the number of queries. 
Each of the q subsequent lines describes a query in the form of four space-separated integers: a, b, k, and m (respectively).

**Constraints**

* 1 <= q <= 10<sup>5</sup>
* 0 <= k <= 10<sup>18</sup>
* 2 <= m <= 10<sup>9</sup>
* 0 <= a,b <= m

**Output Format**

For each query, print the two space-separated integers denoting the respective values of c mod m and d mod m on a new line.

**Sample Input**
```
3
2 0 9 1000
0 1 5 10
8 2 10 1000000000
```

**Sample Output**
```
512 0
0 1
880332800 927506432
```

**Explanation**

In the first query, we have a=2, b=0, k=9, m=1000. We calculate the following:

1.  29 = 512
2.  i<sup>5</sup> = i

## Solutions

* C++1
```
vector<long> Multiply(vector<long>& ab, vector<long>& cd, long m){
    vector<long> res(2);
    res[0] = (ab[0]*cd[0]%m - ab[1]*cd[1]%m + m) % m;
    res[1] = (ab[0]*cd[1]%m + ab[1]*cd[0]%m + m) % m;
    return res;
}

vector<long> Cal(vector<long>& ab, long k, long m){
    if(k==0){
        vector<long>k0(2, 0);
        k0[0] = 1;
        return k0;
    }
    if(k==1) return ab;
    vector<long> res = Cal(ab, k/2, m);
    res = Multiply(res, res, m);
    if(k%2 == 1)
        res = Multiply(res, ab, m);
    return res;
}

int main() {
    int q;
    vector<long> ab(2);
    vector<long> res(2);
    long k, m;
    cin>>q;
    for(int i=0; i<q; ++i){
        cin>>ab[0];
        cin>>ab[1];
        cin>>k;
        cin>>m;
        res = Cal(ab, k, m);
        cout<<to_string(res[0])+" "+to_string(res[1])<<endl;
    }
    return 0;
}
```
* Java1
```
public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        int q = sc.nextInt();
        long [] ab = new long[2];
        long k;
        long m;
        
        for(int i=0; i<q; ++i){
            ab[0] = sc.nextLong();
            ab[1] = sc.nextLong();
            k = sc.nextLong();
            m = sc.nextLong();
            long[] res = Cal(ab, k, m);
            System.out.println(res[0]+" "+res[1]);
        }
    }
    
    private static long[] Cal(long[] ab, long k, long m){
        if(k==0) return new long[]{(long)1, (long)0};
        if(k==1) return ab;
        long [] res = Cal(ab, k/2, m);
        res = Multiply(res, res, m);
        if(k%2 == 1)
            res = Multiply(res, ab, m);
        return res;
    }
    
    private static long[] Multiply(long[] ab, long[] cd, long m){
        long[] res = new long[2];
        res[0] = (ab[0]*cd[0] % m - ab[1]*cd[1] % m + m) % m;
        res[1] = (ab[0]*cd[1] % m + ab[1]*cd[0] % m) % m;
        return res;
    }
```

## Explanation

At the beginning, I extended (8 + 2i)<sup>10</sup> to see if there is any rule. It seems no way to simplify it.

Then, I read the `Russian Peasant Multiplication`. Based on the hint of it, the idea is not difficult to come out. I did use this kind of recursive method to get **x<sup>n</sup>**, but I don't know it has a name `Russian Peasant Multiplication`.

**Formula:**
`(a + b*i) * (c + d*i) = (a*c - b*d) + (a*d + b*c) * i`

**Corner cases:**
* **k==0:** 

(a + b·i)<sup>k</sup> should equal 1, so the result should be `c=1, d=0`.

* **Negative mod Positive:** 

`(a*c - b*d)` might be negative number. In Java or C++ `(a*c - b*d)` **mod** `m` equals a negative number, we have to use `((a*c - b*d)+m) mod m`.

I found from Google that Python has different behaviour of the modulo (%) operation with C++ and Java. Python rounds towards minus infinite and C++ or Java towards 0.

