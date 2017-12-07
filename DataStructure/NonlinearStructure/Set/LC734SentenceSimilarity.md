# LC734. Sentence Similarity

### LeetCode

## Question

Given two sentences words1, words2 (each represented as an array of strings), and a list of similar word pairs pairs, determine if two sentences are similar.

For example, "great acting skills" and "fine drama talent" are similar, if the similar word pairs are pairs = [["great", "fine"], ["acting","drama"], ["skills","talent"]].

Note that the similarity relation is not transitive. For example, if "great" and "fine" are similar, and "fine" and "good" are similar, "great" and "good" are not necessarily similar.

However, similarity is symmetric. For example, "great" and "fine" being similar is the same as "fine" and "great" being similar.

Also, a word is always similar with itself. For example, the sentences words1 = ["great"], words2 = ["great"], pairs = [] are similar, even though there are no specified similar word pairs.

Finally, sentences can only be similar if they have the same number of words. So a sentence like words1 = ["great"] can never be similar to words2 = ["doubleplus","good"].

**Note:**

* The length of words1 and words2 will not exceed 1000.
* The length of pairs will not exceed 2000.
* The length of each pairs[i] will be 2.
* The length of each words[i] and pairs[i][j] will be in the range [1, 20].

## Solutions

* C#1
```
public bool AreSentencesSimilar(string[] words1, string[] words2, string[,] pairs) {
    if(words1.Length != words2.Length) return false;
    HashSet<string> dict = new HashSet<string>();
    for(int i=0; i<pairs.GetLength(0); ++i)
        dict.Add(pairs[i,0]+pairs[i,1]);
    for(int i=0; i<words1.Length; ++i){
        if(words1[i].Equals(words2[i])) continue;
        if(!dict.Contains(words1[i]+words2[i]) && !dict.Contains(words2[i]+words1[i]))
            return false;
    }
    return true;
}
```

## Explanation

1. Using a hash set to map all the pairs' group.
2. check if the `word1[i]==word2[i]`; or `word1[i]+word2[i]` or `word2[i]+word1[i]` are in the set. If not, they are not sentenses similar.

* **worst-case time complexity:** O(n)
* **worst-case space complexity:** O(n)
