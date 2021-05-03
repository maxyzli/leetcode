# Merge Sorted Array

## Solution 1

```java
/**
 * Question   : 88. Merge Sorted Array
 * Complexity : Time: O(n) ; Space: O(1)
 * Topics     : Array
 */
class Solution {
    public void merge(int[] nums1, int m, int[] nums2, int n) {
        if (nums1 == null || nums2 == null) {
            return;
        }

        int p1 = m - 1;
        int p2 = n - 1;
        int positionToInsert = m + n - 1;

        while (p1 >= 0 && p2 >= 0) {
            if (nums1[p1] > nums2[p2]) {
                nums1[positionToInsert--] = nums1[p1--];
            } else {
                nums1[positionToInsert--] = nums2[p2--];
            }
        }

        while (p1 >= 0) {
            nums1[positionToInsert--] = nums1[p1--];
        }

        while (p2 >= 0) {
            nums1[positionToInsert--] = nums2[p2--];
        }
    }
}
```
