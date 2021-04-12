# Merge k Sorted Lists

## Solution 1

Merge one by one

```java
/**
 * Question   : Merge k Sorted Lists
 * Complexity : Time: O(n*k^2) ; Space: O(1)
 * Topics     : Linked List
 */
class Solution {
    public ListNode mergeKLists(ListNode[] lists) {
        if (lists.length ==0 ) {
            return null;
        }

        ListNode outputList = lists[0];

        for (int i = 1; i < lists.length; i++) {
            outputList = merge(outputList, lists[i]);
        }

        return outputList;
    }

    private static ListNode merge(ListNode listA, ListNode listB) {
        if (listA == null) {
            return listB;
        }
        if (listB == null) {
            return listA;
        }

        if (listA.val <= listB.val) {
            listA.next = merge(listA.next, listB);
            return listA;
        } else {
            listB.next = merge(listA, listB.next);
            return listB;
        }
    }
}
```

## Solution 2

Divide and Conquer

```java
/**
 * Question   : 23. Merge k Sorted Lists
 * Complexity : Time: O(kn*log(k)) ; Space: O(log(k))
 * Topics     : Linked List
 */
class Solution {
    public ListNode mergeKLists(ListNode[] lists) {
        if (lists == null || lists.length == 0) {
            return null;
        }
        return mergeKListsUtil(lists, 0, lists.length - 1);
    }

    private ListNode mergeKListsUtil(ListNode[] lists, int low, int high) {
        if (low >= high) {
            return lists[low];
        }

        int mid = low + (high - low) / 2;

        ListNode mergedLeft = mergeKListsUtil(lists, low, mid);
        ListNode mergedRight = mergeKListsUtil(lists, mid + 1, high);

        return merge(mergedLeft, mergedRight);
    }

    private static ListNode merge(ListNode listA, ListNode listB) {
        if (listA == null) {
            return listB;
        }
        if (listB == null) {
            return listA;
        }

        if (listA.val <= listB.val) {
            listA.next = merge(listA.next, listB);
            return listA;
        } else {
            listB.next = merge(listA, listB.next);
            return listB;
        }
    }
}
```

## Solution 3

PriorityQueue

```java
/**
 * Question   : 23. Merge k Sorted Lists
 * Complexity : Time: O(knlog(k)) ; Space: O(k)
 * Topics     : Linked List
 */
class Solution {
    public ListNode mergeKLists(ListNode[] lists) {
        if (lists == null || lists.length == 0) {
            return null;
        }

        PriorityQueue<ListNode> pq = new PriorityQueue<>((a, b) -> {
            return a.val - b.val;
        });

        ListNode dummy = new ListNode(-1);
        ListNode p = dummy;

        for (int i = 0; i < lists.length; i++) {
            if (lists[i] != null) {
                pq.add(lists[i]);
            }
        }

        while (!pq.isEmpty()) {
            ListNode temp = pq.remove();
            p.next = temp;
            p = p.next;
            if (temp.next != null) {
                pq.add(temp.next);
            }
        }

        return dummy.next;
    }
}
```
