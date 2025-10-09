Leetcode 105

Problem : 
Given two integer arrays preorder and inorder representing the preorder and inorder traversal of a binary tree, construct the binary tree and return its root

Example : 
Input : preorder = [3, 9, 20, 15, 7]
        inorder = [9, 3, 15, 20, 7]

        Output :                3
                               / \
                              9  20
                                /  \
                               15   7
Understanding the idea :
🔵 Preorder traversal -> [Root->Left->Right]
so the first element of preorder is always the root

🔵 Inorder traversal -> [Left->Root->Right]
so the position of root in inorder tells us:
- all elements to the left of root-> left subtree
- all elements to the right of root-> right subtree
We recursively apply this pattern

🔸 Brute Force Approach
Idea:
at each recursive step:
- take the first element of preorder as root
- find the elements index in order(linear search)
- build left and right subtrees recursively

                            class Solution{
                                public Treenode buildTree(int []preorder, int[]inorder){
                                    return helper(preorder, inorder, 0, 0, inorder.length - 1);
                                }
                                private TreeNode helper(int[]preorder, int[]inorder, int preStart, int inStart, int inEnd){
                                    if(prestart > preorder.length- 1 || inStart > inEnd) return null;

                                    TreeNode root = new TreeNode(preorder[preStart]);
                                    int inIndex = 0;

                                    //find index of root in inorder (o(n))
                                    for(int i = inStart;i<=inEnd;i++){
                                        if(inorder[i]==root.val){
                                            inIndex = i;
                                            break;
                                        }
                                    }
                                    root.left = helper(preorder, inorder, preStart + 1, inStart, inIndex - 1);
                                    root.right = helper(preorder, inorder, preStart + (inIndex - inStart)+1, inIndex + 1, inEnd);
                                    return root;
                                }
                            }
Time complexity : O(n^2)

✅ Optimized Approach

Idea:
 Use a HashMap to store each value's index in inorder, so we can get in O(1).

 Steps:
 1. Use preIndex to track current root in preorder
 2. Lookup the root position from inorder using HashMap
 3. Recursively build left and right subtrees



                                        class Solution{
                                            int preIndex = 0;
                                            Map<Integer, Integer> inorderMap = new HashMap<>();

                                            public TreeNode buildTree(int[] preorder, int[]inorder){
                                                //store value -> index of inorder
                                                for(int i=0;i<inorder.length;i++){
                                                    inorderMap.put(inorder[i], i);
                                                }
                                                return build(preorder, 0, inorder.length - 1);
                                            }
                                            private TreeNode build(int[]preorder, int inStart, int inEnd){
                                                if(inStart > inEnd) return null;

                                                int rootVal = preorder[preIndex++];
                                                TreeNode root = new TreeNode(rootVal);

                                                int inIndex = inorderMap.get(rootVal);

                                                root.left = build(preorder, inStart, inIndex-1);
                                                root.right = build(preorder, inIndex+1, inEnd);

                                                return root;
                                            }
                                        }
Time complexity : O(n)
Space Complexity : O(n)

