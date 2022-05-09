# Reverse Bits

## Solution 1

```java
/**
 * Question   : Reverse Bits
 * Complexity : Time: O(1) ; Space: O(1)
 * Topics     : Bit
 */
public class Solution {
    public int reverseBits(int n) {
        int output = 0;

        for (int i = 0; i < 32; i++) {
          output <<= 1;

          if ((input & 1) != 0) {
            output |= 1;
          }

          input >>= 1;
        }

        return output;
    }
}
```
