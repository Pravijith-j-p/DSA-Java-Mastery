Leetcode 1899

Problem Summary

You are given:

A list of triplets → each is [a, b, c]

A target triplet → [x, y, z]

You can merge two triplets by taking elementwise max:

[a1, b1, c1]  merge  [a2, b2, c2]  =>
[max(a1,a2), max(b1,b2), max(c1,c2)]


Goal:
Return true if you can merge ANY number of given triplets to get exactly the target triplet.

✅ Key Insight (Greedy)

To contribute to the target triplet, a candidate triplet must obey:

a <= x,  b <= y,  c <= z


If a triplet has any value exceeding the target,
it can never be used → discard it.

✅ Greedy Approach

Iterate over all triplets.

Keep a boolean array tracking whether we matched each component of the target:

possible = [false, false, false]


If a triplet fits within the target (a<=x && b<=y && c<=z),
then see which positions match exactly the target value:

if a == x → possible[0] = true

if b == y → possible[1] = true

if c == z → possible[2] = true

After checking all triplets:

return possible[0] && possible[1] && possible[2]


Because merging takes max, to form the target,
each max must be contributed by some triplet.

Example Walkthrough
Input
triplets = [[2,5,3], [1,8,4], [1,7,5]]
target = [2,7,5]


Check valid triplets ≤ target → only [2,5,3] and [1,7,5]

[2,5,3]: contributes a = 2

[1,7,5]: contributes b = 7 and c = 5

All three positions matched ✅
So result = true

                                class Solution {
                                    public boolean mergeTriplets(int[][] triplets, int[] target) {
                                        boolean[] pos = new boolean[3];  // track target contributions
                                        
                                        for (int[] t : triplets) {
                                            if (t[0] <= target[0] && t[1] <= target[1] && t[2] <= target[2]) {
                                                
                                                if (t[0] == target[0]) pos[0] = true;
                                                if (t[1] == target[1]) pos[1] = true;
                                                if (t[2] == target[2]) pos[2] = true;
                                            }
                                        }
                                        
                                        return pos[0] && pos[1] && pos[2];
                                    }
                                }

| Complexity | Value |
| ---------- | ----- |
| **Time**   | O(n)  |
| **Space**  | O(1)  |
