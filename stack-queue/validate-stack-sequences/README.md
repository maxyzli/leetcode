# Validate Stack Sequences

## Solution 1

Stack & Set

```java
class Solution {
    public boolean validateStackSequences(int[] pushed, int[] popped) {
        if (pushed == null && popped == null) {
            return true;
        }
        if (pushed == null || popped == null) {
            return false;
        }
        if (pushed.length != pushed.length) {
            return false;
        }

        Set<Integer> visited = new HashSet<>();
        Stack<Integer> stack = new Stack<>();
        int j = 0;

        for (int i = 0; i < popped.length; i++) {
            int poppedNum = popped[i];

            while (j < pushed.length && !visited.contains(poppedNum)) {
                stack.add(pushed[j]);
                visited.add(pushed[j]);
                j++;
            }

            int actual = stack.pop();
            if (actual != poppedNum) {
                return false;
            }
        }

        return true;
    }
}
```

## Solution 2

Stack

```java
/**
 * Question   : 946. Validate Stack Sequences
 * Complexity : Time: O(n) ; Space: O(n)
 * Topics     : Stack
 */
class Solution {
    public boolean validateStackSequences(int[] pushed, int[] popped) {
        if (pushed == null && popped == null) {
            return true;
        }
        if (pushed == null || popped == null) {
            return false;
        }
        if (pushed.length != pushed.length) {
            return false;
        }

        Stack<Integer> stack = new Stack<>();
        int j = 0;

        for (int i = 0; i < pushed.length; i++) {
            stack.push(pushed[i]);
            while (!stack.isEmpty() && stack.peek() == popped[j]) {
                stack.pop();
                j++;
            }
        }

        return stack.isEmpty();
    }
}
```
