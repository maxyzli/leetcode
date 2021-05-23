# Basic Calculator

## Solution 1

Stack

```java
/**
 * Question   : 224. Basic Calculator
 * Complexity : Time: O(n) ; Space: O(n)
 * Topics     : Stack/Queue
 */
class Solution {
    public int calculate(String s) {
        Stack<Integer> preSignStack = new Stack<>();
        Stack<Integer> resStack = new Stack<>();

        int preSign = 1;
        int num = 0;
        int res = 0;
        for (char c : s.toCharArray()) {
            if ('0' <= c && c <= '9') {
                num = num * 10 + (c - '0');
            } else if (c == '+') {
                res += preSign * num;
                num = 0;
                preSign = 1;
            } else if (c == '-') {
                res += preSign * num;
                num = 0;
                preSign = -1;
            } else if (c == '(') {
                resStack.push(res);
                preSignStack.push(preSign);
                // Reset
                preSign = 1;
                res = 0;
            } else if (c == ')') {
                res += preSign * num;
                num = 0;
                res *= preSignStack.pop();
                res = resStack.pop() + res;
            }
        }

        return res + preSign * num;
    }
}
```
