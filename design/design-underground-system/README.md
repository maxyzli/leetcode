# Design Underground System

## Solution 1

```java
/**
 * Question   : 1396. Design Underground System
 * Topics     : Design
 */
class UndergroundSystem {
    Map<Integer, Start> startInfo;
    Map<String, SumAmount> table;

    public UndergroundSystem() {
        startInfo = new HashMap<>();
        table = new HashMap<>();
    }

    public void checkIn(int id, String stationName, int t) {
        startInfo.put(id, new Start(stationName, t));
    }

    public void checkOut(int id, String stationName, int t) {
        Start start = startInfo.get(id);
        String key = start.station + "-" + stationName;
        SumAmount sumAmount = table.getOrDefault(key, new SumAmount(0, 0));
        sumAmount.sum += t - start.time;
        sumAmount.amount += 1;
        table.put(key, sumAmount);
    }

    public double getAverageTime(String startStation, String endStation) {
        String key = startStation + "-" + endStation;
        SumAmount sumAmount = table.get(key);
        return 1.0 * sumAmount.sum / sumAmount.amount;
    }
}

class Start {
    public String station;
    public int time;

    public Start(String station, int time) {
        this.station = station;
        this.time = time;
    }
}

class SumAmount {
    public int sum;
    public int amount;

    public SumAmount(int sum, int amount) {
        this.sum = sum;
        this.amount = amount;
    }
}
```
