Leetcode 40

Problem :
Given a collection of integers candidates (may contain duplicates) and a target integer target,
return all unique combination where the chosen numbers sum to target 
Each number in candidates may only be used once in the combination

Example : 
candidates = [10, 1, 2, 7, 6, 1, 5]
target = 8

[
    [1, 1, 6],
    [1, 2, 5],
    [1, 7],
    [2, 6]
]

⚙️ Key Idea
This problem is a mix of Combination Sum I and Subsets II 

🧠 Approach - Backtracking + Duplicate Handling
1. Sort the array to handle duplicates
2. Use backtracking to explore possible combinations
3. Skip duplicate elements at the same recursion level(if (i> start && candidates[i] == candidates[i - 1]) continue;)
4. Stop exploring when the current number exceeds the remaining target

                    import java.util.*;

                    class Solution {
                        public List<List<Integer>> combinationSum2(int[] candidates, int target) {
                            List<List<Integer>> result = new ArrayList<>();
                            Arrays.sort(candidates); // step 1: sort to handle duplicates
                            backtrack(candidates, target, 0, new ArrayList<>(), result);
                            return result;
                        }

                        private void backtrack(int[] candidates, int target, int start, List<Integer> current, List<List<Integer>> result) {
                            if (target == 0) {
                                result.add(new ArrayList<>(current));
                                return;
                            }

                            for (int i = start; i < candidates.length; i++) {
                                // skip duplicate numbers in same recursive level
                                if (i > start && candidates[i] == candidates[i - 1]) continue;

                                if (candidates[i] > target) break; // pruning

                                current.add(candidates[i]);
                                backtrack(candidates, target - candidates[i], i + 1, current, result); // move to next index (no reuse)
                                current.remove(current.size() - 1); // backtrack
                            }
                        }
                    }

⏱️ Complexity

Time: O(2^n) (explores all subsets, but pruned by target)

Space: O(n) for recursion stack