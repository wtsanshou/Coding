# LC551. Student Attendance Record I

### LeetCode

## Question

You are given a string representing an attendance record for a student. The record only contains the following three characters:

1.	'A' : Absent.
2.	'L' : Late.
3.	'P' : Present.

A student could be rewarded if his attendance record doesn't contain more than one 'A' (absent) or more than two continuous 'L' (late).

You need to return whether the student could be rewarded according to his attendance record.

**Example 1:**

```
Input: "PPALLP"
Output: True
```

**Example 2:**

```
Input: "PPALLL"
Output: False
```

## Solutions

### Solution 1

* Java
```
public boolean checkRecord(String s){
    char[] ss = s.toCharArray();

    int absent = 0;
    for(char c : ss){
        if(c=='A') absent++;
        if(absent > 1) return false;
    }

    for(int i=1; i<ss.length-1; i++)
        if(ss[i]=='L' && ss[i]==ss[i-1] && ss[i]==ss[i+1])
            return false;
    
    return true;
}
```

There are two scenarios the student cannot get rewarded:

1. The student has more than one `A`.
2. The student has more than two continuous 'L'.

So we can traversal the String two times. First, check if there are more than on `A` in the String `s`; second, check if there is a three continuous `L`.

**Complexity:**

* **worst-case time complexity:** `O(n)`, where `n` is the length of the input `s`.
* **worst-case space complexity:** `O(n)`, where `n` is the length of the input `s`.

### Solution 2

* C++
```
bool checkRecord(string s) {
    int a=0, l=0;
    for(char c : s)
    {
        if(c=='L')
        {
            if(++l>2) return false;
        }
        else 
        {
            l=0;
            if(c=='A'&& ++a>1) return false;
        }
    }
    return true;
}
```

We can check both scenarios in a single traversal. To count continuous `L`, we only increase `l` when met continuous `L` else set `l=0`. The scenario of more than one `A` is very easy to check `c=='A'&& ++a>1`.

**Complexity:**

* **worst-case time complexity:** `O(n)`, where `n` is the length of the input `s`.
* **worst-case space complexity:** `O(1)`.