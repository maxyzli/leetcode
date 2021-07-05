# LRU Cache

## Solution 1

Hash Map + Double Linked List

```java
class LRUCache {
    int capacity;
    Map<Integer, Node> key2Node;
    DoubleLinkedList ll;

    public LRUCache(int capacity) {
        this.capacity = capacity;
        this.key2Node = new HashMap<>();
        this.ll = new DoubleLinkedList();
    }

    public int get(int key) {
        if (!key2Node.containsKey(key)) {
            return -1;
        }
        Node node = key2Node.get(key);

        // Remember to remove the node first.
        // To maintain the head and tail.
        ll.remove(node);
        ll.addToHead(node);

        return node.val;
    }

    public void put(int key, int value) {
        if (key2Node.containsKey(key)) {
            Node node = key2Node.get(key);
            ll.remove(node);
            key2Node.remove(key);
        }

        if (key2Node.size() == capacity) {
            Node tail = ll.tail;
            key2Node.remove(tail.key);
            ll.remove(tail);
        }

        Node node = new Node(key, value);
        key2Node.put(key, node);
        ll.addToHead(node);
    }
}

class Node {
    int key;
    int val;
    Node prev;
    Node next;
    public Node(int key, int val) {
        this.key = key;
        this.val = val;
    }
}

class DoubleLinkedList {
    Node head;
    Node tail;

    public void addToHead(Node node) {
        if (head == null) {
            head = tail = node;
            return;
        }
        node.next = head;
        head.prev = node;
        head = node;
    }

    public void remove(Node node) {
        Node prev = node.prev;
        Node next = node.next;
        node.prev = null;
        node.next = null;

        if (prev == null) {
            head = next;
        } else {
            prev.next = next;
        }

        if (next == null) {
            tail = prev;
        } else {
            next.prev = prev;
        }
    }
}
```
