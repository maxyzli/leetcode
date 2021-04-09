# Largest Number

## Solution 1

This problem can be solved by sorting strings, not sorting integer. Define a comparator to compare strings by concat() right-to-left or left-to-right.

```java
/**
 * Question   : 179. Largest Number
 * Topics     : array
 * Complexity : Time: O(nlogn) ; Space: O(n)
 */
class Solution {
    public String largestNumber(int[] nums) {
        if (nums == null || nums.length == 0) {
            return "";
        }

        // 1. Convert numbers to strings.
        String[] strs = new String[nums.length];
        for (int i = 0; i < strs.length; i++) {
            strs[i] = String.valueOf(nums[i]);
        }

        // 2. Sort by concat.
        Arrays.sort(strs, (a, b) -> {
            String ab = a + b;
            String ba = b + a;
            // If ba > ab, swap a and b: b, a
            // If ba < ab, do nothing  : a, b
            return ba.compareTo(ab);
        });

        // Handle all 0.
        if (strs[0].equals("0")) {
            return "0";
        }

        // 3. Generate result.
        StringBuffer sb = new StringBuffer();
        for (int i = 0; i < strs.length; i++) {
            sb.append(strs[i]);
        }

        return sb.toString();
    }
}
```
