# Intersection of Two Arrays

## Solution 1

Liner Search

```java
/**
 * Question   : 349. Intersection of Two Arrays
 * Complexity : Time: O(n^2) ; Space: O(n)
 * Topics     : array
 */
class Solution {
    public int[] intersection(int[] nums1, int[] nums2) {
        Set<Integer> intersection = new HashSet<>();

        for (int i = 0; i < nums1.length; i++) {
            for (int j = 0; j < nums2.length; j++) {
                if (nums1[i] == nums2[j]) {
                    intersection.add(nums1[i]);
                }
            }
        }

        int[] res = new int[intersection.size()];
        int idx = 0;
        for (int num : intersection) {
            res[idx++] = num;
        }

        return res;
    }
}
```

## Solution 2

Hash Sets

```java
/**
 * Question   : 349. Intersection of Two Arrays
 * Complexity : Time: O(n) ; Space: O(n)
 * Topics     : array
 */
class Solution {
    public int[] intersection(int[] nums1, int[] nums2) {
        Set<Integer> set = new HashSet<>();

        for (int i = 0; i < nums1.length; i++) {
            set.add(nums1[i]);
        }

        Set<Integer> intersection = new HashSet<>();

        for (int i = 0; i < nums2.length; i++) {
            if (set.contains(nums2[i])) {
                intersection.add(nums2[i]);
            }
        }

        int[] res = new int[intersection.size()];
        int idx = 0;
        for (int num : intersection) {
            res[idx++] = num;
        }

        return res;
    }
}
```

## Solution 3

Two Pointers

```java
/**
 * Question   : 349. Intersection of Two Arrays
 * Complexity : Time: O(n) ; Space: O(n)
 * Topics     : array
 */
class Solution {
    public int[] intersection(int[] nums1, int[] nums2) {
        Set<Integer> set = new HashSet<>();

        for (int i = 0; i < nums1.length; i++) {
            set.add(nums1[i]);
        }

        Set<Integer> intersection = new HashSet<>();

        for (int i = 0; i < nums2.length; i++) {
            if (set.contains(nums2[i])) {
                intersection.add(nums2[i]);
            }
        }

        int[] res = new int[intersection.size()];
        int idx = 0;
        for (int num : intersection) {
            res[idx++] = num;
        }

        return res;
    }
}
```
