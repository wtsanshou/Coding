# LC556. Next Greater Element III

### LeetCode

Given a positive 32-bit integer n, you need to find the smallest 32-bit integer which has exactly the same digits existing in the integer n and is greater in value than n. If no such positive 32-bit integer exists, you need to return -1.

**Example 1:**
```
Input: 12
Output: 21
```

**Example 2:**
```
Input: 21
Output: -1
```

## Solutions

### Solution 1

* C++
```
class Solution {
public:
    void reverse(string& s, int left)
    {
        int right = s.length()-1;
        while(left < right)
            swap(s[left++], s[right--]);
    }
    int nextGreaterElement(int n) {
        string s = to_string(n);

        int i = s.length()-2;
        while(i>=0 && s[i]>=s[i+1]) i--;
        if(i==-1) return -1;

        int j=s.length()-1;
        while(s[i] >= s[j]) j--;
        swap(s[i], s[j]);

        reverse(s, i+1);
        
        try{
            return stoi(s);
        }
        catch(exception e){
            return -1;
        }
        //long res = stol(s);
        //return res>INT_MAX ? -1 : res;
    }
};
```

The idea is similar with * <a href="LC31NextPermutation.md">LC31. Next Permutation</a>

* **worst-case time complexity:** `O(1)`. 
* **worst-case space complexity:** `O(1)`
