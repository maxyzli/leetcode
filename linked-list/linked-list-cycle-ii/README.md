# Linked List Cycle II

## Solution 1

```java
/**
 * Question   : 142. Linked List Cycle II
 * Complexity : Time: O(n) ; Space: O(1)
 * Topics     : Linked List
 */
public class Solution {
    public ListNode detectCycle(ListNode head) {
        if (head == null || head.next == null) {
            return null;
        }

        ListNode slow = head;
        ListNode fast = head;
        boolean hasLoop = false;

        while (fast != null && fast.next != null) {
            fast = fast.next.next;
            slow = slow.next;
            if (slow == fast) {
                hasLoop = true;
                break;
            }
        }

        if (hasLoop == false) {
            return null;
        }

        ListNode p1 = head;
        ListNode p2 = slow;

        while (p1 != p2) {
            p1 = p1.next;
            p2 = p2.next;
        }

        return p1;
    }
}
```
