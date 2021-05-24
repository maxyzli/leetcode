# Trapping Rain Water

## Solution 1

Temporary Array

```java
/**
 * Question   : 42. Trapping Rain Water
 * Complexity : Time: O(n) ; Space: O(n)
 * Topics     : array
 */
class Solution {
    public int trap(int[] height) {
        int n = height.length;

        int[] left = new int[n];
        int[] right = new int[n];

        int leftMax = Integer.MIN_VALUE;
        for (int i = 0; i < height.length; i++) {
            leftMax = Math.max(leftMax, height[i]);
            left[i] = leftMax;
        }

        int rightMax = Integer.MIN_VALUE;
        for (int i = n - 1; i >= 0; i--) {
            rightMax = Math.max(rightMax, height[i]);
            right[i] = rightMax;
        }

        int trap = 0;
        for (int i = 0; i < n; i++) {
            int leftBound = left[i];
            int rightBound = right[i];

            if (height[i] >= leftBound || height[i] >= rightBound) {
                continue;
            }

            trap += Math.min(leftBound, rightBound) - height[i];
        }

        return trap;
    }
}
```

## Solution 2

Two Pointers

```java
/**
 * Question   : 42. Trapping Rain Water
 * Complexity : Time: O(n) ; Space: O(1)
 * Topics     : array
 */
class Solution {
    public int trap(int[] height) {
        int n = height.length;

        int trap = 0;

        int low = 0;
        int high = n - 1;

        int leftMax = Integer.MIN_VALUE;
        int rightMax = Integer.MIN_VALUE;

        while (low < high) {
            if (height[low] < height[high]) {
                if (height[low] >= leftMax) {
                    leftMax = height[low];
                } else {
                    trap += leftMax - height[low];
                }
                low++;
            } else {
                if (height[high] >= rightMax) {
                    rightMax = height[high];
                } else {
                    trap += rightMax - height[high];
                }
                high--;
            }
        }

        return trap;
    }
}
```
