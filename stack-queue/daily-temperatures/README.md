# Daily Temperatures

## Solution 1

```java
/**
 * Question   : 739. Daily Temperatures
 * Complexity : Time: O(n) ; Space: O(n)
 * Topics     : Stack
 */
class Solution {
    public int[] dailyTemperatures(int[] T) {
        if (T == null || T.length == 0) {
            return new int[]{};
        }

        Stack<Integer> stack = new Stack<>();
        int[] output = new int[T.length];

        for (int i = T.length - 1; i >= 0; i--) {
            while (!stack.isEmpty() && T[i] >= T[stack.peek()]) {
                stack.pop();
            }
            if (!stack.isEmpty()) {
                output[i] = stack.peek() - i;
            }
            stack.add(i);
        }

        return output;
    }
}
```
