Leetcode 312

🧩 Problem Statement

You are given n balloons, each balloon has a number on it represented by array nums.
You are asked to burst all balloons.

If you burst the i-th balloon, you gain:

coins = nums[left] * nums[i] * nums[right]


where:

left and right are adjacent balloons that remain (not yet burst).

After bursting balloon i, it disappears — meaning you can’t use it again.

Return the maximum coins you can collect by bursting balloons wisely.

.

🔹 Example 1

Input:
nums = [3,1,5,8]

Output:
167

Explanation:
Best order: [1,5,3,8] or [1,5,8,3]
Steps:

Burst 1 → gain 3*1*5 = 15
Burst 5 → gain 3*5*8 = 120
Burst 3 → gain 1*3*8 = 24
Burst 8 → gain 1*8*1 = 8
Total = 167

⚙️ Key Insight — “Last Balloon to Burst”

Instead of thinking which balloon to burst first,
think which balloon is the last to burst in a range.

If you know which balloon is last in range (i, j):

You’ve already burst everything between i and j.

The remaining balloons are i (left boundary) and j (right boundary).

So the coins gained when bursting k last are:

nums[i] * nums[k] * nums[j]


Plus whatever you earned from bursting in the left and right intervals:

dp[i][k] + dp[k][j]

🧠 DP Definition

Let:

dp[i][j] = maximum coins obtainable by bursting all balloons 
           strictly between i and j


(i.e., balloons in the open interval (i, j))

🧮 Transition Formula

For every range (i, j):

for k in (i+1 ... j-1):
    dp[i][j] = max(dp[i][j],
                   nums[i]*nums[k]*nums[j] + dp[i][k] + dp[k][j])


We try every possible k as the last balloon in (i, j).

🧱 Base Case

If there are no balloons between i and j → dp[i][j] = 0

We also pad the array with 1 at both ends:

nums = [1, 3, 1, 5, 8, 1]


to simplify boundary calculations.

                                class Solution {
                                    public int maxCoins(int[] nums) {
                                        int n = nums.length;
                                        int[] arr = new int[n + 2];
                                        arr[0] = 1;
                                        arr[n + 1] = 1;
                                        for (int i = 0; i < n; i++) arr[i + 1] = nums[i];

                                        int[][] dp = new int[n + 2][n + 2];

                                        // len = distance between left and right
                                        for (int len = 2; len < n + 2; len++) {           // ✅ fix: '<' not '<='
                                            for (int left = 0; left < n + 2 - len; left++) {
                                                int right = left + len;
                                                for (int k = left + 1; k < right; k++) {
                                                    dp[left][right] = Math.max(dp[left][right],
                                                        arr[left] * arr[k] * arr[right] + dp[left][k] + dp[k][right]);
                                                }
                                            }
                                        }

                                        return dp[0][n + 1];
                                    }
                                }
                                
| Metric               | Complexity                         |
| -------------------- | ---------------------------------- |
| **Time Complexity**  | `O(n³)` — 3 nested loops (i, j, k) |
| **Space Complexity** | `O(n²)` — DP table                 |

