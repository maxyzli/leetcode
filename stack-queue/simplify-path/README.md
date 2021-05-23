# Simplify Path

## Solution 1

Stack

```java
/**
 * Question   : 71. Simplify Path
 * Complexity : Time: O(n) ; Space: O(n)
 * Topics     : Stack/Queue
 */
class Solution {
    public String simplifyPath(String path) {
        if (path == null || path.length() == 0) {
            return "";
        }

        String[] paths = path.split("/");

        ArrayDeque<String> deque = new ArrayDeque<>();

        for (int i = 0; i < paths.length; i++) {
            String str = paths[i];

            if (str.equals("..")) {
                if (!deque.isEmpty()) {
                    deque.pop();
                }
            } else if (str.equals(".") || str.equals("")) {
                continue;
            } else {
                deque.push(str);
            }
        }

        if (deque.isEmpty()) {
            return "/";
        }

        StringBuilder sb = new StringBuilder();
        while (!deque.isEmpty()) {
            sb.append("/");
            sb.append(deque.removeLast());
        }

        return sb.toString();
    }
}
```

## Solution 2

LinkedList

```java
/**
 * Question   : 71. Simplify Path
 * Complexity : Time: O(n) ; Space: O(n)
 * Topics     : Stack/Queue
 */
class Solution {
    public String simplifyPath(String path) {
        if (path == null || path.equals("")) {
            return "";
        }

        List<String> list = new LinkedList<>();
        String[] paths = path.split("/");

        for (int i = 0; i < paths.length; i++) {
            if (paths[i].equals("..")) {
                if (!list.isEmpty()) {
                    list.remove(list.size() - 1);
                }
            } else if (paths[i].equals(".") || paths[i].equals("")) {
                continue;
            } else {
                list.add(paths[i]);
            }
        }

        return "/" + String.join("/", list);
    }
}
```
