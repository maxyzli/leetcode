# Implement Trie (Prefix Tree)

## Solution 1

```java
class Trie {
    private class Node {
       int val;
       Node[] children;
       boolean isWord;

       public Node(int val) {
           this.val = val;
           this.children = new Node[26];
       }
    }

    private Node root;

    public Trie() {
        root = new Node(':');
    }

    public void insert(String word) {
        Node curr = root;
        for (char c : word.toCharArray()) {
            int idx = (c - 'a');

            if (curr.children[idx] == null) {
                curr.children[idx] = new Node(idx);
            }

            curr = curr.children[idx];
        }
        curr.isWord = true;
    }

    public boolean search(String word) {
        Node curr = root;
        for (char c : word.toCharArray()) {
            int idx = (c - 'a');

            if (curr.children[idx] == null) {
                return false;
            }

            curr = curr.children[idx];
        }
        return curr.isWord == true;
    }

    public boolean startsWith(String prefix) {
        Node curr = root;
        for (char c : prefix.toCharArray()) {
            int idx = (c - 'a');

            if (curr.children[idx] == null) {
                return false;
            }

            curr = curr.children[idx];
        }
        return true;
    }
}
```
