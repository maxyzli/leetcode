# Power of Two

## Solution 1

```java
/**
 * Question   : 231. Power of Two
 * Complexity : Time: O(log(n)) ; Space: O(1)
 * Topics     : Bit
 */
class Solution {
    public boolean isPowerOfTwo(int n) {
        if (n == 0) {
            return false;
        }
        if (n == 1) {
            return true;
        }
        if (n % 2 != 0) {
            return false;
        }
        return isPowerOfTwo(n / 2);
    }
}
```

## Solution 2

```java
/**
 * Question   : Power of Two
 * Complexity : Time: O(1) ; Space: O(1)
 * Topics     : Bit
 */
class Solution {
    public boolean isPowerOfTwo(int n) {
        if (n < 0) {
            return false;
        }

        int count = 0;

        while (n != 0) {
            count++;
            n = n & (n - 1);
        }

        return count == 1;
    }
}
```
