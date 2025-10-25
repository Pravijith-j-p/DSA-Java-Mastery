Leetcode 309

Problem : 
Given an integer array prices where prices[i] is the price of a stock on the ith day.
You may complete as many transactions as you like (buy one and sell one share of the stock multiple times) with the following rules:

    - After you seel your stock, you cannot but stock on the next day (cooldown of 1 day).

Return the maximum profit you can achieve

Example 1:
Input : prices = [1, 2, 3, 0, 2]
Output :
3

Explanation : 
transactions = [buy, sell, cooldown, buy, sell]

transactions = [buy, sell, cooldown, buy, sell]
profit = (2 - 1) + (2 - 0) = 3


🔹 Example 2
Input:
prices = [1]

Output:
0
(No transaction possible)

⚙️ Approach — Dynamic Programming (State Machine)

We’ll use 3 states to represent what we can do each day:

State	Meaning
hold	We currently hold a stock.
sold	We just sold the stock today.
rest	We are in the cooldown or doing nothing.

Now the transitions:

hold[i] = max(hold[i-1], rest[i-1] - prices[i])
sold[i] = hold[i-1] + prices[i]
rest[i] = max(rest[i-1], sold[i-1])


You can continue holding from yesterday OR buy today (after resting).

You can sell today if you held yesterday.

You can rest today if you were resting or just sold yesterday.

class Solution {
    public int maxProfit(int[] prices) {
        if (prices.length == 0) return 0;

        int n = prices.length;
        int hold = -prices[0]; // initially, buy the stock
        int sold = 0;
        int rest = 0;

        for (int i = 1; i < n; i++) {
            int prevHold = hold;
            int prevSold = sold;
            int prevRest = rest;

            hold = Math.max(prevHold, prevRest - prices[i]);
            sold = prevHold + prices[i];
            rest = Math.max(prevRest, prevSold);
        }

        // Max profit cannot be from a "holding" state (since it's not sold)
        return Math.max(sold, rest);
    }
}
