# LC929. Unique Email Addresses

### LeetCode

## Question

Every email consists of a local name and a domain name, separated by the @ sign.

For example, in alice@leetcode.com, alice is the local name, and leetcode.com is the domain name.

Besides lowercase letters, these emails may contain '.'s or '+'s.

If you add periods ('.') between some characters in the local name part of an email address, mail sent there will be forwarded to the same address without dots in the local name.  For example, "alice.z@leetcode.com" and "alicez@leetcode.com" forward to the same email address.  (Note that this rule does not apply for domain names.)

If you add a plus ('+') in the local name, everything after the first plus sign will be ignored. This allows certain emails to be filtered, for example m.y+name@email.com will be forwarded to my@email.com.  (Again, this rule does not apply for domain names.)

It is possible to use both of these rules at the same time.

Given a list of emails, we send one email to each address in the list.  How many different addresses actually receive mails? 

**Example 1:**
```
Input: ["test.email+alex@leetcode.com","test.e.mail+bob.cathy@leetcode.com","testemail+david@lee.tcode.com"]
Output: 2
Explanation: "testemail@leetcode.com" and "testemail@lee.tcode.com" actually receive mails
```

**Note:**

* 1 <= emails[i].length <= 100
* 1 <= emails.length <= 100
* Each emails[i] contains exactly one '@' character.

## Solutions

* Scala1
```
object Solution {
    def numUniqueEmails(emails: Array[String]): Int = {
        emails.map(email => parse(email)).toSet.size
    }
    
    def parse(email: String): String = {
        val strs = email.split("@")
        val end = strs(0).indexOf("+")
        val left = (if(end>0) strs(0).substring(0,end) else strs(0)).toCharArray.filter(_!='.').mkString
        left+strs(1)
    }
}
```

* Scala2 (pass the tests, but cannot parse the local name without `+`)
```
object Solution {
    def numUniqueEmails(emails: Array[String]): Int = {
        emails.map(email => parse(email)).toSet.size
    }
    
    def parse(email: String): String = {
        val strs = email.split("@")
        strs(0).substring(0,strs(0).indexOf("+")).replace(".","")+strs(1)
    }
}
```

## Explanation

The main question is to parse the local name. Just find the substring before the first `+`, then remove the `.`. Finally, using set to remove duplicate emails.

* **worst-case time complexity:** O(N*M), where `N` is the length of the array `emails` and `M` is the maximum length of the emails.
* **worst-case space complexity:** O(N*M), where `N` is the length of the array `emails` and `M` is the maximum length of the emails.
