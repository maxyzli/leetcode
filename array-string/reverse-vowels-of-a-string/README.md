# Reverse Vowels of a String

## Solution 1

Two Pointers

```java
/**
 * Question   : 345. Reverse Vowels of a String
 * Topics     : String
 * Complexity : Time: O(n) ; Space: O(n)
 */
class Solution {
    public String reverseVowels(String s) {
        Set<Character> set = new HashSet<>();
        set.add('a');
        set.add('e');
        set.add('i');
        set.add('o');
        set.add('u');

        int low = 0;
        int high = s.length() - 1;

        StringBuilder sb = new StringBuilder(s);

        while (low < high) {
            while (low < high && !set.contains(Character.toLowerCase(sb.charAt(low)))) {
                low++;
            }
            while (low < high && !set.contains(Character.toLowerCase(sb.charAt(high)))) {
                high--;
            }
            if (low < high) {
                char temp = sb.charAt(low);
                sb.setCharAt(low, sb.charAt(high));
                sb.setCharAt(high, temp);
                low++;
                high--;
            }
        }

        return sb.toString();
    }
}
```
