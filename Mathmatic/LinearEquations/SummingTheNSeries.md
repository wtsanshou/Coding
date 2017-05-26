# Summing the N series

### HackerRank

## Question

![Question](Images/SummingtheNseriesQ.png)

## Solutions

* C++1
```bash
int SN(long double N){
    long double x = fmod(N, 1e9 + 7);
    return (int) fmod(x*x,  1e9 + 7);
}

int main() {
    int T;
    long double N;
    cin>>T;
    for(int i=0; i<T; ++i){
        cin>>N;
        cout<< SN(N)<< endl;
    }
    return 0;
}
```

* Java1
```bash
public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        int T = sc.nextInt();
        BigInteger N;
        for(int i=0; i<T; ++i){
            N = sc.nextBigInteger();
            System.out.println(SN(N));
        }  
    }
    
    private static BigInteger MOD = new BigInteger("1000000007");
    
    private static BigInteger SN(BigInteger N){
        N = N.mod(MOD);
        return (N.multiply(N)).mod(MOD);
    }
```

## Explanation

![Explanation](Images/SummingtheNseriesE.PNG)