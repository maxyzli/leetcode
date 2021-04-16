# Letter Combinations of a Phone Number

## Solution 1

```java
/**
 * Question   : 17. Letter Combinations of a Phone Number
 * Complexity : Time: O(4^n) ; Space: O(n)
 * Topics     : Backtracking
 */
class Solution {
    HashMap<Character, String> mapping = new HashMap<>(){{
        put('2', "abc");
        put('3', "def");
        put('4', "ghi");
        put('5', "jkl");
        put('6', "mno");
        put('7', "pqrs");
        put('8', "tuv");
        put('9', "wxyz");
    }};

    public List<String> letterCombinations(String digits) {
        if (digits == null || digits.length() == 0) {
            return new ArrayList<>();
        }

        StringBuilder sb = new StringBuilder();
        List<String> res = new ArrayList<>();
        int digitIdx = 0;

        letterCombinationsUtil(digits, digitIdx, mapping, sb, res);

        return res;
    }

    private void letterCombinationsUtil(String digits, int digitIdx, HashMap<Character, String> mapping, StringBuilder sb, List<String> res) {
        if (digitIdx == digits.length()) {
            res.add(sb.toString());
            return;
        }

        String str = mapping.get(digits.charAt(digitIdx));
        for (int i = 0; i < str.length(); i++) {
            sb.append(str.charAt(i));
            letterCombinationsUtil(digits, digitIdx + 1, mapping, sb, res);
            sb.deleteCharAt(sb.length() - 1);
        }
    }
}
```

## Solution 2

Queue

```java
class Solution {
    HashMap<Character, String> mapping = new HashMap<>(){{
        put('2', "abc");
        put('3', "def");
        put('4', "ghi");
        put('5', "jkl");
        put('6', "mno");
        put('7', "pqrs");
        put('8', "tuv");
        put('9', "wxyz");
    }};

    public List<String> letterCombinations(String digits) {
        if (digits == null || digits.length() == 0) {
            return new ArrayList<>();
        }

        Queue<String> queue = new LinkedList<>();

        // Initialization.
        String str = mapping.get(digits.charAt(0));
        for (int i = 0; i < str.length(); i++) {
            queue.add(str.charAt(i) + "");
        }

        for (int i = 1; i < digits.length(); i++) {
            str = mapping.get(digits.charAt(i));
            int queueSize = queue.size();
            for (int j = 0; j < queueSize; j++) {
                String temp = queue.remove();
                for (char c : str.toCharArray()) {
                    queue.add(temp + c);
                }
            }
        }

        List<String> res = new ArrayList<>();
        while (!queue.isEmpty()) {
            res.add(queue.remove());
        }

        return res;
    }
}
```
