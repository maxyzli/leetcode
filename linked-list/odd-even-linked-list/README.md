# Odd Even Linked List

## Solution 1

```java
/**
 * Question   : 328. Odd Even Linked List
 * Complexity : Time: O(n) ; Space: O(n)
 * Topics     : Linked List
 */
class Solution {
    public ListNode oddEvenList(ListNode head) {
        if (head == null || head.next == null) {
            return head;
        }

        ListNode dummyOdd = new ListNode(0);
        ListNode dummyEven = new ListNode(0);
        ListNode oddPrev = dummyOdd;
        ListNode evenPrev = dummyEven;
        ListNode curr = head;

        while (curr != null) {
            oddPrev.next = curr;
            oddPrev = oddPrev.next;

            curr = curr.next;

            if (curr != null) {
                evenPrev.next = curr;
                evenPrev = evenPrev.next;
                curr = curr.next;
            }
        }
        oddPrev.next = null;
        evenPrev.next = null;

        // Connect odd and even.
        oddPrev.next = dummyEven.next;

        return dummyOdd.next;
    }
}
```
