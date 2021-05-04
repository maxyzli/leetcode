# Intersection of Two Arrays II

## Solution 1

Map

```jsx
/**
 * Question   : 350. Intersection of Two Arrays II
 * Complexity : Time: O(n) ; Space: O(n)
 * Topics     : array
 */
class Solution {
    public int[] intersect(int[] nums1, int[] nums2) {
        Map<Integer, Integer> map = new HashMap<>();

        for (int num : nums2) {
            map.putIfAbsent(num, 0);
            map.put(num, map.get(num) + 1);
        }

        List<Integer> list = new LinkedList<>();
        for (int num : nums1) {
            if (map.containsKey(num) && map.get(num) > 0) {
                list.add(num);
                map.put(num, map.get(num) - 1);
            }
        }

        int[] res = new int[list.size()];
        int idx = 0;
        while (!list.isEmpty()) {
            res[idx++] = list.get(0);
            list.remove(0);
        }

        return res;
    }
}
```

## Solution 2

Two Pointers

```jsx
/**
 * Question   : 350. Intersection of Two Arrays II
 * Complexity : Time: O(n) ; Space: O(n)
 * Topics     : array
 */
class Solution {
    public int[] intersect(int[] nums1, int[] nums2) {
        Arrays.sort(nums1);
        Arrays.sort(nums2);

        List<Integer> list = new LinkedList<>();

        int p1 = 0;
        int p2 = 0;
        while (p1 < nums1.length && p2 < nums2.length) {
            if (nums1[p1] == nums2[p2]) {
                list.add(nums1[p1]);
                p1++;
                p2++;
            } else if (nums1[p1] > nums2[p2]) {
                p2++;
            } else {
                p1++;
            }
        }

        int[] res = new int[list.size()];
        int idx = 0;
        while (!list.isEmpty()) {
            res[idx++] = list.get(0);
            list.remove(0);
        }

        return res;
    }
}
```
