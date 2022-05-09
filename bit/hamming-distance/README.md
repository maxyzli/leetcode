# Hamming Distance

## Solution 1

```java
/**
 * Question   : 461. Hamming Distance
 * Complexity : Time: O(1) ; Space: O(1)
 * Topics     : Bit
 */
class Solution {
    public int hammingDistance(int x, int y) {
        int res = 0;
        while (x != 0 || y != 0) {
            if ((x & 1) != (y & 1)) {
                res++;
            }
            x >>>= 1;
            y >>>= 1;
        }
        return res;
    }
}
```

## Solution 2

```java
/**
 * Question   : 461. Hamming Distance
 * Complexity : Time: O(1) ; Space: O(1)
 * Topics     : Bit
 */
class Solution {
    public int hammingDistance(int x, int y) {
        int res = 0;
        int diff = x ^ y;

        while (diff != 0) {
            res++;
            diff = diff & (diff - 1);
        }

        return res;
    }
}
```
