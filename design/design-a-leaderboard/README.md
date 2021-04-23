# Design A Leaderboard

## Solution 1

Brute Force

```java
/**
 * Question   : Design A Leaderboard
 * Topics     : Design
 */
class Leaderboard {
    private Map<Integer, Integer> map;

    public Leaderboard() {
        map = new HashMap<>();
    }

    // O(1)
    public void addScore(int playerId, int score) {
        map.put(playerId, map.getOrDefault(playerId, 0) + score);
    }

    // O(nlog(n))
    public int top(int K) {
        Integer[] scores = map.values().toArray(new Integer[map.values().size()]);

        Arrays.sort(scores, (a, b) -> b - a); // Descending.

        int sum = 0;

        for (int i = 0; i < K; i++) {
            sum += scores[i];
        }

        return sum;
    }

    // O(1)
    public void reset(int playerId) {
        if (map.containsKey(playerId)) {
            map.remove(playerId);
        }
    }
}
```

## Solution 2

Map + TreeSet

```java
/**
 * Question   : Design A Leaderboard
 * Topics     : Design
 */
class Player {
    int id;
    int score;

    public Player(int id, int score) {
        this.id = id;
        this.score = score;
    }
}

class Leaderboard {
    private Map<Integer, Player> map;
    private TreeSet<Player> treeSet;

    public Leaderboard() {
        map = new HashMap<>();
        treeSet = new TreeSet<>((a, b) -> {
            if (a.score != b.score) {
                return b.score - a.score;
            }
            return a.id - b.id;
        });
    }

    // O(log(n))
    public void addScore(int playerId, int score) {
        Player player = null;
        if (map.containsKey(playerId)) {
            player = map.get(playerId);
            // If we don't remove the player from the tree set, it won't reorder the players.
            treeSet.remove(player); // O(log(n))
            player.score += score;
        } else {
            player = new Player(playerId, score);
            map.put(playerId, player);
        }
        treeSet.add(player); // O(log(n))
    }

    // O(k)
    public int top(int K) {
        Iterator<Player> it = treeSet.iterator();

        int sum = 0;

        for (int i = 0; i < K; i++) {
            if (!it.hasNext()) {
                break;
            }
            sum += it.next().score;
        }

        return sum;
    }

    // O(log(n))
    public void reset(int playerId) {
        if (map.containsKey(playerId)) {
            Player player = map.get(playerId);
            map.remove(playerId);
            treeSet.remove(player);
        }
    }
}
```

## Solution 3

Map + Heap

Note:

- PriorityQueue only guarantee the head will always be the smallest or largest element.
- TreeSet keeps all elements in sorted order.
- Iterator returned by TreeSet allows you to access all elements in sorted order.

```java
/**
 * Question   : Design A Leaderboard
 * Topics     : Design
 */
class Player {
    int id;
    int score;

    public Player(int id, int score) {
        this.id = id;
        this.score = score;
    }
}

class Leaderboard {
    private Map<Integer, Player> map;
    private PriorityQueue<Player> pq;

    public Leaderboard() {
        map = new HashMap<>();
        pq = new PriorityQueue<>((a, b) -> {
            if (a.score != b.score) {
                return b.score - a.score;
            }
            return a.id - b.id;
        });
    }

    // O(log(n))
    public void addScore(int playerId, int score) {
        Player player = null;
        if (map.containsKey(playerId)) {
            player = map.get(playerId);
            // If we don't remove the player from the tree set, it won't reorder the players.
            pq.remove(player); // O(log(n))
            player.score += score;
        } else {
            player = new Player(playerId, score);
            map.put(playerId, player);
        }
        pq.add(player); // O(log(n))
    }

    // O(klog(n))
    public int top(int K) {
        int sum = 0;

        List<Player> poppedPlayers = new ArrayList<>();

        // In PriorityQueue, only head is biggest/smallest.
        // The others are not soted, so we cannot use PQ iterator.
        for (int i = 0; i < K; i++) {
            if (pq.isEmpty()) {
                break;
            }
            Player player = pq.remove();
            sum += player.score;
            poppedPlayers.add(player);
        }

        // We need to put the players back. O(klog(n))
        for (Player player : poppedPlayers) {
            pq.add(player);
        }

        return sum;
    }

    // O(log(n))
    public void reset(int playerId) {
        if (map.containsKey(playerId)) {
            Player player = map.get(playerId);
            map.remove(playerId);
            pq.remove(player);
        }
    }
}
```
