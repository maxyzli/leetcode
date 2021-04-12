# Two Sum IV - Input is a BST

## Solution 1

Traverse Tree

```java
/**
 * Question   : 653. Two Sum IV - Input is a BST
 * Complexity : Time: O(nlog(n)) ; Space: O(log(n))
 * Topics     : tree
 */
class Solution {
    TreeNode root;

    public boolean findTarget(TreeNode root, int k) {
        this.root = root;
        return traverse(root, k);
    }

    private boolean traverse(TreeNode node, int k) {
        if (node == null) {
            return false;
        }

        if (findSecondValue(this.root, node, k - node.val)) {
            return true;
        };

        return traverse(node.left, k) || traverse(node.right, k);
    }

    private boolean findSecondValue(TreeNode node, TreeNode first, int target) {
        if (node == null) {
            return false;
        }
        if (node.val == target) {
            if (node == first) {
                return false;
            }
            return true;
        } else if (node.val > target) {
            return findSecondValue(node.left, first, target);
        } else {
            return findSecondValue(node.right, first, target);
        }
    }
}
```

## Solution 2

Store number in a list

```java
/**
 * Question   : 653. Two Sum IV - Input is a BST
 * Complexity : Time: O(n) ; Space: O(log(n))
 * Topics     : tree
 */
class Solution {
    public boolean findTarget(TreeNode root, int k) {
        List<Integer> list = new ArrayList<>();
        traverse(root, list);

        int low = 0;
        int high = list.size() - 1;

        while (low < high) {
            int num1 = list.get(low);
            int num2 = list.get(high);

            if (num1 + num2 == k) {
                return true;
            } else if (num1 + num2 > k) {
                high--;
            } else {
                low++;
            }
        }

        return false;
    }

    private void traverse(TreeNode root, List<Integer> list) {
        if (root == null) {
            return;
        }
        traverse(root.left, list);
        list.add(root.val);
        traverse(root.right, list);
    }
}
```

## Solution 3

Set

```java
/**
 * Question   : 653. Two Sum IV - Input is a BST
 * Complexity : Time: O(n) ; Space: O(n)
 * Topics     : tree
 */
class Solution {
    public boolean findTarget(TreeNode root, int k) {
        Set<Integer> set = new HashSet<>();
        return find(root, k, set);
    }

    private boolean find(TreeNode root, int k, Set<Integer> set) {
        if (root == null) {
            return false;
        }

        if (set.contains(k - root.val)) {
            return true;
        }
        set.add(root.val);

        return find(root.left, k, set) || find(root.right, k, set);
    }
}
```
