Leetcode 78

Given an integer array nums (unique elements)
Return all possible subsets (the powerset)

💡 Example 
Input : [1, 2, 3]

Output :
[
[],
[1],
[2],
[3],
[1, 2],
[1, 3],
[2, 3],
[1, 2, 3]
]

🧠 Intuition

Each element can be either:

✅ included in the subset, or

❌ excluded from the subset.

That’s 2 choices per element → total 2^n subsets.

We can use backtracking to explore all possibilities.

❇️ Approach Backtracking -DFS

1. Start with an empty list
2. At each step check if the next element can be added to the result
3. Add the current subset list to result, before exploring further

🔁 Recursive Tree for [1,2,3]

Start → []
 ├─ include 1 → [1]
 │   ├─ include 2 → [1,2]
 │   │   ├─ include 3 → [1,2,3]
 │   │   └─ exclude 3 → [1,2]
 │   └─ exclude 2 → [1]
 │       ├─ include 3 → [1,3]
 │       └─ exclude 3 → [1]
 └─ exclude 1 → []
     ├─ include 2 → [2]
     │   ├─ include 3 → [2,3]
     │   └─ exclude 3 → [2]
     └─ exclude 2 → []
         ├─ include 3 → [3]
         └─ exclude 3 → []

All subsets collected along the way

import java.utils.*;

                                class Solution{
                                    public List<List<Integer>> subsets (int [] nums){
                                        List<List<Integer>> result = new ArrayList<>();
                                        backtrack(0, nums, new ArrayList<>(), result);
                                        return result;
                                    }
                                    private void backtrack(int start, int[]nums, List<Integer> current, List<List<Integer>> result){
                                        result.add(new ArrayList<>(current));

                                        //Explore further
                                        for(int i = start; i< nums.length; i++){
                                            current.add(nums[i]);
                                            backtrack(i+1, nums, current, result);
                                            current.remove(current.size() - 1);
                                        }
                                    }
                                }

🧮 Example Execution for [1,2,3]

| Step | Current Subset                         | Action                                   |
| ---- | -------------------------------------- | ---------------------------------------- |
| 1    | []                                     | Add → result = [[]]                      |
| 2    | [1]                                    | Add → result = [[], [1]]                 |
| 3    | [1,2]                                  | Add → result = [[], [1], [1,2]]          |
| 4    | [1,2,3]                                | Add → result = [[], [1], [1,2], [1,2,3]] |
| 5    | Backtrack to [1,3] → Add               |                                          |
| 6    | Backtrack to [2] → Add                 |                                          |
| 7    | Continue ... → finally all 8 subsets ✅ |                                          |

