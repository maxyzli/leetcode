# Remove All Adjacent Duplicates In String

## Solution 1

Stack + StringBuilder

```java
/**
 * Question   : 1047. Remove All Adjacent Duplicates In String
 * Complexity : Time: O(n) ; Space: O(n)
 * Topics     : Stack
 */
class Solution {
    public String removeDuplicates(String S) {
        if (S == null || S.length() == 0) {
            return "";
        }

        Stack<Character> stack = new Stack<>();

        for (int i = S.length() - 1; i >= 0; i--) {
            char c = S.charAt(i);
            if (!stack.isEmpty() && stack.peek() == c) {
                stack.pop();
            } else {
                stack.add(c);
            }
        }

        StringBuilder sb = new StringBuilder();
        while (!stack.isEmpty()) {
            sb.append(stack.pop());
        }

        return sb.toString();
    }
}
```

## Solution 2

StringBuilder

```java
/**
 * Question   : 1047. Remove All Adjacent Duplicates In String
 * Complexity : Time: O(n) ; Space: O(n)
 * Topics     : Stack
 */
class Solution {
    public String removeDuplicates(String S) {
        if (S == null || S.length() == 0) {
            return "";
        }

        StringBuilder sb = new StringBuilder();

        for (int i = 0; i < S.length(); i++) {
            char c = S.charAt(i);

            if (sb.length() > 0 && sb.charAt(sb.length() - 1) == c) {
                sb.deleteCharAt(sb.length() - 1);
            } else {
                sb.append(c);
            }
        }

        return sb.toString();
    }
}
```
