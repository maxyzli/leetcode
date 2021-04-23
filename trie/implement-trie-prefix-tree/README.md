# Implement Trie (Prefix Tree)

## Solution 1

```java
/**
 * Question   : 208. Implement Trie (Prefix Tree)
 * Topics     : Trie
 */
class Trie {
    Node root;

    public Trie() {
        root = new Node('*');
    }

    // O(len(word))
    public void insert(String word) {
        Node curr = root;

        for (int i = 0; i < word.length(); i++) {
            char c = word.charAt(i);
            int childIndex = word.charAt(i) - 'a';

            if (curr.children[childIndex] == null) {
                Node newNode = new Node(c);
                curr.children[childIndex] = newNode;
            }

            curr = curr.children[childIndex];
        }

        // Mark as a word.
        curr.isWord = true;
    }

    // O(len(word))
    public boolean search(String word) {
        Node curr = root;

        for (int i = 0; i < word.length(); i++) {
            int childIndex = word.charAt(i) - 'a';

            if (curr.children[childIndex] == null) {
                return false;
            }

            curr = curr.children[childIndex];
        }

        return curr.isWord;
    }

    // O(len(prefix))
    public boolean startsWith(String prefix) {
        Node curr = root;

        for (int i = 0; i < prefix.length(); i++) {
            int childIndex = prefix.charAt(i) - 'a';

            if (curr.children[childIndex] == null) {
                return false;
            }

            curr = curr.children[childIndex];
        }

        return true;
    }
}

class Node {
    int value;
    Node[] children;
    boolean isWord;

    public Node(int value) {
        this.value = value;
        this.children = new Node[26];
    }
}
```

## Solution 2

OOP

```java
class Trie {
    private Node root;

    public Trie() {
        this.root = new Node('*');
    }

    public void insert(String word) {
        insert(root, word, 0);
    }

    private void insert(Node root, String word, int i) {
        if (i >= word.length()) {
            return;
        }

        char curr = word.charAt(i);

        if (!root.hasChild(curr)) {
            root.addChild(curr);
        }

        if (i == word.length() - 1) {
            root.getChild(curr).setEnd(true);
        } else {
            insert(root.getChild(curr), word, i + 1);
        }
    }

    public boolean search(String word) {
        return search(root, word, 0);
    }

    private boolean search(Node root, String word, int i) {
        if (i >= word.length()) {
            return false;
        }

        char curr = word.charAt(i);

        if (!root.hasChild(curr)) {
            return false;
        }

        if (i == word.length() - 1) {
            return root.getChild(curr).isEnd();
        } else {
            return search(root.getChild(curr), word, i + 1);
        }
    }

    public boolean startsWith(String prefix) {
        return startWith(root, prefix, 0);
    }

    private boolean startWith(Node root, String prefix, int i) {
        if (i >= prefix.length()) {
            return false;
        }

        char curr = prefix.charAt(i);

        if (!root.hasChild(curr)) {
            return false;
        }

        if (i == prefix.length() - 1) {
            return true;
        } else {
            return startWith(root.getChild(curr), prefix, i + 1);
        }
    }
}

class Node {
    private char value;
    private boolean isEnd;
    private Node[] children;

    public Node(char value) {
        this.value = value;
        children = new Node[26];
    }

    public char getValue() {
        return value;
    }

    public boolean isEnd() {
        return isEnd;
    }

    public void setEnd(boolean end) {
        isEnd = end;
    }

    public boolean hasChild(char c) {
        if (children[c - 'a'] == null)  {
            return false;
        }
        return true;
    }

    public void addChild(char c) {
        children[c - 'a'] = new Node(c);
    }

    public Node getChild(char c) {
        return children[c - 'a'];
    }
}
```
