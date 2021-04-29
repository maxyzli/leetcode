# Candy

## Solution 1

Naive Approach (Time Limit Exceeded)

```jsx
/**
 * Question   : Temple Offerings
 * Complexity : Time: O(n^2) ; Space: O(1)
 * Topics     : Array
 */
public class Solution {
    public int candy(int[] ratings) {
        if (ratings == null || ratings.length == 0) {
            return 0;
        }

        int n = ratings.length;
        int count = 0;

        for (int i = 0; i < n; i++) {
            int left = 1;
            for (int j = 1; j <= i; j++) {
                if (ratings[j - 1] < ratings[j]) {
                    left++;
                } else {
                    left = 1;
                }
            }

            int right = 1;
            for (int j = n - 2; j >= i; j--) {
                if (ratings[j] > ratings[j + 1]) {
                    right++;
                } else {
                    right = 1;
                }
            }

            count += Math.max(left, right);
        }

        return count;
    }
}
```

## Solution 2

Greedy

```java
/**
 * Question   : 135. Candy
 * Complexity : Time: O(n) ; Space: O(n)
 * Topics     : Array
 */
class Solution {
    public int candy(int[] ratings) {
        if (ratings == null || ratings.length == 0) {
            return 0;
        }

        int n = ratings.length;

        int[] left = new int[n];
        left[0] = 1;

        for (int i = 1; i < ratings.length; i++) {
            if (ratings[i - 1] < ratings[i]) {
                left[i] = left[i - 1] + 1;
            } else {
                left[i] = 1;
            }
        }

        int[] right = new int[n];
        right[n - 1] = 1;

        for (int i = n - 2; i >= 0; i--) {
            if (ratings[i] > ratings[i + 1]) {
                right[i] = right[i + 1] + 1;
            } else {
                right[i] = 1;
            }
        }

        int sum = 0;
        for (int i = 0; i < n; i++) {
           sum += Math.max(left[i], right[i]); 
        }
        
        return sum;
    }
}
```
