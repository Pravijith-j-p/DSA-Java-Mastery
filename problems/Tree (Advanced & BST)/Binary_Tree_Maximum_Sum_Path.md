LeetCode 124

Problem :
Given a non-empty binary tree, find the path with the maximum sum.
A path can start and end at any node, but it must go downward(parent->child) or turn at a node - you can't revisit nodes

Input: [1, 2, 3]
Output = 6 
Explanation : The path [2->1->3] gives sum = 6

Input : [-10, 9, 20, null, null, 15, 7]
Output : 42
Explanation : The path [15->20->7] gives sum = 42

Brute Force (Exponential - Not Practical)
Idea : 
Try every possible path, compute it's sum, and keep track of the max
- for each node, find all paths passing through it
- Time complexity : O(n^2) or worse(because repeated traversal)

                                    class Solution{
                                        int max = Integer.MIN_VALUE;

                                        public int maxPathSum(TreeNode root){
                                            if(root == null) return 0;
                                            helper(root);
                                            return max;
                                        }
                                        private int helper(TreeNode root){
                                            if(root == null) return 0;

                                            int left = Math.max(0, helper(root.left));
                                            int right = Math.max(0, helper(root.right));
                                            int pathThroughRoot = root.val + left + right;

                                            max = Math.max(max, pathThroughRoot);
                                            return root.val + Math.max(left, right);
                                        }
                                    }

✅ Optimized Approach (DFS)

PostOrder DFS + Track Max Gain

Idea : 
For each node 
1. Compute the maximum gain from its left and right subtrees(ignore negative sums)
2. The max path that passes through the node is:
leftGain + rightGain + node.val
3. Update a global maximum for the best path seen so far
4. Return to parent only one side (since path cannot branch upwards)

                                class Solution{
                                    int maxSum = Integer.MIN_VALUE;

                                    public int maxPathSum(TreeNode root){
                                        dfs(root);
                                        return maxSum;
                                    } 
                                    private int dfs(TreeNode node){
                                        if(node == null) return 0;

                                        int left = Math.max(0, dfs(node.left));
                                        int right = Math.max(0,dfs(node.right));

                                        int currentPathSum = node.val + left +right;

                                        maxSum = Math.max(maxSum, currentPathSum);

                                        return node.val + Math.max(left, right);
                                    }
                                }

🧭 Pattern Recap
Concept	Explanation
Type	DFS + Recursion
Key Action	Compute max path through each node
