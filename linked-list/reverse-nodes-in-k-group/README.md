# Reverse Nodes in k-Group

## Solution 1

```java
/**
 * Question   : 25. Reverse Nodes in k-Group
 * Complexity : Time: O(n) ; Space: O(n)
 * Topics     : Linked List
 */
class Solution {
    ListNode next;

    public ListNode reverseKGroup(ListNode head, int k) {
        if (head == null || head.next == null) {
            return head;
        }
        if (getLength(head) < k) {
            return head;
        }

        ListNode end = head;
        ListNode newHead = reverse(head, k);
        end.next = reverseKGroup(next, k);

        return newHead;
    }

    private ListNode reverse(ListNode head, int n) {
        if (head == null) {
            return null;
        }
        if (head.next == null || n == 1) {
            next = head.next;
            return head;
        }
        ListNode newHead = reverse(head.next, n - 1);
        head.next.next = head;
        head.next = null;
        return newHead;
    }

    private int getLength(ListNode head) {
        if (head == null) {
            return 0;
        }
        return 1 + getLength(head.next);
    }
}
```
