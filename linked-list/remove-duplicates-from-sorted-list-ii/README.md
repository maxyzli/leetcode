# Remove Duplicates from Sorted List II

## Solution 1

Map

```java
/**
 * Question   : 82. Remove Duplicates from Sorted List II
 * Complexity : Time: O(n) ; Space: O(1)
 * Topics     : Linked List
 */
class Solution {
    public ListNode deleteDuplicates(ListNode head) {
        if (head == null) {
            return null;
        }

        Map<Integer, Integer> map = new HashMap<>();

        ListNode curr = head;
        while (curr != null) {
            map.putIfAbsent(curr.val, 0);
            map.put(curr.val, map.get(curr.val) + 1);
            curr = curr.next;
        }

        ListNode dummy = new ListNode(0);
        ListNode p = dummy;

        curr = head;
        while (curr != null) {
            if (map.get(curr.val) == 1) {
                p.next = curr;
                p = p.next;
            }
            curr = curr.next;
        }
        p.next = null;

        return dummy.next;
    }
}
```

## Solution 2

Two Pointers

```java
/**
 * Question   : 83. Remove Duplicates from Sorted List
 * Complexity : Time: O(n) ; Space: O(1)
 * Topics     : Linked List
 */
class Solution {
    public ListNode deleteDuplicates(ListNode head) {
        if (head == null || head.next == null) {
            return head;
        }

        ListNode dummy = new ListNode(-1);
        dummy.next = head;
        ListNode prev = dummy;
        ListNode slow = head;
        ListNode fast = head;

        int duplicate = 0;
        while (fast != null) {
            if (fast.val == slow.val) {
                duplicate++;
                fast = fast.next;
            } else {
                if (duplicate == 1) {
                    prev.next = slow;
                    prev = prev.next;
                }
                slow = fast;
                duplicate = 0;
            }
        }

        if (duplicate == 1) {
            prev.next = slow;
            prev = prev.next;
        }
        prev.next = null;

        return dummy.next;
    }
}
```
