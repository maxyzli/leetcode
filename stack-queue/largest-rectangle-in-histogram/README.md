# Largest Rectangle in Histogram

## Solution 1

Brute Force (Enum Width)

```java
/**
 * Question   : 84. Largest Rectangle in Histogram
 * Complexity : Time: O(n^2) ; Space: O(1)
 * Topics     : Stack/Queue
 */
class Solution {
    public int largestRectangleArea(int[] heights) {
        if (heights == null || heights.length == 0) {
            return 0;
        }

        int n = heights.length;
        int ans = Integer.MIN_VALUE;

        for (int low = 0; low < n; low++) {
            int minHeight = heights[low];
            for (int high = low; high < n; high++) {
                minHeight = Math.min(minHeight, heights[high]);
                int currWidth = high - low + 1;
                ans = Math.max(ans, currWidth * minHeight);
            }
        }

        return ans;
    }
}
```


## Solution 2

Brute Force (Enum Height)

```java
/**
 * Question   : 84. Largest Rectangle in Histogram
 * Complexity : Time: O(n^2) ; Space: O(1)
 * Topics     : Stack/Queue
 */
public class Solution {
    public int largestRectangleArea(int[] heights) {
        if (heights == null || heights.length == 0) {
            return 0;
        }

        int n = heights.length;
        int largest = 0;

        for (int i = 0; i < n; i++) {
            int currHeight = heights[i];
            int left = i, right = i;

            // Find first height from the left which is smaller than curr height.
            while (left >= 0 && heights[left] >= currHeight) {
                left--;
            }
            // Find first height from the right which is smaller than curr height.
            while (right < n && heights[right] >= currHeight) {
                right++;
            }

            largest = Math.max(largest, currHeight * (right - left - 1));
        }

        return largest;
    }
}
```


## Solution 3

Stack

```java
/**
 * Question   : 84. Largest Rectangle in Histogram
 * Complexity : Time: O(n) ; Space: O(n)
 * Topics     : Stack/Queue
 */
public class Solution {
    public int largestRectangleArea(int[] heights) {
        if (heights == null || heights.length == 0) {
            return 0;
        }

        int n = heights.length;

        Stack<Integer> stack = new Stack<>();

        int[] leftSmallerIdx = new int[n];
        int[] rightSmallerIdx = new int[n];

        for (int i = 0; i < n; i++) {
            while (!stack.isEmpty() && heights[stack.peek()] >= heights[i]) {
                stack.pop();
            }
            leftSmallerIdx[i] = stack.isEmpty() ? -1 : stack.peek();
            stack.push(i);
        }

        stack.clear();

        for (int i = n - 1; i >= 0; i--) {
            while (!stack.isEmpty() && heights[stack.peek()] >= heights[i]) {
                stack.pop();
            }
            rightSmallerIdx[i] = stack.isEmpty() ? n : stack.peek();
            stack.push(i);
        }

        int largestArea = 0;
        for (int i = 0; i < n; i++) {
            int height = heights[i];
            int width = rightSmallerIdx[i] - leftSmallerIdx[i] - 1;
            largestArea = Math.max(largestArea, height * width);
        }

        return largestArea;
    }
}
```
