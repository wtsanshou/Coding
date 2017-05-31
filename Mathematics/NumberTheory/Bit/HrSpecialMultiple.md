# Special Multiple

### HackerRank

## Question

You are given an integer N. Can you find the least positive integer X made up of only 9's and 0's, such that, X is a multiple of N?

**Update**

X is made up of one or more occurences of 9 and zero or more occurences of 0.

**Input Format** 

The first line contains an integer T which denotes the number of test cases. T lines follow. 

Each line contains the integer N for which the solution has to be found.

**Output Format** 

Print the answer X to STDOUT corresponding to each test case. The output should not contain any leading zeroes.

**Constraints** 

* 1 <= T <= 10<sup>4</sup> 
* 1 <= N <= 500

**Sample Input**
```
3
5
7
1
```
**Sample Output**
```
90
9009
9
```
**Explanation** 

90 is the smallest number made up of 9's and 0's divisible by 5. Similarly, you can derive for other cases.

## Solutions
* C++1
```
static vector<long> mem;
long countSmallest90Num(int n){
    for(int i=0; i<mem.size(); ++i){
        if(mem[i] % n == 0)
            return mem[i];
    }
    int next = mem.size();
    while(++next){
        string bina;
        int x = next;
        while(x>0){
            bina = to_string(x&1) + bina;
            x >>= 1;
        }
        replace(bina.begin(), bina.end(), '1', '9');
        long res = stol(bina, nullptr, 10);
        mem.push_back(res);
        if(res % n == 0)
            return res;
    }
    return 0;
}
int main() {
    int T, N;
    cin>>T;
    for(int i=0; i<T; ++i){
        cin>>N;
        cout<<countSmallest90Num(N)<<endl;
    }
    return 0;
}
```

* Java1
```
private static List<Long> mem = new LinkedList<Long>(); 
    
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        int T = sc.nextInt();
        for(int i=0; i<T; ++i){
            int N = sc.nextInt();
            System.out.println(FindSmallest90Num(N));
        }
    }
    
    private static long FindSmallest90Num(int N){
        for(int i=0; i<Solution.mem.size(); ++i){
            if(Solution.mem.get(i) % N == 0)
                return Solution.mem.get(i);
        }
        int next = Solution.mem.size();
        while(++next > 0){
            String binaryI = Integer.toBinaryString(next);
            binaryI = binaryI.replace('1', '9');
            long res = Long.parseLong(binaryI);
            Solution.mem.add(res);
            if(res % N == 0) return res;
        }
        return 0;
    }
```

## Explanation

Integer: 1,  2,  3,   4,   5, ..., n

Binary:  1, 10, 11, 100, 101, ..., n10

90Nums:  9, 90, 99, 900, 909, ..., n90
