Leetcode 875

Koko wants to finish all bananas in h hours.

She chooses a speed k (bananas per hour).
Each pile consumes:

hours needed = ceil(pile / k)


If total hours needed ≤ h → ✅ k is valid
Else → ❌ k is too slow

We need the minimum k.

This is the classic pattern:

✅ Binary Search on Answer
because the function:

speed ↑ → hours ↓ (monotonically decreasing)


So we can binary search on eating speed:

low = 1
high = max(piles)

✅ Pattern / Key Idea

Binary Search on the Minimum Feasible Value

For each candidate speed mid, compute total hours:

for each pile:
    hours += (pile + mid - 1) / mid   // ceiling(pile/mid)


If hours > h → need higher speed

If hours ≤ h → valid, try smaller speed

piles = [3, 6, 7, 11], h = 8

Try k = 6:
3/6 → 1
6/6 → 1
7/6 → 2
11/6 → 2

Total = 6 ≤ 8  ✅ valid → try smaller

                                class Solution {
                                    public int minEatingSpeed(int[] piles, int h) {
                                        int left = 1;
                                        int right = 0;
                                        for (int p : piles) right = Math.max(right, p);

                                        while (left < right) {
                                            int mid = left + (right - left) / 2;

                                            if (canFinish(piles, h, mid)) {
                                                right = mid;    // try smaller speed
                                            } else {
                                                left = mid + 1; // must increase speed
                                            }
                                        }

                                        return left;
                                    }

                                    private boolean canFinish(int[] piles, int h, int speed) {
                                        long hours = 0;
                                        for (int p : piles) {
                                            hours += (p + speed - 1) / speed; // ceil
                                        }
                                        return hours <= h;
                                    }
                                }

| Operation                          | Complexity           |
| ---------------------------------- | -------------------- |
| Binary Search Range (1 → max pile) | O(log maxPile)       |
| Check validity for each speed      | O(n)                 |
| **Total Time**                     | **O(n log maxPile)** |
| Space                              | **O(1)**             |
