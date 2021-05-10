# Third Maximum Number

## Solution 1

```java
/**
 * Question   : Find Three Largest Number
 * Complexity : Time: O(n) ; Space: O(1)
 */
public class Solution {
    public int thirdMax(int[] array) {
        PriorityQueue<Integer> pq = new PriorityQueue<>();

        for (int i = 0; i < array.length; i++) {
            int curr = array[i];

            if (pq.size() < 3 && !pq.contains(curr)) {
                pq.add(curr);
                continue;
            }

            if (!pq.contains(curr) && curr > pq.peek()) {
                pq.remove();
                pq.add(curr);
            }
        }

        if (pq.size() < 3) {
            while (pq.size() != 1) pq.remove();
        }

        return pq.remove();
    }
}
```

## Solution 2

```java
/**
 * Question   : 414. Third Maximum Number
 * Complexity : Time: O(n) ; Space: O(1)
 * Topics     : Array
 */
class Solution {
    public int thirdMax(int[] nums) {
        Integer first = null;
        Integer second = null;
        Integer third = null;

        for (int i = 0; i < nums.length; i++) {
            int num = nums[i];

            if ((first == null) || (num > first)) {
                third = second;
                second = first;
                first = num;
            } else if (num != first && (second == null || num > second)) {
                third = second;
                second = num;
            } else if ((num != first && num != second) && (third == null || num > third)) {
                third = num;
            }
        }

        if (third != null) {
            return third;
        }
        return first;
    }
}
```
