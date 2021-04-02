# Merge Two Sorted Lists

## Solution 1

Recursion

```java
/**
 * Question   : Merge Two Sorted Lists
 * Complexity : Time: O(n) ; Space: O(1)
 * Topics     : Linked List
 * Date       : 2020/12/07
 */
public class Solution {
    public ListNode mergeTwoLists(ListNode l1, ListNode l2) {
        if (l1 == null) {
            return l2;
        }
        if (l2 == null) {
            return l1;
        }

        if (l1.val <= l2.val) {
            l1.next = mergeTwoLists(l1.next, l2);
            return l1;
        } else {
            l2.next = mergeTwoLists(l1, l2.next);
            return l2;
        }
    }
}
```

## Solution 2

Iteration

```java
/**
 * Question   : 21. Merge Two Sorted Lists
 * Complexity : Time: O(n) ; Space: O(1)
 * Topics     : Linked List
 * Date       : 2021/01/26
 */
public class Solution {
    public ListNode mergeTwoLists(ListNode l1, ListNode l2) {
        ListNode sentinel = new ListNode(-1);
        ListNode prev = sentinel;

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

        return sentinel.next;
    }
}
```
