# Copy List with Random Pointer

## Solution 1: Brute Force

```java
// TC: O(n)
// SC: O(n)
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

## Solution 2: Optimized

```java
// TC: O(n)
// SC: O(1)
class Solution {
    public Node copyRandomList(Node head) {
        if (head == null) {
            return null;
        }

        // 1. Copy nodes.
        Node curr = head;
        while (curr != null) {
            Node next = curr.next;
            Node copy = new Node(curr.val);

            curr.next = copy;
            copy.next = next;

            curr = next;
        }

        // 2. Handle random pointers.
        curr = head;
        while (curr != null) {
            Node copy = curr.next;
            Node random = curr.random;

            if (random != null) {
                copy.random = random.next;
            }

            curr = copy.next;
        }

        // 3. Seperate copied nodes.
        Node dummy = new Node(0);
        Node p1 = dummy;

        curr = head;
        while (curr != null) {
            Node copy = curr.next;
            curr.next = copy.next;
            p1.next = copy;

            p1 = p1.next;
            curr = curr.next;
        }

        return dummy.next;
    }
}
```
