# Design Linked List

# Solution 1

```java
/**
 * Question   : 707. Design Linked List
 * Topics     : Linked List
 */
class MyLinkedList {
    private class Node {
        int val;
        Node next;
        public Node(int data) {
            this.val = data;
        }
    }

    private Node head;
    private Node tail;
    private int size;

    public MyLinkedList() {
        this.head = null;
        this.tail = null;
        this.size = 0;
    }

    public boolean isEmpty() {
        return size == 0;
    }

    /** Get the value of the index-th node in the linked list. If the index is invalid, return -1. */
    public int get(int index) {
        if (index < 0 || index >= size) {
            return -1;
        }

        Node curr = head;
        for (int i = 0; i < index; i++) {
            curr = curr.next;
        }

        return curr.val;
    }

    /** Add a node of value val before the first element of the linked list. After the insertion, the new node will be the first node of the linked list. */
    public void addAtHead(int val) {
        Node newNode = new Node(val);

        if (isEmpty()) {
            head = newNode;
            tail = newNode;
        } else {
            newNode.next = head;
            head = newNode;
        }

        size++;
    }

    public void removeHead() {
        if (isEmpty()) {
            return;
        }

        Node next = head.next;
        head.next = null;
        head = next;

        size--;
    }

    public void removeTail() {
        if (isEmpty()) {
            return;
        }

        Node prev = null;
        Node curr = head;
        for (int i = 0; i < size - 1; i++) {
            prev = curr;
            curr = curr.next;
        }
        prev.next = null;
        this.tail = prev;

        size--;
    }

    /** Append a node of value val to the last element of the linked list. */
    public void addAtTail(int val) {
        Node newNode = new Node(val);

        if (isEmpty()) {
            head = newNode;
            tail = newNode;
        } else {
            tail.next = newNode;
            tail = newNode;
        }

        size++;
    }

    /** Add a node of value val before the index-th node in the linked list. If index equals to the length of linked list, the node will be appended to the end of linked list. If index is greater than the length, the node will not be inserted. */
    public void addAtIndex(int index, int val) {
        if (index < 0 || index > size) {
            return;
        }
        if (index == 0) {
            addAtHead(val);
            return;
        }
        if (index == size) {
            addAtTail(val);
            return;
        }

        Node prev = null;
        Node curr = head;
        for (int i = 0; i < index; i++) {
            prev = curr;
            curr = curr.next;
        }

        Node newNode = new Node(val);
        prev.next = newNode;
        newNode.next = curr;

        size++;
    }

    /** Delete the index-th node in the linked list, if the index is valid. */
    public void deleteAtIndex(int index) {
        if (isEmpty() || index < 0 || index >= size) {
            return;
        }
        if (index == 0) {
            removeHead();
            return;
        }
        if (index == size - 1) {
            removeTail();
            return;
        }

        Node prev = null;
        Node curr = head;
        for (int i = 0; i < index; i++) {
            prev = curr;
            curr = curr.next;
        }
        prev.next = prev.next.next;
        curr.next = null;

        size--;
    }
}
```
