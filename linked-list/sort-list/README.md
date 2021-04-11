# Sort List

## Solution 1

```java
/**
 * Question   : 147. Insertion Sort List
 * Complexity : Time: O(nlog(n)) ; Space: O(1)
 * Topics     : Linked List
 */
class Solution {
    public ListNode sortList(ListNode head) {
        if (head == null || head.next == null) {
            return head;
        }

        ListNode slow = head;
        // Key difference.
        ListNode fast = head.next;
        while (fast != null && fast.next != null) {
            slow = slow.next;
            fast = fast.next.next;
        }
        ListNode rightHead = slow.next;
        slow.next = null;

        ListNode left = sortList(head);
        ListNode right = sortList(rightHead);

        return mergeTwoLists(left, right);
    }

    public ListNode mergeTwoLists(ListNode l1, ListNode l2) {
        ListNode dummy = new ListNode(-1);
        ListNode prev = dummy;

        while (l1 != null && l2 != null) {
            if (l1.val <= l2.val) {
                prev.next = l1;
                l1 = l1.next;
            } else {
                prev.next = l2;
                l2 = l2.next;
            }
            prev = prev.next;
        }

        while (l1 != null) {
            prev.next = l1;
            l1 = l1.next;
            prev = prev.next;
        }

        while (l2 != null) {
            prev.next = l2;
            l2 = l2.next;
            prev = prev.next;
        }

        return dummy.next;
    }
}
```
