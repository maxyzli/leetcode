# Remove Linked List Elements

## Solution 1

```java
/**
 * Question   : 203. Remove Linked List Elements
 * Complexity : Time: O(n) ; Space: O(1)
 * Topics     : Linked List
 */
public class Solution {
    public ListNode removeElements(ListNode head, int val) {
        if (head == null) {
            return null;
        }

        ListNode dummy = new ListNode(0);
        ListNode p = dummy;
        ListNode temp = head;

        while (temp != null) {
            if (temp.val != val) {
                p.next = temp;
                p = p.next;
            }
            temp = temp.next;
        }
        p.next = null;

        return dummy.next;
    }
}
```
