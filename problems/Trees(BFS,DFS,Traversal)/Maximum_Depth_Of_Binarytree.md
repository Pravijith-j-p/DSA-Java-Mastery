Leetcode 104

Problem :
Given the root of a Binary tree, return its maximum depth - the number of nodes along the longest path from the root down to the farthest leaf node

Example : 

Input :                         3
                              /   \
                            9     20
                                  /\
                                15  7

Output : 3

Brute Force Approach
Idea : Recursively explore all paths and track the depth manually

Code :

                            class Solution {
                                public int maxDepth(TreeNode root){
                                    if(root == null) return 0;
                                    return 1 + Math.max(maxDepth(root.left), maxDepth)
                                }
                            }

⚡ Optimized Approach (same logic, clean form)

The above recursive approach is already optimal since every node is visted exctaly once.
Alternatively, you can use BFS (level order traversal) to compute depth iteratively

                            class Solution{
                                public int maxDepth(TreeNode root){
                                    if(root == null) return 0;
                                    Queue<TreeNode> queue = new LinkedList<>();
                                    queue.add(root);
                                    int depth = 0;

                                    while(!queue.isEmpty()){
                                        int size = queue.size();
                                        for(int i=o;i<size;i++){
                                            TreeNode node = queue.poll();
                                            if(node.left != null) queue.add(node.left);
                                            if(node.right != null) queue.add(node.right);
                                        }
                                        depth ++;
                                    }
                                    return depth;
                                }
                            }
Time complexity : O(n)
Space complexity : O(n)