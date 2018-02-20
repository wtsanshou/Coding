# LC756. Pyramid Transition Matrix

We are stacking blocks to form a pyramid. Each block has a color which is a one letter string, like `Z`.

For every block of color `C` we place not in the bottom row, we are placing it on top of a left block of color `A` and right block of color `B`. We are allowed to place the block there only if `(A, B, C)` is an allowed triple.

We start with a bottom row of bottom, represented as a single string. We also start with a list of allowed triples allowed. Each allowed triple is represented as a string of length 3.

Return true if we can build the pyramid all the way to the top, otherwise false.

**Example 1:**
```
Input: bottom = "XYZ", allowed = ["XYD", "YZE", "DEA", "FFF"]
Output: true
```

**Explanation:**

We can stack the pyramid like this:
```
    A
   / \
  D   E
 / \ / \
X   Y   Z
```

This works because ('X', 'Y', 'D'), ('Y', 'Z', 'E'), and ('D', 'E', 'A') are allowed triples.

**Example 2:**
```
Input: bottom = "XXYX", allowed = ["XXX", "XXY", "XYX", "XYY", "YXZ"]
Output: false
```

**Explanation:**

We can't stack the pyramid to the top.

Note that there could be allowed triples (A, B, C) and (A, B, D) with C != D.

**Note:**

* bottom will be a string with length in range [2, 8].
* allowed will have length in range [0, 200].
* Letters in all strings will be chosen from the set {'A', 'B', 'C', 'D', 'E', 'F', 'G'}.

## Solutions

* Java1
```
class Solution {
    public boolean pyramidTransition(String bottom, List<String> allowed) {
        Map<String, List<String>> dict = new HashMap<>();
        for(String a : allowed){
            String a1 = a.substring(0,2);
            String a2 = a.substring(2);
            if(!dict.containsKey(a1)){
                dict.put(a1, new ArrayList<String>());
            }
            dict.get(a1).add(a2);
        }
        return isPyramid(bottom, dict);
    }
    
    private boolean isPyramid(String bottom, Map<String, List<String>> dict){
        if(bottom.length() <= 1) return true;
        List<String> upLayer = new ArrayList<>();
        addLayer("", 0, upLayer, bottom, dict);
        for(String up : upLayer)
            if(isPyramid(up, dict)) return true;
        return false;
    } 
    
    private void addLayer(String aLayer, int i, List<String> upLayer, String bottom, Map<String, List<String>> dict){
        if(i >= bottom.length()-1){
            upLayer.add(aLayer);
            return;
        }
        String start = bottom.substring(i, i+2);
        if(!dict.containsKey(start)) return;
        for(String c : dict.get(start))
            addLayer(aLayer+c, i+1, upLayer, bottom, dict);
    }
}
```

## Explanation

Using a hashmap to classify all triples based on the first the two letters in the `allowed` list.

Find out all possible up layer Strings. I used back tracking to collect all possible up layer Strings. (Time consumption here)

With recursive idea, if there has at least one `uplayer` satisfy pyramid transition, the `bottom` is pyramid transition.

* **worst-case time complexity:** O(B*(N/B)<sup>B</sup>), where B is length of `bottom`, N is the size of `allowed`.
* **worst-case space complexity:** O((N/B)<sup>B</sup>)