Leetcode 230

Problem : 
Given the root of a binary search tree, and an integer k,
return the kth smallest value (1-indexed) among all the values of the nodes in the tree.

Since BST's inorder traversal gives values in sorted (ascending) order,
we can leverage that directly

Example : 
Input : root = [3, 1, 4, null, 2] k = 1

Output : 1

🔵 Brute Force Approach - Inorder Traversal with List

Idea:
- Perform inorder traversal -> collect all node values into a list(sorted order)
- return the k-th element of that list

                                class Solution{
                                    public int kthSmallest(TreeNode root, int k){
                                        List<Integer> inorder = new ArrayList<>();
                                        inorderTraversal(root, inorder);
                                        return inorder.get(k-1);
                                    }
                                    private void inorderTraversal(TreeNode root, List<Integer> inorder){
                                        if(root == null) return;
                                        inorderTraversal(root.left, inorder);
                                        inorder.add(root.val);
                                        inorderTraversal(root.right, inorder);
                                    }
                                }
Time complexity :   O(n)
Space complexity  :O(n)

✅ Optimized Solution
Inorder traversal with Counter(No List)

Idea:
- instead of storing all elements,
keep a counter and stop when you reach the k th element during inorder traversal
- this use less memmory and improve runtime

                                class Solution{
                                    public int kthSmallest(TreeNode root){
                                        inorder(root, k);
                                        return result;
                                    }
                                    privare void inorder(TreeNode root, int k){
                                        if(root == null) return;

                                        inorder(root.left, k);
                                        count++;
                                        if(count == k){
                                            result = root.val;
                                            return;
                                        }
                                        inorder(root.right, k);
                                    }
                                }
Time complexity : O(h+k)
Space complexity : O(h)

🧭 Pattern / Key Idea

Inorder Traversal + Early Stop / Counter Pattern

Useful for ordered operations on BSTs (like kth smallest/largest).
