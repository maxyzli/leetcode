# Word Pattern

## Solution 1

We use hash table to stroe the two way mappings.

```java
/**
 * Question   : 290. Word Pattern
 * Complexity : Time: O(p) ; Space: O(p+s)
 * Topics     : Hash Table
 */
class Solution {
    public boolean wordPattern(String pattern, String s) {
        String[] strings = s.split(" ");

        if (pattern.length() != strings.length) {
            return false;
        }

        Map<Character, String> charToStr = new HashMap<>();
        Map<String, Character> strToChar = new HashMap<>();

        for (int i = 0; i < pattern.length(); i++) {
            char c = pattern.charAt(i);

            if (charToStr.containsKey(c)) {
                if (!charToStr.get(c).equals(strings[i])) {
                    return false;
                }
            } else {
                if (strToChar.containsKey(strings[i])) {
                    return false;
                }

                charToStr.put(c, strings[i]);
                strToChar.put(strings[i], c);
            }
        }

        return true;
    }
}
```
