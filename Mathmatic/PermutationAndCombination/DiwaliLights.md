# Diwali Lights

#### HackerRank

## Question
On the eve of Diwali, Hari is decorating his house with a serial light bulb set. The serial light bulb set has N bulbs placed sequentially on a string which is programmed to change patterns every second. If at least one bulb in the set is on at any given instant of time, how many different patterns of light can the serial light bulb set produce?
Note: Lighting two bulbs *-* is different from **-
Input Format 
The first line contains the number of test cases T, T lines follow. 
Each line contains an integer N, the number of bulbs in the serial light bulb set.
Output Format 
Print the total number of patterns modulo 105
Constraints 
1 <= T <= 1000 
0< N < 104
Sample Input
2
1
2
Sample Output
1
3
Explanation
Case 1: 1 bulb can be lit in only 1 way. 
Case 2: 2 bulbs can be lit in -*, *-, ** i.e. 3 ways.

## Solutions
* C++1
```bash
int CountFormats(int N) {
    int res = 1;
    for(int i=0; i<N; ++i)
        res = (res << 1) % 100000;
    return res-1;
}
int main() {
    /* Enter your code here. Read input from STDIN. Print output to STDOUT */   
    int T, N;
    cin>>T;
    for(int i=0; i<T; ++i){
        cin>>N;
        cout<< CountFormats(N)<< endl;
    }
    return 0;
}
```

* C++2
```bash
int CountFormats(int N) {
    if(N==0) return 1;
    long res = CountFormats(N/2);
    res = (res*res) % 100000;
    return N%2==0 ? res : (res*2)% 100000;
}

int main() {
    /* Enter your code here. Read input from STDIN. Print output to STDOUT */   
    int T, N;
    cin>>T;
    for(int i=0; i<T; ++i){
        cin>> N;
        cout<< CountFormats(N) - 1<< endl;
    }
    return 0;
}
```

* Java1
```bash
public static void main(String[] args) {
        /* Enter your code here. Read input from STDIN. Print output to STDOUT. Your class should be named Solution. */
        Scanner sc = new Scanner(System.in);
        int T, N;
        T = sc.nextInt();
        for(int i=0; i<T && sc.hasNextInt(); ++i){
            N = sc.nextInt();
            System.out.println(CountFormats(N));
        }   
    }
    
    private static int CountFormats(int N){
        int res = 1;
        for(int i=0; i<N; ++i)
            res = (res<< 1) % 100000;
        return res-1;
    }
```

* Java2
```bash
public static void main(String[] args) {
        /* Enter your code here. Read input from STDIN. Print output to STDOUT. Your class should be named Solution. */
        Scanner sc = new Scanner(System.in);
        int T, N;
        T = sc.nextInt();
        for(int i=0; i<T && sc.hasNextInt(); ++i){
            N = sc.nextInt();
            System.out.println(CountFormats(N)-1);
        }   
    }
    
    private static long CountFormats(int N){
        if(N==0) return 1;
        long res = CountFormats(N/2);
        res = (res*res) % 100000;
        return N%2==0 ? res : (res*2) % 100000;
}
```

## Explanation

![alt text](https://github.com/wtsanshou/Coding/blob/master/Mathmatic/Combinatorics/Images/DiwaliLightsE.PNG "explanation")
