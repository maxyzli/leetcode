# Serialize and Deserialize Binary Tree

## Solution 1

```java
/**
 * Question   : 297. Serialize and Deserialize Binary Tree
 * Topics     : Tree
 * Complexity : Time: O(n) ; Space: O(log(n))
 */
public class Codec {
    final String END = "#";
    final String SEP = ",";

    public String serialize(TreeNode root) {
        StringBuilder sb = new StringBuilder();
        serializeUtil(root, sb);
        return sb.toString();
    }

    private void serializeUtil(TreeNode root, StringBuilder sb) {
        if (root == null) {
            sb.append(END + SEP);
            return;
        }
        sb.append(root.val + SEP);
        serializeUtil(root.left, sb);
        serializeUtil(root.right, sb);
    }

    public TreeNode deserialize(String data) {
        String[] arr = data.split(SEP);
        int[] index = new int[1];
        return deserializeUtil(arr, index);
    }

    private TreeNode deserializeUtil(String[] arr, int[] index) {
        if (index[0] >= arr.length) {
            return null;
        }

        String str = arr[index[0]];
        index[0]++;

        if (str.equals(END)) {
            return null;
        }

        TreeNode root = new TreeNode(Integer.valueOf(str));
        root.left = deserializeUtil(arr, index);
        root.right = deserializeUtil(arr, index);

        return root;
    }
}
```
