# Copy List with Random Pointer

## Solution 1

Brute Force

```java
/**
 * Question   : 138. Copy List with Random Pointer
 * Complexity : Time: O(n) ; Space: O(n)
 * Topics     : Linked List
 */
class Solution {
    public Node copyRandomList(Node head) {
        Map<Node, Node> map = new HashMap<>();

        Node curr = head;
        while (curr != null) {
            map.put(curr, new Node(curr.val));
            curr = curr.next;
        }

        curr = head;
        while (curr != null) {
            if (curr.next != null) {
                map.get(curr).next = map.get(curr.next);
            }
            curr = curr.next;
        }

        curr = head;
        while (curr != null) {
            if (curr.random != null) {
                map.get(curr).random = map.get(curr.random);
            }
            curr = curr.next;
        }

        return map.get(head);
    }
}
```

## Solution 2

Optimized

```java
/**
 * Question   : 138. Copy List with Random Pointer
 * Complexity : Time: O(n) ; Space: O(1)
 * Topics     : Linked List
 */
class Solution {
    public Node copyRandomList(Node head) {
        if (head == null) {
            return null;
        }

        // make copy of each node, and link them together side-by-side in a single list.
        Node iter = head;
        while (iter != null) {
            Node next = iter.next;
            Node copy = new Node(iter.val);
            iter.next = copy;
            copy.next = next;
            iter = next;
        }

        // assign random pointers for the copy nodes.
        iter = head;
        while (iter != null) {
            if (iter.next != null && iter.random != null) {
                iter.next.random = iter.random.next;
            }
            iter = iter.next.next;
        }

        // restore the original list, and extract the copy list.
        Node p = new Node(0);
        Node temp = p;
        iter = head;
        while (iter != null) {
            temp.next = iter.next;
            temp = temp.next;
            // restore the original list.
            iter.next = iter.next.next;
            iter = iter.next;
        }

        return p.next;
    }
}
```
