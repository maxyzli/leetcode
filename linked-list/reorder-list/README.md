# Reorder List

## Solution 1

Sentinel node

```jsx

/**
 * Question   : 143. Reorder List
 * Complexity : Time: O(n) ; Space: O(n)
 * Topics     : Linked List
 * Date       : 2021/03/25
 */
class Solution {
    public void reorderList(ListNode head) {
        if (head == null || head.next == null) {
            return;
        }

        // 1. Find 2 parts.
        ListNode prev = null;
        ListNode slow = head;
        ListNode fast = head;
        while (fast != null && fast.next != null) {
            prev = slow;
            slow = slow.next;
            fast = fast.next.next;
        }
        prev.next = null;
        ListNode l2 = slow;

        // 2. Reverse l2.
        l2 = reverse(l2);

        // 3. Reorder
        ListNode dummy = new ListNode(0);
        ListNode p = dummy;
        ListNode p1 = head;
        ListNode p2 = l2;

        while (p1 != null || p2 != null) {
            if (p1 != null) {
                p.next = p1;
                p = p.next;
                p1 = p1.next;
            }
            if (p2 != null) {
                p.next = p2;
                p = p.next;
                p2 = p2.next;
            }
        }

        dummy.next = null;
    }

    private ListNode reverse(ListNode node) {
        if (node == null || node.next == null) {
            return node;
        }
        ListNode root = reverse(node.next);
        node.next.next = node;
        node.next = null;
        return root;
    }
}
```

## Solution 2

Queue

```java
class Solution {
    public void reorderList(ListNode head) {
        if (head == null || head.next == null) {
            return;
        }

        ListNode prev = null, slow = head, fast = head;

        while (fast != null && fast.next != null) {
            prev = slow;
            slow = slow.next;
            fast = fast.next.next;
        }

        prev.next = null;
        ListNode reverseHead = reverse(slow);

        Queue<ListNode> queue = new LinkedList<>();

        ListNode l1 = head, l2 = reverseHead;
        while (l1 != null || l2 != null) {
            if (l1 != null) {
                queue.add(l1);
                l1 = l1.next;
            }
            if (l2 != null) {
                queue.add(l2);
                l2 = l2.next;
            }
        }

        ListNode curr = queue.remove();
        while (!queue.isEmpty()) {
            curr.next = queue.remove();
            curr = curr.next;
        }
    }

    private ListNode reverse(ListNode node) {
        if (node.next == null) return node;
        ListNode newHead = reverse(node.next);
        node.next.next = node;
        node.next = null;
        return newHead;
    }
}
```
