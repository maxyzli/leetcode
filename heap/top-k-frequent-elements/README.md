# Top K Frequent Elements

# Solution 1: Heap

```java
// TC: O(nlog(k))
// SC: O(n)
class Solution {
    public int[] topKFrequent(int[] nums, int k) {
        if (k > nums.length) {
            return new int[]{};
        }

        Map<Integer, Integer> count = new HashMap<>();
        for (int num : nums) {
            count.put(num, count.getOrDefault(num, 0) + 1);
        }

        PriorityQueue<Integer> pq = new PriorityQueue<>((a, b) -> count.get(a) - count.get(b));
        for (int num : count.keySet()) {
            pq.add(num);
            if (pq.size() > k) {
                pq.remove();
            }
        }

        int[] res = new int[k];
        int j = 0;
        while (!pq.isEmpty()) {
            res[j++] = pq.remove();
        }

        return res;
    }
}
```

# Solution 2: Bucket Sort

```java
// TC: O(n)
// SC: O(n)
class Solution {
    public int[] topKFrequent(int[] nums, int k) {
        if (k > nums.length) {
            return new int[]{};
        }

        Map<Integer, Integer> count = new HashMap<>();
        for (int num : nums) {
            count.put(num, count.getOrDefault(num, 0) + 1);
        }

        int n = nums.length;
        List<Integer>[] bucket = new ArrayList[n + 1];

        for (int key : count.keySet()) {
            int freq = count.get(key);
            if (bucket[freq] == null) {
                bucket[freq] = new ArrayList<>();
            }
            bucket[freq].add(key);
        }

        int res[] = new int[k];
        int index = 0;

        for (int i = n; i >= 1; i--){
            if (bucket[i] != null){
                for (int val : bucket[i]) {
                    res[index++] = val;
                    if (index == k) {
                        return res;
                    }
                }
            }
        }

        return res;
    }
}
```
