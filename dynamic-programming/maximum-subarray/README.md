# Maximum Subarray

## Solution 1: DP

```java
// TC: O(n)
// SC: O(1)
class Solution {
    public int maxSubArray(int[] nums) {
        int max = nums[0];
        int acc = nums[0];

        for (int i = 1; i < nums.length; i++) {
            acc = Math.max(acc + nums[i], nums[i]);
            max = Math.max(max, acc);
        }

        return max;
    }
}
```
