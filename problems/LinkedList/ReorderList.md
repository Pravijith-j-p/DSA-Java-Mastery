LeetCode 143

Problem : Given the head of a singly linked list:

L0->L1->L2->....->Ln

Reorder this to :

 L0->Ln->L1->Ln-1->...

You must do this in-place without altering the values

Example : 
Input : 1->2->3->4->5
Output : 1->5->2->4->3

🔹 Brute Force

- put all nodes into an arrayList
- use two pointers (front , back) and rebuild the list
- Time: O(n)
- space : O(n)

                        public void reorderList(ListNode head){
                            if(head == null) return;

                            List<ListNode> nodes = new ArrayList<>();
                            ListNode curr = head;
                            while(curr != null){
                                nodes.add(curr);
                                curr = curr.next;
                            }

                            int i = 0,j = nodes.size() - 1;
                            while( i<j){
                                nodes.get(i).next = nodes.gest(j);
                                i++;
                                if( i==j) break;
                                nodes.get(j).next = nodes.get(i);
                                j--;
                            }
                            nodes.get(i).next = null;
                        }

🔹 Optimized
Steps:
1. find the middle of the linkedlist (slow/fast pointer)
2. Reverse the second half of the list
3. Merge two halves

Time : O(n)
Space : O(1)

                        public void reorderList(ListNode head){
                            if(head == null || head.next == null) return;

                            //Step 1 find the middle
                            ListNode slow = head, fast = head;
                            while (fast != null && fast.next != null){
                                slow = slow.next;
                                fast = fast.next.next;
                            }
                            //Step 2 :Reverse second half
                            ListNode prev = null, curr = slow.next;
                            slow.next = null;
                            while(curr != null){
                                ListNode nextTemp = curr.next;
                                curr.next = prev;
                                prev = curr;
                                curr = nextTemp;
                            }

                            //Step 3 Merge two halves
                            ListNode first = head, second = prev;
                            while(second != null){
                                ListNode temp1 = first.next;
                                ListNode temp2 = second.next;

                                first.next = second;
                                second.next = temp1;

                                first =temp1;
                                second = temp2;
                            }
                        }
