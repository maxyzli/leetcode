# Encode and Decode Strings

## Solution 1

```
// Take ["a:b", "c"] for example, the encoded word is s = "3:a:b1:c".

public class Codec {
    // TC: O(n)
    public String encode(List<String> strs) {
        StringBuilder sb = new StringBuilder();

        for (String str : strs) {
            sb.append(str.length()).append(":").append(str);
        }

        return sb.toString();
    }

    // TC: O(n)
    public List<String> decode(String s) {
        List<String> list = new ArrayList<>();

        int endIndex = 0;
        while (endIndex != s.length()) {
            int colonIndex = s.indexOf(":", endIndex);
            int wordLength = Integer.parseInt(s.substring(endIndex, colonIndex));
            endIndex = colonIndex + wordLength + 1;
            list.add(s.substring(colonIndex + 1, endIndex));
        }

        return list;
    }
}
```
