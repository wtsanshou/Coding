# Jim and the Jokes

### HackerRank

## Question

Jim runs a big burger restaurant and, to entertain his customers, he always tell them jokes. He is running out of jokes and he needs you to help him find new ones.

An often heard programmer joke goes like this:

"Why do programmers always mix up Christmas and Halloween? Because Dec 25 is Oct 31".

Got it? :-) It is because 25<sub>10</sub> (25 in Decimal) is equal to 31<sub>8</sub> (31 in Octal).
If we are talking about dates, then let m be the month and d be the date and the corresponding value be f(m, d) = dm (d in base m). Let's describe some slightly different jokes:

"Why do programmers always mix up event x and event y? Because f(mx, dx) = f(my, dy) ".

Here mx means the month of event x and dx the day of event x. Similar for my and dy.

Jim knows that his customers love this kind of jokes. That's why he gives you a calendar with N events in it and asks you to count the number of such jokes he can create using the given events.

Two jokes ((x1, x2) and (y1, y2)) differ if they don't contain the same events.

**Note:**

* The given numbers are all represented with digits from 0-9, that's why for months like 11 or 12, we can't use additional characters to represent 10 or 11.
* It might happen, that a special event cannot be used for a joke because the base conversion is invalid. For example 25<sub>2</sub> is not possible since base 2 can only contain digits 0 and 1.
* Unary base is invalid.
* Two events can have the same date.

**Input Format**

On the first line you will get N. The following N lines you will be given the dates mi, di of the special events, each separated by a single space.

**Output Format**

Print the number of jokes Jim can make.

**Constraints**

* 1 <= N <= 10<sub>5</sub>
* (mi, di) will be a valid date in the Gregorian Calendar without leap day.

**Sample Input**
```
2
10 25
8 31
```

**Sample Output**
```
1
```

**Sample Input**
```
2
2 25
2 25
```

**Sample Output**
```
0
```

**Sample Input**
```
2
11 10
10 11
```

**Sample Output**
```
1
```

**Explanation**

There are two special events happening on (10, 25) and (8, 31). He can make one joke, namely the one described in the description.

In the second test case there are no valid dates we can use for our jokes since 25 is not defined for base 2.

In the third test case f(11, 10) = 1011 = 1110 = f(10, 11).

## Solutions

* Java1
```
public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        int N = sc.nextInt();
        int m, d;
        HashMap<Integer, Integer> count = new HashMap();
        for(int i=0; i<N; ++i){
            m = sc.nextInt();
            d = sc.nextInt();
            int val10 = getVal(m, d);
            if(val10 != 0)
                count.put(val10, count.getOrDefault(val10, 0) + 1);
        }
        long res = 0;
        for(Integer key : count.keySet()){
            long val = count.get(key);
            res += (val * (val-1)) / 2;
        }
        System.out.println(res);
    }
    
    private static int getVal(int m, int d){
        if(m < 10){
            int day = d;
            while(day>0){
                if(day%10 >= m) return 0;
                day /= 10;
            }
        }
        int res =0, base=1;
        while(d > 0){
            res += (d%10) * base;
            d /= 10;
            base *= m;
        }
        return res;
    }
```

## Explanation

The idea of this algorithm is to convert every date to 10 based number, and count the appeard times of each number.

**Note:** don't count no valid dates. The no valid dates is that any digit of day equals or larger than number of month.

`(mi, di) will be a valid date in the Gregorian Calendar without leap day`. A valid date here has no 0 month or 0 day. Therefor, the converted number must be positive numbers. Thus, I set no valid dates as 0;

**Corner case:** A valid date appeared 10<sub>5</sub> times. 

The result will be **10<sub>5</sub> * (10<sub>5</sub> - 1) / 2**. It will be out of Integer range.