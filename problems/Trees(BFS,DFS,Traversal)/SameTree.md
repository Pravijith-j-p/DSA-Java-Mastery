Leetcode 100

Problem : given the roots of two binary trees p and q , write a function to check if they are the same or not
Two binary trees are considerd the same if they are structurally identical, and the nodes have the same values

                                    Input : 

                                    p=   1                q =     1
                                        / \                      /\
                                        2   3                    2  3

                                    Output : True

                                    Input : p=        1          1
                                                    /             \
                                                   2                2

                                    Output : false

🔵 Brute Force 
Idea : 
use recursion to compare both trees
- if both nodes are null -> same
- if one is null or values differ -> not same
- recursively compare both left and right trees

                            class Solution{
                                public boolean isSameTree(TreeNode p, Treenode q){
                                    if(p == null && q ==null) return true;
                                    if(p == null && q ==null) return false;
                                    if(p.val != q.val) return false;
                                    return isSameTree(p.left, q.left) && isSameTree(p.right, q.right);
                                }
                            }
Time Complexity : O(n)
Space complexity : O(H) -> height of the tree

❇️ Iterative Approach (Using Queue)

                            class Solution{
                                public boolean isSameTree(TreeNode p, TreeNode q){
                                    Queue<TreeNode> queue = new LinkedList<>();
                                    queue.add(p);
                                    queue.add(q);

                                    while(!queue.isEmpty()){
                                        TreeNode first = queue.poll();
                                        TreeNode second = queue.poll();

                                        if(first == null && second == null) continue;
                                        if(first ==null || second ==null) return false;
                                        if(first.val != second.val) return false;

                                        queue.add(first.left);
                                        queue.add(second.left);
                                        queue.add(first.left);
                                        queue.add(second.right);
                                    }
                                    return true;
                                }
                            }
