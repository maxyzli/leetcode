# Number of 1 Bits

# Solution 1

```java
/**
 * Question   : 191. Number of 1 Bits
 * Complexity : Time: O(1) ; Space: O(1)
 * Topics     : Bit
 */
public class Solution {
    public int hammingWeight(int n) {
        int count = 0;
        for (int i = 0; i < 32; i++) {
            count += n & 1;
            n >>>= 1;
        }
        return count;
    }
}
```

# Solution 2

```java
/**
 * Question   : 191. Number of 1 Bits
 * Complexity : Time: O(1) ; Space: O(1)
 * Topics     : Bit
 */
public class Solution {
    public int hammingWeight(int n) {
        int count = 0;
        for (int i = 0; i < 32; i++) {
            if ((n & (1 << i)) != 0) {
                count++;
            }
        }
        return count;
    }
}
```

# Solution 3

```java
/**
 * Question   : 191. Number of 1 Bits
 * Complexity : Time: O(1) ; Space: O(1)
 * Topics     : Bit
 */
public class Solution {
    public int hammingWeight(int n) {
        int count = 0;
        while (n != 0) {
            count++;
            n = n & (n - 1);
        }
        return count;
    }
}
```
