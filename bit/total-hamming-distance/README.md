# Total Hamming Distance

## Solution 1

Time Limit Exceeded

```java
/**
 * Question   : 477. Total Hamming Distance
 * Complexity : Time: O(n^2) ; Space: O(1)
 * Topics     : Bit
 */
class Solution {
    public int totalHammingDistance(int[] nums) {
        int total = 0;

        for (int i = 0; i < nums.length; i++) {
            for (int j = i + 1; j < nums.length; j++) {
                total += hammingDistance(nums[i], nums[j]);
            }
        }

        return total;
    }

    private int hammingDistance(int a, int b) {
        int diff = a ^ b;

        int res = 0;
        while (diff != 0) {
            res++;
            diff = diff & (diff - 1);
        }

        return res;
    }
}
```

## Solution 2

```java
/**
 * Question   : 477. Total Hamming Distance
 * Complexity : Time: O(n) ; Space: O(1)
 * Topics     : Bit
 */
class Solution {
    public int totalHammingDistance(int[] nums) {
        int n = nums.length;

        // count stores the number of 1 in each bit.
        int[] count = new int[32];

        for (int i = 0; i < n; i++) {
            int num = nums[i];
            int j = 0;
            while (num > 0) {
                count[j] += num & 1;
                num >>>= 1;
                j++;
            }
        }

        int res = 0;
        for (int i = 0; i < count.length; i++) {
            // (number of 1) * (number of 0) in this bit.
            res += count[i] * (n - count[i]);
        }

        return res;
    }
}
```
