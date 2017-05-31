# Is Fibo

### HackerRank

## Question

You are given an integer, N. Write a program to determine if N is an element of the Fibonacci sequence.

The first few elements of the Fibonacci sequence are 0,1,1,2,3,5,8,13,…. A Fibonacci sequence is one where every element is a sum of the previous two elements in the sequence. The first two elements are 0 and 1.

**Formally:** 

* Fib<sub>0</sub> = 0
* Fib<sub>1</sub> = 1
* ….
* Fib<sub>n</sub> = Fib<sub>n-1</sub> + Fib<sub>n-2</sub>  (n>1)

**Input Format** 

The first line contains N, number of test cases. 

N lines follow. Each line contains an integer N.

**Output Format** 

Display IsFibo if N is a Fibonacci number and IsNotFibo if it is not. The output for each test case should be displayed in a new line.

**Constraints** 

* 1 <= T <= 10<sup>5</sup>
* 1 <= N <= 10<sup>10</sup>

**Sample Input**
```
3
5
7
8
```

**Sample Output**
```
IsFibo
IsNotFibo
IsFibo
```

**Explanation** 

* 5 is a Fibonacci number given by Fib<sub>5</sub> = 3+2 
* 7 is not a Fibonacci number 
* 8 is a Fibonacci number given by Fib<sub>8</sub> = 3+5 

## Solutions
* C++1
```
static set<long> mem({0, 1, 2});
string isFibo(long N){
    if(mem.count(N)>0) return "IsFibo";
    else return "IsNotFibo";
}
int main() {
    int T;
    long N;
    cin>>T;
    for(int i=mem.size(); i<60; ++i){
        long temp = *(mem.rbegin()) + *(++mem.rbegin());
        mem.insert(temp);
    }
    for(int i=0; i<T; ++i){
        cin>>N;
        cout<<isFibo(N)<<endl;
    }
    return 0;
}
```
* Java1
```
static LinkedList<Long> mem = new LinkedList<Long>(Arrays.asList((long)1, (long)2));
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        int T = sc.nextInt();
        for(int i=0; i<T; ++i){
            long N = sc.nextLong();
            System.out.println(isFibonacci(N));
        }
    }
    
    private static String isFibonacci(long N){
        if(Solution.mem.contains(N)) return "IsFibo";
        for(int i=Solution.mem.size(); Solution.mem.getLast()<N; ++i){
            long temp = Solution.mem.getLast() + Solution.mem.get(i-2);
            Solution.mem.add(temp);
            if(temp==N) return "IsFibo";
        }
        return "IsNotFibo";
    }
```

## Explanation

This is not a difficult question, but I was a little careless!

I almost noticed every corner cases:

* **1 <= N <= 10<sup>10</sup>**, N is larger than integer range.
* If you re-calculate fibonacci for each N, it may exceed time limitation. So, I save the fibonacci numbers in static data structure.

But, I still got wrong answer!!!

Then, I used some test cases:

**Sample Input**
```
4
317811
196418
10000000000
317811
```

**Sample Output**
```
IsFibo
IsFibo
IsNotFibo
IsNotFibo
```

`317811` should be IsFibo. The first answer is correct. But the final anser is wrong. So, the problem is form `1e10`. I used `long` to handle N and create fibonacci numbers. `long` is 64 bit should be able to handle them. Even `N=1e10`, the maxmum fibonacci should be less than `2e10`.

Finally, I found my mistake: I declared `T` and `N` together using `int`. When the input is out of range of `int`, there is an overflow. However, I can understan `1e10` is overflow, but why it affects the next input? Hence, I output all values of N:
```
317811
196418
2147483647
2147483647
```

It seems after the first overflow, all `N` after that are `2147483647` no matter what input is.