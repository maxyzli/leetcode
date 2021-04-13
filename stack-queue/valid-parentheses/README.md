# Valid Parentheses

## Solution 1

Stack

```java
/**
 * Question   : Valid Parentheses
 * Complexity : Time: O(n) ; Space: O(n)
 * Topic      : Stack
 */
public class Solution {
    public boolean isValid(String s) {
        if (s == null || s.length() == 1) {
            return false;
        }

        Stack<Character> stack = new Stack<>();

        for (int i = 0; i < s.length(); i++) {
            char c = s.charAt(i);
            if (c == '(' || c == '[' || c == '{') {
                stack.push(c);
            } else {
                if (stack.isEmpty()) return false;
                if (!isPair(stack.pop(), c)) return false;
            }
        }

        return stack.isEmpty() ? true : false;
    }

    private boolean isPair(char o, char c) {
        if ((o == '(' && c == ')') || o == '[' && c == ']' || o == '{' && c == '}') {
            return true;
        }
        return false;
    }
}
```
