# LC93. Restore IP Addresses

### LeetCode

## Question

Given a string containing only digits, restore it by returning all possible valid IP address combinations.

A valid IP address consists of exactly four integers (each integer is between 0 and 255) separated by single points.

**Example:**
```
Input: "25525511135"

Output: ["255.255.11.135", "255.255.111.35"]
```

## Solutions

### Solution 1

* Python
```
class Solution:
    def restoreIpAddresses(self, s: str) -> List[str]:
        result = []
        self.back_tracking(0, '', result, s)
        return result
    
    def back_tracking(self, ith: int, ip: str, result: [], s: str):
        if ith == 4 or len(s) == 0:
            if ith == 4 and len(s) == 0:
                result.append(ip)
            return
                
        for i in range(3):
            if i >= len(s) or (i != 0 and s[0] == '0'):
                break
            
            part = s[:i + 1]
            if int(part) <= 255:
                if ith != 0:
                    part = f'.{part}'
                self.back_tracking(ith + 1, ip + part, result, s[i + 1:])
```

Back tracking the possible ips. 

**Note:** 
* heading `0`
* first `.`