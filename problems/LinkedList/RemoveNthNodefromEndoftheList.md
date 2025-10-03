Leetcode 19

🔹 Problem Statement

Given the head of a linked list, remove the n-th Node from end of the list and return its head

Example 1 :
Input : head = [1,2,3,4,5] , n = 2
Output : [1,2,3,5]

Example 2 :
Input : head = [1], n=1
Output : []


🔸 Brute Force Approach

1. first , find the length of the linkedlist
2. then calculate (length - n) position from begining
3. Delete that node

                        public ListNode removeNthFromEnd(ListNode head, int n){
                            // Step 1 : find the length
                            int length = 0;
                            ListNode temp = head;
                            while(temp != null){
                                length ++;
                                temp = temp.next;
                            }
                            //step 2 : if we need to remove the head
                            if(n == length){
                                return head.next;
                            }
                            //Step 3 : Move to (length - n - 1)th node
                            temp = head;
                            for(int  i =1; i< length - n; i++){
                                temp = temp.next;
                            }
                            //step 4 :remove target node
                            temp.next = temp.next.next;

                            return head;
                        }
Time complexity : O(n)
Space complexity : O(1)

🔹 Optimized Approach (Two Pointers / Fast-Slow)

1. Use a dummy node before head
2. Move fast pointer n + 1 steps ahead
3. Then move fast and slow pointer together until fast reaches null
4. Now slow.next is the node to delete

                        public ListNode removeNthFromEnd(ListNode head, int n){
                            ListNode Dummy = new ListNode(0);
                            dummy.next = head;
                            ListNode fast = dummy, slow = dummy

                            //Move fast ahead by n + 1 steps
                            for(int i=0;i<= n;i++){
                                fast = fast.next
                            }
                            //Move fast and slow until fast reaches null
                            while(fast != null){
                                fast = fast.next;
                                slow = slow.next;
                            }
                            //Remove the nth node
                            slow.next = slow.next.next;

                            return dummy.next;
                        }

Time Complexity: O(N) (one pass ✅)
Space Complexity: O(1)