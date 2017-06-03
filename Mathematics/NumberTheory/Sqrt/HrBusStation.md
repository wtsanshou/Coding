# Bus Station

### HackerRank

## Question

There are  groups of friends, and each group is numbered from 1 to n. The ith group contains  people.

They live near a bus stop, and only a single bus operates on this route. An empty bus arrives at the bus stop and all the groups want to travel by the bus.
However, group of friends do not want to get separated. So they enter the bus only if the bus can carry the entire group.

Moreover, the groups do not want to change their relative positioning while travelling. In other words, group 3 cannot travel by bus, unless group 1 and group 2 have either (a) already traveled by the bus in the previous trip or (b) they are also sitting inside the bus at present.

You are given that a bus of size x can carry x people simultaneously. 

Find the size x of the bus so that (1) the bus can transport all the groups and (2) every time when the bus starts from the bus station, there is no empty space in the bus (i.e. the total number of people present inside the bus is equal to x)?

**Input Format** 

The first line contains an integer n (1 <= n <= 10<sup>5</sup>) . The second line contains n space-separated integers a1, a2,…, a<sub>n</sub> (1 <= a<sub>i</sub> <= 10<sup>4</sup>) .

**Output Format**

Print all possible sizes of the bus in an increasing order.

**Sample Input**
```
8
1 2 1 1 1 2 1 3
```

**Sample Output**
```
3 4 6 12
```

**Sample Explanation**

In the above example, a1 = 1, a2 = 2, a3 = 1, a4 = 1, a5 = 1, a6 = 2, a7 = 1, a8 = 3.

If x = 1 : In the first trip, a1 go by the bus. There will be no second trip because the bus cannot accommodate group 2. Hence "x = 1" is not the required answer.

If x = 2 : No bus trip is possible. That's because a1 cannot go alone, as one seat will be left vacant in the bus. And, a1 & a2 cannot go together, because the bus is cannot accommodate both the groups simultaneously.

If x = 3 : In the first trip, a1 & a2 go by the bus. In the second trip, a3, a4 & a5 go by the bus. In the third trip, a6 & a7 go by the bus. In the fourth trip, a8 go by the bus.

If x = 4 : In the first trip, a1, a2 & a3 go by the bus. In the second trip, a4, a5 & a6 go by the bus. In the third trip,  a7& a8 go by the bus.

Similarly you can figure out the output for x= 5, 6 & 7.

## Solution

* Java1
```
public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        int n = sc.nextInt();
        Set<Integer> sumSet = new HashSet<Integer>();
        List<Integer> res = new ArrayList<Integer>();
        int sum = 0;
        for(int i=0; i<n; ++i){
            sum += sc.nextInt();
            sumSet.add(sum);
        }
        int s = (int)Math.sqrt(sum);
        for(int i=1; i<=s; ++i){
            if(sum % i != 0) continue;
            if(IsPossibleSize(i, sum, sumSet))
                res.add(i);
            if(sum/i != i && IsPossibleSize(sum/i, sum, sumSet))
                res.add(sum/i);
        }
        Collections.sort(res);
        for(int i=0; i<res.size(); ++i)
            System.out.print(res.get(i) + " ");
        System.out.println();
    }
    
    private static boolean IsPossibleSize(int size, int sum, Set<Integer> sumSet){
        int sumS = size;
        while(sumS < sum){
            if(!sumSet.contains(sumS))
                return false;
            sumS += size;
        }
        return true;
    }
```

## Explanation

The hint is the `size * x` (1 <= x <= sum/size) must be contained in the sum sets (sum from 1<sup>st</sup> to i<sup>th</sup> (1<=i<=n)).