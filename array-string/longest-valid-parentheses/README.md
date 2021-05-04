# Longest Valid Parentheses

## Solution 1

Stack

```java
/**
 * Question   : 32. Longest Valid Parentheses
 * Topics     : String
 * Complexity : Time: O(n) ; Space: O(n)
 */
public class Solution {
    public int longestValidParentheses(String s) {
        if (s == null || s.length() == 0) {
            return 0;
        }

        int longest = 0;

        Stack<Integer> stack = new Stack<>();

        for (int i = 0; i < s.length(); i++) {
            char c = s.charAt(i);

            if (c == '(') {
                stack.add(i);
                continue;
            }

            // c is ')' now.

            // If stack is empty or the last element in stack is ')'
            // we add the index of current ')' to the stack.
            if (stack.isEmpty() || s.charAt(stack.peek()) == ')') {
                stack.add(i);
                continue;
            }

            // Here stack is not empty and the last in stack element is '('.
            // We find a match so pop '(' out of the stack.
            stack.pop();

            // If stack is empty means it's valid from the beginning until this index.
            // The length is i + 1.
            if (stack.isEmpty()) {
                longest = Math.max(longest, i + 1);
            } else {
                longest = Math.max(longest, i - stack.peek());
            }
        }

        return longest;
    }
}
```
