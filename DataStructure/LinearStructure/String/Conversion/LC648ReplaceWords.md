# LC648. Replace Words

### LeetCode

## Question

In English, we have a concept called root, which can be followed by some other words to form another longer word - let's call this word successor. For 
example, the root an, followed by other, which can form another word another.

Now, given a dictionary consisting of many roots and a sentence. You need to replace all the successor in the sentence with the root forming it. If a successor has many roots can form it, replace it with the root with the shortest length.

You need to output the sentence after the replacement.

**Example 1:**
```
Input: dict = ["cat", "bat", "rat"]
sentence = "the cattle was rattled by the battery"
Output: "the cat was rat by the bat"
```

**Note:**

1.  The input will only have lower-case letters.
2.  1 <= dict words number <= 1000
3.  1 <= sentence words number <= 1000
4.  1 <= root length <= 100
5.  1 <= sentence words length <= 1000

## Solutions

* C++1
```
class Solution {
public:
    vector<string> getWords(string& sentence)
    {
        stringstream ss(sentence);
        string token;
        vector<string> res;
        while(getline(ss, token, ' '))
            res.push_back(token);
        return res;
    }
    
    string getReplaceWord(unordered_map<string, bool>& dmap, string& word, int maxS)
    {
        for(int i=1; i<word.length() && i<=maxS; ++i)
        {
            string temp = word.substr(0, i);
            if(dmap[temp] == true)
                return temp;
        }
        return word;
    }
    
    string replaceWords(vector<string>& dict, string sentence) {
        unordered_map<string, bool> dmap;
        int maxS = 1;
        for(string d : dict)
        {
            dmap[d]=true;
            if(d.length()>maxS)
                maxS = d.length();
        }
     
        vector<string> words = getWords(sentence);
        string res = "";
        if(!words.empty())
            res = getReplaceWord(dmap, words[0], maxS);
        for(int i=1; i<words.size(); ++i)
            res += " " + getReplaceWord(dmap, words[i], maxS);
        return res;
    }
};
```

* Java1
```
public class Solution {
    public String replaceWords(List<String> dict, String sentence) {
        Map<String, Boolean> dmap = new HashMap<>();
        int maxS = 1;
        for(String d : dict) {
            dmap.put(d, true);
            if(d.length() > maxS) maxS = d.length();
        }
        
        String[] words = sentence.split(" ");
        StringBuilder res = new StringBuilder();
        if(words.length > 0)
            res.append(getReplaceWord(dmap, words[0], maxS));
        for(int i=1; i<words.length; ++i)
            res.append(" " + getReplaceWord(dmap, words[i], maxS));
        
        return res.toString();
    }
    
    private String getReplaceWord(Map<String, Boolean> dmap, String word, int maxS){
        for(int i=1; i<word.length() && i<=maxS; ++i){
            String temp = word.substring(0, i);
            if(dmap.containsKey(temp))
                return temp;
        }
        return word;
    }
}
```

## Explanation

**NOTE:** the root is starting from the beginning of every word, otherwise, it could be more complex.

The most straight forword way is to check every word to see if a substring of the word is in the dictionary.

* **worst-case time complexity:** O(n<sup>2</sup>)
* **worst-case space complexity:** O(n)