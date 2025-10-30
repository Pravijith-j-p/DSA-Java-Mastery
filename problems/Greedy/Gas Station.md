Leetcode 134

Problem:
You are given:

gas[i] → gas available at station i

cost[i] → gas needed to travel from station i to (i+1) % n

Goal:
Return the starting station index from which you can complete the full circle once, or -1 if impossible.

✅ ✅ Greedy Key Insight
1. If total gas < total cost → impossible

Because even in the best path, the whole system doesn't have enough gas.

2. Single-pass Greedy

We try stations one by one:

Maintain tank — current fuel while simulating the trip.

If tank becomes negative at station i,
then no station from previous start to i can be a valid starting point.

So we set:

start = i + 1
tank = 0


Why?
Because if you can’t reach i+1 starting from earlier, starting even earlier makes it worse.

Example Walkthrough
Input:

gas = [1,2,3,4,5]
cost = [3,4,5,1,2]

| i | gas-cost | tank      | start |
| - | -------- | --------- | ----- |
| 0 | -2       | -2 → fail | 1     |
| 1 | -2       | -2 → fail | 2     |
| 2 | -2       | -2 → fail | 3     |
| 3 | +3       | 3         | stays |
| 4 | +3       | 6         | stays |

total gas = total cost → possible
✅ start = 3

                                class Solution {
                                    public int canCompleteCircuit(int[] gas, int[] cost) {
                                        int total = 0;
                                        int tank = 0;
                                        int start = 0;

                                        for (int i = 0; i < gas.length; i++) {
                                            int diff = gas[i] - cost[i];
                                            total += diff;
                                            tank += diff;

                                            if (tank < 0) {         // cannot start from here
                                                start = i + 1;
                                                tank = 0;
                                            }
                                        }

                                        return total >= 0 ? start : -1;
                                    }
                                }

| Complexity | Value |
| ---------- | ----- |
| **Time**   | O(n)  |
| **Space**  | O(1)  |
