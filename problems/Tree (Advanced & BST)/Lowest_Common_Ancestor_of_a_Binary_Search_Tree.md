Leetcode 235

Problem : Given a Binary Search Tree and two nodes p and q , find their lowest common ancestor (LCA)- the lowest node that has both p and q as descendants (a node can be a descendant of itself)

Input : 
root = [6, 2, 8, 0, 4, 7, 9, null, null, 3, 5]
p= 2
q = 8

Output : 6

🔵 Brute Force Approach

Idea : 
- Find path from root->p
- find path from root->q
- Compare paths to find the last common node

                                class Solution{
                                    public TreeNode lowestCommonAncestor(TreeNode root, TreeNode p, TreeNode q){
                                        List<TreeNode> path1 = new ArrayList<>();
                                        List<TreeNode> path2 = new ArrayList<>();

                                        getPath(root, p, path1);
                                        getPath(root, q, path2);

                                        int i = 0;
                                        TreeNode lca = null;
                                        while(i< path1.size() && i<path2.size()){
                                            if(path.get(i) == oath2.get(i)){
                                                lca = path1.get(i);
                                            }else break;
                                            i++;
                                        }
                                        return lca;
                                    }
                                    private boolean getPath(TreeNode root, TreeNode target, List<TreeNode> path){
                                        if(root == null) return false;
                                        path.add(root);
                                        if(root == target) retur true;
                                        if(getPath(root.left, target, path)|| getPath(root.right, target, path)) return true;
                                        path.remove(path.size() - 1);
                                        return false;
                                    }
                                }

Time complexity : O(n)
Space complexity : O(h)

✅ Optimized approach (Using BST Property)

Idea :
Since it's a binary searct tree we can leverage its property

- if p.val and q.val are less than root.val, go left.
- if p.val and q.val are greater than root.val go right
- Otherwise  current root = lca

                                class Solution{
                                    public TreeNode lowestCommonAncestor(TreeNode root, TreeNode p, TreeNode q){
                                        while( root != null){
                                            if(p.val < root.val && q.val < root.val){
                                                root = root.left;
                                            } else if(p.val > root.val && q.val > root.val){
                                                root = root.right;
                                            }else{
                                                return root;
                                            }
                                        }
                                        return null;
                                    }
                                }
Time complexity : O(h) - h is height of tree
Space complexity : O(1)

🧭 Pattern / Key Idea
Binary Search Tree Traversal + Value Comparison

