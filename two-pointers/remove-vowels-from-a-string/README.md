# Remove Vowels from a String

## Solution 1

```java
/**
 * Question   : 1119. Remove Vowels from a String
 * Complexity : Time: O(n) ; Space: O(1)
 * Topics     : String
 */
class Solution {
    public String removeVowels(String s) {
        Set<Character> set = new HashSet<>();
        set.add('a');
        set.add('e');
        set.add('i');
        set.add('o');
        set.add('u');

        StringBuilder sb = new StringBuilder(s);

        int i = 0;
        int j = 0;

        while (j < sb.length()) {
            if (!set.contains(sb.charAt(j))) {
                swap(sb, i++, j++);
            } else {
                j++;
            }
        }

        return sb.substring(0, i);
    }

    private void swap(StringBuilder sb, int i, int j) {
        char temp = sb.charAt(i);
        sb.setCharAt(i, sb.charAt(j));
        sb.setCharAt(j, temp);
    }
}
```
