# Add Two Numbers

## Solution 1

Iteration (Simpler)

```java
/**
 * Question   : 2. Add Two Numbers
 * Complexity : Time: O(n) ; Space: O(n)
 * Topics     : Linked List
 */
public class Solution {
    public ListNode addTwoNumbers(ListNode l1, ListNode l2) {
        if (l1 == null) {
            return l2;
        }
        if (l2 == null) {
            return l1;
        }

        ListNode dummy = new ListNode(0);
        ListNode p = dummy;
        ListNode p1 = l1;
        ListNode p2 = l2;
        int carry = 0;

        while (p1 != null || p2 != null) {
            int sum = carry;

            if (p1 != null) {
                sum += p1.val;
                p1 = p1.next;
            }
            if (p2 != null) {
                sum += p2.val;
                p2 = p2.next;
            }

            carry = sum / 10;
            p.next = new ListNode(sum % 10);
            p = p.next;
        }

        if (carry > 0) {
            p.next = new ListNode(carry);
        }

        return dummy.next;
    }
}
```

## Solution 2

Recursion

```java
/**
 * Question   : Add Two Numbers
 * Complexity : Time: O(m+n) ; Space: O(m+n)
 * Topics     : Linked List
 */
public class Solution {
    public ListNode addTwoNumbers(ListNode l1, ListNode l2) {
        int l1Length = getLength(l1);
        int l2Length = getLength(l2);
        return l1Length > l2Length ? addTwoNumbers(l1, l2, 0) : addTwoNumbers(l2, l1, 0);
    }

    // L1 is always longer.
    private ListNode addTwoNumbers(ListNode l1, ListNode l2, int carry) {
        if (l1 == null && carry == 0) {
            return null;
        }
        if (l1 == null && carry != 0) {
            return new ListNode(carry);
        }

        int sum = l1.val + carry;

        if (l2 != null) sum += l2.val;

        l1.val = sum % 10;
        l1.next = addTwoNumbers(l1.next, l2 == null ? null : l2.next, sum / 10);

        return l1;
    }

    private int getLength(ListNode head) {
        if (head == null) return 0;
        return 1 + getLength(head.next);
    }
}
```
