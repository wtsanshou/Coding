# LC393. UTF-8 Validation

### LeetCode

## Question

A character in UTF8 can be from 1 to 4 bytes long, subjected to the following rules:

1. For 1-byte character, the first bit is a 0, followed by its unicode code.
2. For n-bytes character, the first n-bits are all one's, the n+1 bit is 0, followed by n-1 bytes with most significant 2 bits being 10.

This is how the UTF-8 encoding would work:

```
   Char. number range  |        UTF-8 octet sequence
      (hexadecimal)    |              (binary)
   --------------------+---------------------------------------------
   0000 0000-0000 007F | 0xxxxxxx
   0000 0080-0000 07FF | 110xxxxx 10xxxxxx
   0000 0800-0000 FFFF | 1110xxxx 10xxxxxx 10xxxxxx
   0001 0000-0010 FFFF | 11110xxx 10xxxxxx 10xxxxxx 10xxxxxx
```

Given an array of integers representing the data, return whether it is a valid utf-8 encoding.

**Note:**

The input is an array of integers. Only the least significant 8 bits of each integer is used to store the data. This means each integer represents only 1 byte of data.

**Example 1:**

data = [197, 130, 1], which represents the octet sequence: 11000101 10000010 00000001.

Return true.

It is a valid utf-8 encoding for a 2-bytes character followed by a 1-byte character.

**Example 2:**

data = [235, 140, 4], which represented the octet sequence: 11101011 10001100 00000100.

Return false.

The first 3 bits are all one's and the 4th bit is 0 means it is a 3-bytes character.

The next byte is a continuation byte which starts with 10 and that's correct.
But the second continuation byte does not start with 10, so it is invalid.

## Solutions

* C++1
```
class Solution {
public:
    int getTypeOfUTF8(int first)
    {
        if(first<0 || first>=256) return -1;
        if((first & 248) == 240) return 3;
        if((first & 240) == 224) return 2;
        if((first & 224) == 192) return 1;
        if((first & 128) == 0) return 0;
        return -1;
    }
    bool isValidedFollower(int follow)
    {
        if(follow<0 || follow>=256) return false;
        return (follow&192) == 128;
    }
    bool validUtf8(vector<int>& data) {
        int i=0, follow=0, n=data.size();
        while(i<n)
        {
            follow = getTypeOfUTF8(data[i]);
            if(follow==-1) return false;
            while(follow>0)
            {
                if(i+1==n || !isValidedFollower(data[i+1])) return false;
                i++;
                follow--;
            }
            i++;
        }
        return i==n && follow==0;
    }
};
```

* C++2
```
bool validUtf8(vector<int>& data) {
    int count=0;
    for(int byte : data)
    {
        if(count==0)
        {
            if(byte>>5 == 0b110) count = 1; //C++14 binary
            else if(byte>>4 == 0b1110) count = 2;
            else if(byte>>3 == 0b11110) count = 3;
            else if(byte>>7 == 0b1) return false;
        }
        else
        {
            if(byte>>6 != 0b10) return false;
            count--;
        }
    }
    return count == 0;
}
```

## Explanation

Check from the first integer:

If it's the first byte of the UTF-8 octet sequence, the starting bits could be:

1. `110` : one more byte following
2. `1110` : two more byte following
3. `11110` : three more byte following
4. `0` : zero more byte following
5. `10` or `11111` : return false

If it's not the first byte of the UTF-8 octet sequence, the starting bits should be: `10`

**NOTE:** the solution 2 doesn't consider negative value and value more than 255. 

* **worst-case time complexity:** O(n)
* **worst-case space complexity:** O(1)