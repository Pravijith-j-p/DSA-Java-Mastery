Leetcode 39

Problem : Given an array of distinct candidates and a target integer target, return all unique combinations of candidates where the chosen numbers sum to target

You may use same number from candidates an unlimited number of times
You can return the combinations in any order

Example:

candidates = [2, 3, 6, 7]
target = 7

Output : [[2, 2, 3],[7]]

Explanation : 2 + 2 + 3 = 7
7 = 7

Approach
Backtracking

1. Sort the candidates (optional, helps in pruning)
2. Use a recursive helper function to explore all combinatons
3. At each step:
    - Include the current number if it doesn't exceed the remaining target
    - Recurse the updated target
    - Exclude (backtrack) after exploring the path

import java.utils.*;

                                    class Solution{
                                        public<List<List<Integers>>> combinationSum(int [] candidates, int target){
                                            List<List<Integer>> result = new int ArrayList<>();
                                            backtrack(candidates, target, 0, new ArrayList<>(), result);
                                        }

                                        private void backtrack(int[] candidates, int target, int start, List<Integer> current, List<List<Integer>> result);
                                        if(target == 0){
                                            result.add(new ArrayList<>(current));
                                            return;
                                        }

                                        for(int i = start; i< candidates.length; i++){
                                            if(candidates[i] > target) continue;        // pruning
                                            current.add(candidates[i]);
                                            backtrack(candidates, target - candidates[i], i, current, result);      //not i+1, since we can reuse same number
                                            current.remove(current.size() - 1);     //backtrack
                                        }
                                    }

⏱️ Time Complexity

Worst case: O(2^n) — exponential (since we explore all subsets)

Average case: Faster due to pruning when sum exceeds target.