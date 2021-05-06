# Reverse Integer

## Solution 1

```java
/**
 * Question   : 7. Reverse Integer
 * Complexity : Time: O(n) ; Space: O(1)
 * Topics     : Math
 */
class Solution {
    public int reverse(int x) {
        int sign = 1;

        if (x < 0) {
            sign = -1;
            x = -x;
        }

        int num = 0;
        while (x > 0) {
            // 1. If num > Integer.MAX_VALUE / 10 then num * 10 > Integer.MAX_VALUE
            if (num > Integer.MAX_VALUE / 10) {
                return 0;
            }
            // 2. num == Integer.MAX_VALUE / 10 && sign > 0 && x % 10 > 7
            //    then num * 10 + x % 10 > Integer.MAX_VALUE
            if (num == Integer.MAX_VALUE / 10 && sign > 0 && x % 10 > 7) {
                return 0;
            }
            // 3. num == Integer.MAX_VALUE / 10 && sign < 0 && x % 10 > 8
            //    then -(num * 10 + x % 10) < Integer.MIN_VALUE
            if (num == Integer.MAX_VALUE / 10 && sign < 0 && x % 10 > 8) {
                return 0;
            }
            num = num * 10 + x % 10;
            x /= 10;
        }

        return sign * num;
    }
}
```
