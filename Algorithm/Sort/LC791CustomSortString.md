# LC791. Custom Sort String

### LeetCode

## Question

S and T are strings composed of lowercase letters. In S, no letter occurs more than once.

S was sorted in some custom order previously. We want to permute the characters of T so that they match the order that S was sorted. More specifically, if x occurs before y in S, then x should occur before y in the returned string.

Return any permutation of T (as a string) that satisfies this property.

**Example :**
```
Input: 
S = "cba"
T = "abcd"
Output: "cbad"
```

**Explanation:** 

"a", "b", "c" appear in S, so the order of "a", "b", "c" should be "c", "b", and "a". 

Since "d" does not appear in S, it can be at any position in T. "dcba", "cdba", "cbda" are also valid outputs.

**Note:**

* S has length at most 26, and no character is repeated in S.
* T has length at most 200.
* S and T consist of lowercase letters only.

## Solutions

* Java1
```
class Solution {
    public String customSortString(String S, String T) {
        char[] result = T.toCharArray();
        int[] order = new int[26];
        char [] newOrder = new char[256];
        for(int i=0; i<S.length(); ++i)
            order[S.charAt(i) - 'a'] = i;
        for(int i=0; i<result.length; ++i){
            if( order[result[i]-'a'] != 0){
                result[i] = (char)('z' + order[result[i]-'a']);
                newOrder[result[i]] = T.charAt(i);
            }
        }
        Arrays.sort(result);
        for(int i=0; i<result.length; ++i){
            if(result[i] > 'z')
                result[i] = newOrder[result[i]];
        }
        return new String(result);
    }
}
```

## Explanation

In String `T`, replace all characters which appare in String `S` by characters after `z` with the order in String `S`. At the same time, remember the replaced characters.

Then sort the String T.

Change back all replaced characters in String `T`.

* **worst-case time complexity:** O(N*log(N)), where `N` is the length of the String `T`.
* **worst-case space complexity:** O(N)