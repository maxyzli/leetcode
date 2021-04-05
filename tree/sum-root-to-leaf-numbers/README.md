# Sum Root to Leaf Numbers

## Solution 1

```java
/**
 * Question   : 129. Sum Root to Leaf Numbers
 * Topics     : Tree
 * Complexity : Time: O(n) ; Space: O(log(n))
 */
class Solution {
    int acc = 0;

    public int sumNumbers(TreeNode root) {
        acc = 0;
        sumNumbersUtil(root, 0);
        return acc;
    }

    private void sumNumbersUtil(TreeNode root, int pathSum) {
        if (root == null) {
            return;
        }

        int temp = pathSum * 10 + root.val;
        if (root.left == null && root.right == null) {
            acc += temp;
        }

        sumNumbersUtil(root.left, temp);
        sumNumbersUtil(root.right, temp);
    }
}
```
