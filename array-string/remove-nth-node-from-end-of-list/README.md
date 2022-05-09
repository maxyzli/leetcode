# Remove Nth Node From End of List

## Solution 1: Two Pointers

```java
// TC: O(n)
// SC: O(1)
class Solution {
    public ListNode removeNthFromEnd(ListNode head, int n) {
        if (head == null) {
            return null;
        }

        ListNode fast = head;
        
        int k = n;
        while (k != 0) {
            fast = fast.next;
            k--;
        }
        
        ListNode prev = null;
        ListNode slow = head;
        
        while (fast != null) {
            prev = slow;
            slow = slow.next;
            fast = fast.next;
        }
        
        // Remove head.
        if (prev == null) {
            return head.next;
        }
        
        prev.next = prev.next.next;
        
        return head;
    }
}
```
