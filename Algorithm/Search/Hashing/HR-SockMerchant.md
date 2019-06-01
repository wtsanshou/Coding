# HR. Sock Merchant

John works at a clothing store. He has a large pile of socks that he must pair by color for sale. Given an array of integers representing the color of each sock, determine how many pairs of socks with matching colors there are.

For example, there are `n=7` socks with colors `ar=[1,2,1,2,1,3,2]`. There is one pair of color `1` and one of color `2`. There are three odd socks left, one of each color. The number of pairs is `2`.

**Function Description**

Complete the sockMerchant function in the editor below. It must return an integer representing the number of matching pairs of socks that are available.
sockMerchant has the following parameter(s):

```
n: the number of socks in the pile
ar: the colors of each sock
```

**Input Format**

```
The first line contains an integer `n`, the number of socks represented in `ar`. 
The second line contains `n` space-separated integers describing the colors `ar[i` of the socks in the pile.
```

**Constraints**

* 1 <= n <= 100
* 1 <= ar[i] <= 100 where 0 <= i < n

**Output Format**

```
Return the total number of matching pairs of socks that John can sell.
```

**For example**

```
Sample Input
9
10 20 20 10 10 30 50 10 20
Sample Output
3
```

## Solutions

### Solution 1

* Java
```
import java.io.*;
import java.math.*;
import java.security.*;
import java.text.*;
import java.util.*;
import java.util.concurrent.*;
import java.util.regex.*;

public class Solution {

    // Complete the sockMerchant function below.
    static int sockMerchant(int n, int[] ar) {
        Map<Integer, Integer> count = new HashMap<>();
        int res = 0;
        for(int i=0; i<n; i++){
            int num = count.getOrDefault(ar[i], 0);
            if(num==0) count.put(ar[i], 1);
            else if(num>0){
                res++;
                count.put(ar[i], 0);
            }
        }
        return res;
    }

    private static final Scanner scanner = new Scanner(System.in);

    public static void main(String[] args) throws IOException {
        BufferedWriter bufferedWriter = new BufferedWriter(new FileWriter(System.getenv("OUTPUT_PATH")));

        int n = scanner.nextInt();
        scanner.skip("(\r\n|[\n\r\u2028\u2029\u0085])?");

        int[] ar = new int[n];

        String[] arItems = scanner.nextLine().split(" ");
        scanner.skip("(\r\n|[\n\r\u2028\u2029\u0085])?");

        for (int i = 0; i < n; i++) {
            int arItem = Integer.parseInt(arItems[i]);
            ar[i] = arItem;
        }

        int result = sockMerchant(n, ar);

        bufferedWriter.write(String.valueOf(result));
        bufferedWriter.newLine();

        bufferedWriter.close();

        scanner.close();
    }
}
```

* Java
```
static int sockMerchant(int n, int[] ar) {
    int[] count = new int[101];
    int res = 0;
    for(int i=0; i<n; i++){
        int num = count[ar[i]];
        if(num==0) count[ar[i]] = 1;
        else if(num>0){
            res++;
            count[ar[i]] = 0;
        }
    }
    return res;
}
```

Using a map to store single socks, when found a pair of socks, clean it in the map.

**Complexity:**

* **worst-case time complexity:** `O(n)`, where `n` is the length of the input `ar`.
* **worst-case space complexity:** `O(n)`, where `n` is the length of the input `ar`.
