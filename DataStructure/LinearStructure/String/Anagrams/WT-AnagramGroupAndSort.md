# WT. Anagram Group And Sort

## Question

Given a list words, group the anagram together. Then sort the groups by their size in ascending order. Reture a list these group sizes.

**Example 1**
```
input:
["cat", "god", "act", "dog", "gdo"]

output:
[2, 3]
```

**Restrictions:**

1. All words are consisted of lower case letters

## Solutions

### Solution 1

* Java
```
public List<Integer> groupSort(String[] input) {
    Map<String, List<String>> map = new HashMap<>();
    for (String word : input) {
        String sortedWord = sort(word);
        if (!map.containsKey(sortedWord)) {
            map.put(sortedWord, new ArrayList<>());
        }

        map.get(sortedWord).add(word);
    }

    List<List<String>> values = new ArrayList<>(map.values());
    Collections.sort(values, (a, b) -> Integer.compare(a.size(), b.size()));

    List<Integer> res = new ArrayList<>();
    for(List<String> value : values)
        res.add(value.size());

    return res;
}

private String sort(String word) {
    final char[] arr = word.toCharArray();
    Arrays.sort(arr);
    return new String(arr);
}
```

When I see the question, I know the grouping is the trick part of the question. When grouping done, the rest is very easy. 

When we check a word, we have to quickly find out the anagram group of it. Checking all existing groups is one solution, but it will be very slow. So I came out the idea to use map. Because the sorted anagram will be the same word, so we can used the sorted word as key. Then store all anagrams under their sorted key.

I forgot to ask what is the order if two groups have the same size.

**Complexity:**

* **worst-case time complexity:** `O(n * max(log(n), m*log(m)))`, where `n` is the length of `input`, `m` is the maximum length word in the `input`.
* **worst-case space complexity:** `O(n)`, where `n` is the length of `input`.