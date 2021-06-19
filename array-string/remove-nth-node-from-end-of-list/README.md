# Remove Nth Node From End of List

## Solution 1

```java
/**
 * Question   : 19. Remove Nth Node From End of List
 * Complexity : Time: O(n) ; Space: O(1)
 * Topics     : Linked List
 */
class Solution {
    public ListNode removeNthFromEnd(ListNode head, int n) {
        int len = length(head);
        int step = len - n;

        if (step == 0) {
            return head.next;
        }

        ListNode prev = null;
        ListNode temp = head;
        while (step != 0) {
            prev = temp;
            temp = temp.next;
            step--;
        }

        prev.next = prev.next.next;

        return head;
    }

    private int length(ListNode head) {
        if (head == null) {
            return 0;
        }
        return 1 + length(head.next);
    }
}
```

## Solution 2

Two pointers

```java
public class Solution {
    public ListNode removeNthFromEnd(ListNode head, int n) {
        if (head == null || head.next == null) {
            return null;
        }

        ListNode slow = head, fast = head;

        for (int i = 0; i < n; i++) {
            fast = fast.next;
        }

        // Remove Head Node.
        if (fast == null) {
            return head.next;
        }

        while (fast.next != null) {
            slow = slow.next;
            fast = fast.next;
        }

        slow.next = slow.next.next;

        return head;
    }
}
```
