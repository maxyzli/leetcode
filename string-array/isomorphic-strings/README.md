# Isomorphic Strings

## Solution 1

Map + Set

```java
/**
 * Question   : 205. Isomorphic Strings
 * Complexity : Time: O(n) ; Space: O(n)
 * Topics     : String
 * Date       : 2021/03/19
 */
class Solution {
    public boolean isIsomorphic(String s, String t) {
        if (s.length() != t.length()) {
            return false;
        }

        Map<Character, Character> mapping = new HashMap<>();
        Set<Character> used = new HashSet<>();

        for (int i = 0; i < s.length(); i++) {
            char sChar = s.charAt(i);
            char tChar = t.charAt(i);
            if (!mapping.containsKey(sChar)) {
                if (used.contains(tChar)) {
                    return false;
                }
                mapping.put(sChar, tChar);
                used.add(tChar);
            }
            if (mapping.get(sChar) != tChar) {
                return false;
            }
        }

        return true;
    }
}
```
