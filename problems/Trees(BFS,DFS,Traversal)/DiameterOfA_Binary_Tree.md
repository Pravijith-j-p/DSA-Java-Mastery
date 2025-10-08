LeetCode 543

Problem : Given the root of a binary tree , return the length of the diameter of the tree
The diameter of a binary tree is the length of the longest path between any two nodes in the tree
This path may or may not pass through the root

Example: 
Input : 
                                1
                               / \
                              2   3  
                             /\
                            4  5

Output : 3

Explanation : 
The longest path is [4->2->1->3] or [5->2->1->3]

Path length = 3 edges

Intution :
For every node, the longest path passing through it is:

left subtree height + right subtree height

We compute this at every node and keep track of the maximum value

To do this efficiently, we use DFS(Depth First Search) recursion to compute the height while updating a global diameter

🔵 Brute Force Approach

Idea💡 :
For each node
1. Compute left height
2. Compute right height
3. Update diameter = max(diameter, left+right).

Since hieght is recomputed for every node , it leads to O(n^2)

                                class Solution{
                                    public int diameterOfBinaryTree(TreeNode root){
                                        if (root == null) return 0;
                                        int left = height(root.left);
                                        int right = height(root.right);
                                        int diameterThroughRoot = left + right;
                                        int leftDiameter = diameterOfBinaryTree(root.left);
                                        int rightDiameter = diameterOfBinaryTree(root.right);
                                        return Math.max(diameterThroughRoot, Math.max(leftDiameter, rightDiameter));
                                    }
                                    private int height(TreeNode node){
                                        if(node == null) return 0;
                                        return 1 + Math.max(height(node.left), height(node.right));
                                    }
                                }

🧠 Optimized Approach

We compute height and diameter in one DFS traversal

                                class Solution{
                                    int diameter = 0;

                                    public int diameterOfBinaryTree(TreeNode root){
                                        height(root);
                                        return diameter;
                                    }
                                    private int height(TreeNode node){
                                        if(node == null) return 0;

                                        int leftHeight = height(node.left);
                                        int rightHeight = height(node.right);

                                        //Update diameter
                                        diameter = Math.max(diameter, leftHeight+rightHeight);

                                        //Return height
                                        return 1 + Math.max(leftHeight, rightHeight);
                                    }
                                }
Time complexity : O(n)
Space complexity : O(n)

🧩 Pattern / Key Idea

Pattern: Post-order DFS (bottom-up)

Key Idea: Height computation + global diameter update