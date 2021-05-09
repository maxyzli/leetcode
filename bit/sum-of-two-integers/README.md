# Sum of Two Integers

## Solution 1

```java
/**
 * Question   : 371. Sum of Two Integers
 * Complexity : Time: O(1) ; Space: O(1)
 * Topics     : Bit
 */
class Solution {
    public int getSum(int a, int b) {
        while (b != 0) {
            int carry = (a & b) << 1;
            a = a ^ b;
            b = carry;
        }

        // Round1:
        // a: 0111
        // b: 0110
        //  (a & b) << 1 = 0110 << 1 = 1100 (carry part)
        //  (a ^ b)                  = 0001 (add without carry)
        // Round2:
        // a: 0001
        // b: 1100
        //  (a & b) << 1 = 0000 << 1 = 0000 (carry part)
        //  (a ^ b)                  = 1101 (add without carry)

        return a;
    }
}
```
