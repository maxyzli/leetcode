# Intersection of Two Linked Lists

## Solution 1

```java
/**
 * Question   : 160. Intersection of Two Linked Lists
 * Topics     : Linked List
 * Complexity : Time: O(n) ; Space: O(1)
 */
public class Solution {
    public ListNode getIntersectionNode(ListNode headA, ListNode headB) {
        if (headA == null || headB == null) {
            return null;
        }
        if (headA == headB) {
            return headA;
        }

        int lengthA = getLength(headA);
        int lengthB = getLength(headB);

        if (lengthB < lengthA) {
            return getIntersectionNode(headB, headA);
        }

        ListNode p1 = headA;
        ListNode p2 = headB;

        for (int i = 0; i < lengthB - lengthA; i++) {
            p2 = p2.next;
        }

        while (p1 != null && p2 != null) {
            if (p1 == p2) {
                return p1;
            }
            p1 = p1.next;
            p2 = p2.next;
        }

        return null;
    }

    private int getLength(ListNode head) {
        if (head == null) {
            return 0;
        }
        return 1 + getLength(head.next);
    }
}
```
