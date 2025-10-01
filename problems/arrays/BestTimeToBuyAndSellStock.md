Leetcode 121

Problem : Given an array prices where prices[i] is the price of a stock on day i, find the maximum profit you can achieve by buying once and selling once

1️⃣ Brute Force Approach

Idea : Check all pairs (i, j) where i < j and calculate profit prices[j] - prices [i].
Time complexity : O(n^2)
Space complexity : O(1)

            public int maxProfitBruteForce(int [] prices) {
                int maxProfit = 0;
                for(int i = 0; i< prices.length; i++){
                    for(int j = i+1; j< prices.length; j++){
                        maxProfit = Math.max(maxProfit, prices[j] - prices[i]);
                    }
                }
                return maxProfit;
            }

2️⃣ Optimized Approach (Single Pass / Greedy)

Idea : Track the minimum price so far while iteration
Update maxProfit as current price - minPrice
Time complexity : O(n)
Space complexity : O(1)

                public int maxProfitOptimized(int [] prices){
                    int minPrice = Integer.MIN_VALUE;
                    int maxProfit = 0;
                    for(int price :prices){
                        if( price < minPrice) minPrice = price;
                        else maxProfit = Math.max(maxProfit, price - minPrice);
                    }
                    return maxProfit;
                }

Dry Run Example
prices = [7, 1, 5, 3, 6, 4]

                | Day | Price | Min Price | Max Profit |
                | --- | ----- | --------- | ---------- |
                | 0   | 7     | 7         | 0          |
                | 1   | 1     | 1         | 0          |
                | 2   | 5     | 1         | 4          |
                | 3   | 3     | 1         | 4          |
                | 4   | 6     | 1         | 5          |
                | 5   | 4     | 1         | 5          |
Answer : 5


