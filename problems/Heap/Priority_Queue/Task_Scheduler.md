Leetcode 621

Problem :
- A list of CPU Tasks(each represented by a capital letter, like A, B, C)
- A cooldown interval n, which means same tasks must be seperated by at least n intervals

You must return the minimum time units needed to finish all tasks

Each task takes 1 unit of time 
The CPU can be idle if necessary

Example:
Input : tasks =['A', 'A', 'A', 'B', 'B', 'B'] , n= 2

Output : 8

Explanation :
A->B->idle->A->B->idle->A->B

Total time = 8

Intution :
If two same tasks must be at least n apart,
then the most frequent task determines how the CPU schedule looks

Step 1 : Count frequencies

A -> 3 times
B -> 3 times

Step 2 : The pattern idea
Arrange the most frequent task first:

A _ _ A _ _ A

There are 3 - 1 gaps between A's
each gap must have at least n = 2 spaces -> _ _

Now fill the gaps with other tasks

AB _ AB _ A

Then fill remaining gaps with idle time
✅ 8 units total

Approach 1: Math Formula (Efficient)

Time Complexity: O(N)
Space Complexity: O(1)

import java.util.*;

                                        class Solution {
                                            public int leastInterval(char[] tasks, int n) {
                                                int[] freq = new int[26];
                                                for (char c : tasks) freq[c - 'A']++;

                                                Arrays.sort(freq);
                                                int maxFreq = freq[25];
                                                int countMax = 0;

                                                // count how many tasks have the max frequency
                                                for (int i = 25; i >= 0; i--) {
                                                    if (freq[i] == maxFreq) countMax++;
                                                    else break;
                                                }

                                                return Math.max(tasks.length, (maxFreq - 1) * (n + 1) + countMax);
                                            }
                                        }


