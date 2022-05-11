# Maximum Product Subarray

## Solution 1: DP

## Solution 2: DP with space compression

```java
// TC: O(n)
// SC: O(1)
class Solution {
    public int maxProduct(int[] nums) {
        int res = nums[0];
        int max = nums[0];
        int min = nums[0];

        for (int i = 1; i < nums.length; i++) {
            int num = nums[i];
            int currMax = max;
            int currMin = min;

            max = Math.max(
                num,
                Math.max(currMin * num, currMax * num)
            );

            min = Math.min(
                num,
                Math.min(currMin * num, currMax * num)
            );

            res = Math.max(res, max);
        }


        return res;
    }
}
```

