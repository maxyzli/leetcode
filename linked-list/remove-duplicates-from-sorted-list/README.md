# Remove Duplicates from Sorted List

# Solution 1

Two Pointers

```java
/**
 * Question   : 83. Remove Duplicates from Sorted List
 * Complexity : Time: O(n) ; Space: O(1)
 * Topics     : LL
 */
class Solution {
    public ListNode deleteDuplicates(ListNode head) {
        if (head == null || head.next == null) {
            return head;
        }

        ListNode dummy = new ListNode();
        dummy.next = head;
        ListNode prev = dummy;
        ListNode slow = head;
        ListNode fast = head.next;

        while (fast != null) {
            if (slow.val != fast.val) {
                prev.next = slow;
                prev = prev.next;
                slow = fast;
            }
            fast = fast.next;
        }

        prev.next = slow;
        prev = prev.next;
        prev.next = null;

        return dummy.next;
    }
}
```
