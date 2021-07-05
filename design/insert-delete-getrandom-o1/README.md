# Insert Delete GetRandom O(1)

## Solution 1

```java
class RandomizedSet {
    private Map<Integer, Integer> val2Idx;
    private List<Integer> nums;
    private Random rand = new Random();

    public RandomizedSet() {
        this.nums = new ArrayList<>();
        this.val2Idx = new HashMap<>();
    }

    public boolean insert(int val) {
        if (val2Idx.containsKey(val)) {
            return false;
        }
        this.nums.add(val);
        val2Idx.put(val, nums.size() - 1);
        return true;
    }

    public boolean remove(int val) {
        if (!val2Idx.containsKey(val)) {
            return false;
        }

        // Replace val with last number.
        int index = val2Idx.get(val);
        int lastNum = nums.get(nums.size() - 1);
        nums.set(index, lastNum);
        val2Idx.put(lastNum, index);

        // Remove last element in array.
        nums.remove(nums.size() - 1);
        // Remove val from map.
        val2Idx.remove(val);

        return true;
    }

    public int getRandom() {
        // nextInt(10) -> 0 - 9;
        return nums.get(rand.nextInt(nums.size()));
    }
}
```
