# Isomorphic Strings

## Solution 1

Map

```java
/**
 * Question   : 205. Isomorphic Strings
 * Complexity : Time: O(n) ; Space: O(n)
 * Topics     : Hash Table
 */
class Solution {
    public boolean isIsomorphic(String s, String t) {
        if (s.length() != t.length()) {
            return false;
        }

        Map<Character, Character> sTot = new HashMap<>();
        Map<Character, Character> tTos = new HashMap<>();

        for (int i = 0; i < s.length(); i++) {
            char charS = s.charAt(i);
            char charT = t.charAt(i);

            if (sTot.containsKey(charS)) {
                if (sTot.get(charS) != charT) {
                    return false;
                }
            } else {
                if (tTos.containsKey(charT)) {
                    return false;
                }
                sTot.put(charS, charT);
                tTos.put(charT, charS);
            }
        }

        return true;
    }
}
```
