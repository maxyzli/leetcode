# Basic Calculator II

## Solution 1

Stack

```java
/**
 * Question   : 227. Basic Calculator II
 * Complexity : Time: O(n) ; Space: O(n)
 * Topics     : Stack/Queue
 */
class Solution {
    public int calculate(String s) {
        if (s == null || s.length() == 0) {
            return 0;
        }

        Stack<Integer> numStack = new Stack<>();

        char preSign = '+';
        int i = 0;
        while (i < s.length()) {
            if (s.charAt(i) == ' ') {
                i++;
            } else if (Character.isDigit(s.charAt(i))) {
                int num = 0;
                while (i < s.length() && Character.isDigit(s.charAt(i))) {
                    num = num * 10 + (s.charAt(i) - '0');
                    i++;
                }
                if (preSign == '+') {
                    numStack.push(num);
                } else if (preSign == '-') {
                    numStack.push(-num);
                } else if (preSign == '*') {
                    numStack.push(numStack.pop() * num);
                } else if (preSign == '/') {
                    numStack.push(numStack.pop() / num);
                }
            } else {
                preSign = s.charAt(i);
                i++;
            }
        }

        int res = 0;
        while (!numStack.isEmpty()) {
            res += numStack.pop();
        }

        return res;
    }
}
```
