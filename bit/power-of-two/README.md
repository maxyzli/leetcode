# Power of Two

## Solution 1

Binary representation of a power of two contains exactly one bit turned on.

```java
/**
 * Question   : 231. Power of Two
 * Complexity : Time: O(1) ; Space: O(1)
 * Topics     : Bit
 */
class Solution {
    public boolean isPowerOfTwo(int n) {
			if (input <= 0) {
        return false;
      }
      // Turn off the rightmost set bit
      return (input & (input - 1)) == 0;
    }
}
```
