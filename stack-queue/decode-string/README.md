# Decode String

## Solution 1

```java
/**
 * Question   : 394. Decode String
 * Complexity : Time: O(n) ; Space: O(n)
 * Topics     : Stack/Queue
 */
class Solution {
    public String decodeString(String s) {
        if (s == null || s.length() == 0) {
            return "";
        }

        int num = 0;
        StringBuilder sb = new StringBuilder();

        Stack<Integer> numStack = new Stack<>();
        Stack<String> strStack = new Stack<>();

        for (char c : s.toCharArray()) {
            if (c >= '0' && c <= '9') {
                num = num * 10 + (c - '0');
            } else if (c == '[') {
                numStack.push(num);
                strStack.push(sb.toString());
                num = 0;
                sb.setLength(0);
            } else if (c == ']') {
                String item = sb.toString();
                int times = numStack.pop();
                for (int i = 1; i < times; i++) {
                    sb.append(item);
                }
                sb.insert(0, strStack.pop());
            } else {
                sb.append(c);
            }
        }

        return sb.toString();
    }
}
```
