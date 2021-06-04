# Partition Labels

## Solution 1

```java
/**
 * Question   : 763. Partition Labels
 * Complexity : Time: O(n) ; Space: O(1)
 * Topics     : Sliding Window
 */
class Solution {
    public List<Integer> partitionLabels(String s) {
        int[] c2Index = new int[26];

        for (int i = 0; i < s.length(); i++) {
            c2Index[s.charAt(i) - 'a'] =  i;
        }

        int left = 0;
        int right = 0;

        List<Integer> res = new ArrayList<>();

        for (int i = 0; i < s.length(); i++) {
            char c = s.charAt(i);
            right = Math.max(right, c2Index[c - 'a']);
            if (i == right) {
                res.add(right - left + 1);
                left = right + 1;
            }
        }

        return res;
    }
}
```
