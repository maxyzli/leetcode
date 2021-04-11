# Insertion Sort List

## Solution 1

```java
/**
 * Question   : 147. Insertion Sort List
 * Complexity : Time: O(n^2) ; Space: O(1)
 * Topics     : Linked List
 */
class Solution {
    public ListNode insertionSortList(ListNode head) {
        if (head == null || head.next == null) {
            return head;
        }

        ListNode dummy = new ListNode(-1);
        dummy.next = head;

        ListNode prev = head;
        ListNode curr = head.next;
        while (curr != null) {
            if (curr.val >= prev.val) {
                prev = curr;
                curr = curr.next;
            } else {
                ListNode p = dummy;
                while (p.next != null && p.next.val <= curr.val) {
                    p = p.next;
                }
                prev.next = curr.next;
                curr.next = p.next;
                p.next = curr;

                curr = prev.next;
            }
        }

        return dummy.next;
    }
}
```
