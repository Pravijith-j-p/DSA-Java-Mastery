Leetcode 98

Problem : 
Given a binary tree, determine if it is a valid Binary Search Tree(BST)
A valis BST id defined as  
- For every node
    - all nodes in its left subtree have values less than the node's value
    - all nodes in its right subtree have values greater than the node's value

Example :
Input : root = [2, 1, 3]

Output : true

Example : root = [5, 1, 4, null, null, 3, 6]

false
Explanation : Node 4 has left child 3 and right child 6
but node 5 has right child 4 , which violates the BST rule

🔵 Brute force approach
Idea : 
- Perform inorder traversal of the tree (which should give ascending values for a valid BST)
- Store values in a list
- Check if the list is strictly increasing

                                class Solution {
                                    public boolean isValidBST(TreeNode root){
                                        List<Integer> inorder = new ArrayList<>();
                                        inorderTraversal(root, inorder);

                                        for(int i=1;i< inorder.size();i++){
                                            if(inorder.get(i) <= inorder.get(i - 1)) return false;
                                        }
                                        return true;
                                    }

                                    private void inorderTraversal(TreeNode node, List<Integer> inorder){
                                        if(root == null) return;
                                        inorderTraversal(root.left, inorder);
                                        inorder.add(root.val);
                                        inorderTraversal(root.right, inorder);
                                    }
                                }
Time Complexity : O(n)
Space Complexity : O(n)

✅ Optimized approach - DFS with value range

                                class Solution{
                                    public boolean isValidBST(TreeNode root){
                                        return validate(root, Long.MIN_VALUE, Long.MAX_VALUE);
                                    }
                                    private boolean validate(TreeNode node, long min, long max){
                                        if(node == null) return true;
                                        if(node.val <= min || node.val >= max) return false;
                                        return validate(node.left, min, node.val) && validate(node.right, node.val, max);
                                    }
                                }
Time complexity :  O(n)
Space complexity : O(h)

🧭 Pattern / Key Idea

DFS + Range Validation (Min/Max Bound Check)
This is one of the most important tree-based recursion patterns.


