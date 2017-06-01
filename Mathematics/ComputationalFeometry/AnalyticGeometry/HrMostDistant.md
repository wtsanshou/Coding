# Most Distant

### HackerRank

## Question

Keko has N dots in a 2-D coordinate plane. He wants to measure the gap between the most distant two dots. To make the problem easier, Keko decided to change each dot's x or y coordinate to zero.

Help Keko calculate the distance!

**Input Format**

The first line contains an integer, N, the number of dots. 

The next N lines each contain the integer coordinates of the dots in (x,y) fashion.

**Constraints** 

* 2 <= N <= 10<sup>6</sup>
* -10<sup>9</sup> <= x<sub>i</sub>, y<sub>i</sub> <= 10<sup>9</sup>

It is guaranteed that all dots are distinct, and either their x or y coordinate is equal to 0.

**Output Format**

Print the distance between the most distant dots with an absolute error of, at most, 10<sup>-6</sup>.

**Sample Input**
```
4
-1 0
1 0
0 1
0 -1
```

**Sample Output**
```
2.000000
```

**Explanation**

In the sample, the most distant dots are located at (-1,0) and (1,0). 

The distance between them is 2.

## Solution

* C++1
```
double Distance(double p1[2], double p2[2]){
    double x = p1[0] - p2[0];
    double y = p1[1] - p2[1];
    return sqrt(x*x + y*y);
}

int main() {
    int N;
    double x, y;
    cin>>N;
    double p[4][2] = {0};
    for(int i=0; i<N; ++i){
        cin>>x>>y;
        p[0][0] = max(p[0][0], x);
        p[1][0] = min(p[1][0], x);
        p[2][1] = max(p[2][1], y);
        p[3][1] = min(p[3][1], y);
    }
    double res = 0.0;
    for(int i=0; i<3; ++i)
        for(int j=i+1; j<4; ++j)
            res = max(res, Distance(p[i], p[j]));
    //cout<<res<<endl;
    printf("%.12f\n", res);
    return 0;
}
```

* Java1
```
public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        int N = sc.nextInt();
        double x, y;
        double[][] p = new double[4][2];
        for(int i=0; i<N; ++i){
            x = sc.nextDouble();
            y = sc.nextDouble();
            p[0][0] = Math.max(p[0][0], x);
            p[1][0] = Math.min(p[1][0], x);
            p[2][1] = Math.max(p[2][1], y);
            p[3][1] = Math.min(p[3][1], y);
        }
        double res = 0.0;
        for(int i=0; i<3; ++i){
            for(int j=i+1; j<4; ++j)
                res = Math.max(res, Distance(p[i], p[j]));
        }
        System.out.printf("%.12f\n", res);
    }
    
    private static double Distance(double[] p1, double[] p2){
        double x = p1[0] - p2[0];
        double y = p1[1] - p2[1];
        return Math.sqrt(x*x + y*y);
    }
```

## Explanation

This is a simple Geometry question, because the points are all on the x, y axis. We just need to find four farthest points from origin of four axis directions. **Note:** the input points may be less than 4 points or not on all axis directions. It doesn't matter. We just need to find the most distant between the found four points.

I wrote java code first. There are some test cases seemed exceed time limitation. The algorithm is O(n) time complexity. I was thinking could it be less than O(n)? Could it be O(log(n)) or O(1)? However, we need to read the n points at least. It's already O(n).

Then, I wrote C++ code. It passed all tests. Because C++ is faster than Java in HackerRank server?   