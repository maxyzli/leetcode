# Permutations

## Solution 1

```java
/**
 * Question   : 46. Permutations
 * Complexity : Time: O(n!) ; Space: O(n)
 * Topics     : Backtracking
 */
class Solution {
    public List<List<Integer>> permute(int[] array) {
        // Corner cases.
        if (array == null || array.length == 0) {
            return new LinkedList<>();
        }

        List<Integer> path = new ArrayList<>();
        List<List<Integer>> list = new ArrayList<>();

        permute(array, path, list);

        return list;
    }

    private void permute(int[] array, List<Integer> path, List<List<Integer>> list) {
        if (path.size() == array.length) {
            list.add(new LinkedList<>(path));
            return;
        }

        for (int i = 0; i < array.length; i++) {
            if (!path.contains(array[i])) {
                path.add(array[i]);
                permute(array, path, list);
                // Backtracking
                path.remove(path.size() - 1);
            }
        }
    }
}
```

## Solution 2

Swap each element with each element after it.

```java
/**
 * Question   : 46. Permutations
 * Complexity : Time: O(n!) ; Space: O(n)
 * Topics     : Backtracking
 */
class Solution {
    public List<List<Integer>> permute(int[] array) {
        // Corner cases.
        if (array == null || array.length == 0) {
            return new LinkedList<>();
        }

        List<List<Integer>> list = new ArrayList<>();
        int start = 0;

        permute(array, start, list);

        return list;
    }

    private void permute(int[] array, int start, List<List<Integer>> list) {
        if (start == array.length) {
            list.add(makeList(array));
            return;
        }

        for (int i = start; i < array.length; i++) {
            swap(array, start, i);
            permute(array, start + 1, list);
            // Backtracking
            swap(array, start, i);
        }
    }

    private void swap(int[] array, int i, int j) {
        int temp = array[i];
        array[i] = array[j];
        array[j] = temp;
    }

    private List<Integer> makeList(int[] array){
        List<Integer> current = new ArrayList<>();
        for (int num: array) {
            current.add(num);
        }
        return current;
    }
}
```
