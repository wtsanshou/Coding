# LC443. String Compression

### LeetCode

## Question

Given an array of characters, compress it in-place.

The length after compression must always be smaller than or equal to the original array.

Every element of the array should be a character (not int) of length 1.

After you are done modifying the input array in-place, return the new length of the array.

**Follow up:**

Could you solve it using only O(1) extra space?

**Example 1:**

```
Input:
["a","a","b","b","c","c","c"]

Output:
Return 6, and the first 6 characters of the input array should be: ["a","2","b","2","c","3"]
```

**Explanation:**

"aa" is replaced by "a2". "bb" is replaced by "b2". "ccc" is replaced by "c3".

**Example 2:**

```
Input:
["a"]

Output:
Return 1, and the first 1 characters of the input array should be: ["a"]
```

**Explanation:**

Nothing is replaced.

**Example 3:**

```
Input:
["a","b","b","b","b","b","b","b","b","b","b","b","b"]

Output:
Return 4, and the first 4 characters of the input array should be: ["a","b","1","2"].
```

**Explanation:**

Since the character "a" does not repeat, it is not compressed. "bbbbbbbbbbbb" is replaced by "b12".

Notice each digit has it's own entry in the array.

**Note:**

* All characters have an ASCII value in [35, 126].
* 1 <= len(chars) <= 1000.

## Solutions

* C#1
```
public class Solution {
    public int Compress(char[] chars) {
        int same=1, j=0, n=chars.Length;
        for(int i=0; i<n-1; ++i){
            if(chars[i] == chars[i+1])
                same++;
            else{
                chars[j++] = chars[i];
                if(same != 1) 
                    j = copyNumIn(j, chars, same);
                same = 1;
            }
        }
        chars[j++] = chars[n-1];
        if(same != 1) {
            j = copyNumIn(j, chars, same);
        } 
        return j;
    }
    
    private int copyNumIn(int j, char[] chars, int same){
        string s = same.ToString();
        for(int i=0; i<s.Length; ++i)
            chars[j++] = s[i];
        return j;
    }
}
```

## Explanation

At the begining, I thought I just need to count the length after the compression. After see the test, I notice I have to modify the input array in-place. So, clearing the real requirements is very very important.

The idea is quite simple, just count the number of the continous values. If the number is more than `1`, convert the number to string and copy it the the input array after the compressed value.

But, I think this compress question might have some problem for decompress. Because the ASCII value in [35, 126], if the value is a number, it will be confused when you decompress it.

* **worst-case time complexity:** O(n)
* **worst-case space complexity:** O(1).
