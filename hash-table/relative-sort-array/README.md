# Relative Sort Array

## Solution 1

```java
/**
 * Question   : 1122. Relative Sort Array
 * Complexity : Time: O(nlogn) ; Space: O(n)
 * Topics     : Hash Table
 */
class Solution {
    public int[] relativeSortArray(int[] arr1, int[] arr2) {
        Map<Integer, Integer> map = new HashMap<>();
        for (int i = 0; i < arr2.length; i++) {
            map.put(arr2[i], i);
        }

        List<Integer> list = new ArrayList<>();
        for (int i = 0; i < arr1.length; i++) {
            list.add(arr1[i]);
        }

        Collections.sort(list, (a, b) -> {
            if (map.containsKey(a) && map.containsKey(b)) {
                return map.get(a) - map.get(b);
            } else if (map.containsKey(a)) {
                return -1;
            } else if (map.containsKey(b)) {
                return 1;
            } else {
                return a - b;
            }
        });

        for (int i = 0; i < list.size(); i++) {
            arr1[i] = list.get(i);
        }

        return arr1;
    }
}
```

## Solution 2

Counting Sort

```java
/**
 * Question   : 1122. Relative Sort Array
 * Complexity : Time: O(n+m) ; Space: O(n)
 * Topics     : Hash Table
 */
class Solution {
    public int[] relativeSortArray(int[] arr1, int[] arr2) {
        int[] count = new int[1001];

        for (int i = 0; i < arr1.length; i++) {
            count[arr1[i]]++;
        }

        int index = 0;
        for (int num : arr2) {
            while (count[num] != 0) {
                arr1[index++] = num;
                count[num]--;
            }
        }

        for (int i = 0; i < count.length; i++) {
            while (count[i] != 0) {
                arr1[index++] = i;
                count[i]--;
            }
        }

        return arr1;
    }
}
```
