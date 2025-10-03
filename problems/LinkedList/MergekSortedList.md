Leetcode 23

Problem :  given an array of k linkedlists, each list is sorted in ascending order. Merge all the linkedlists into one sorted list and return it

Example :
Input : [[1->4->5], [1->3->4],[2->6]]
Output : 1->1->2->3->4->4->5->6

Brute Force:
- put all elements of list to an array
- sort the array
- build a new linkedlist from it

Time Complexity : O(nlogn)
Space complexity : O(n)

                        public ListNode mergekLists(ListNode [] lists){
                            List<Integer> values = new ArrayList<>();

                            for(ListNode node : lists){
                                while(node != null){
                                    values.add(node.val);
                                    node = node.next;
                                }
                            }
                            if( values.isEmpty()) return null;

                            Collections.sort(values);

                            ListNode dummy = new ListNode(-1);
                            ListNode curr = dummy;
                            for(int val : values){
                                curr.next = new ListNode(val);
                                curr = curr.next;
                            }
                            return dummy.next;
                        }
🔵 Optimized approach

Pairwise Merge (Divide and conquer)

- Reuse the mergeTwoList function
- Repeateadly merge lists two at a time until only one remains
- This is similar to how merge sort works

Time complexity : O(n logk) -> k number of lists, n -> number of nodes
Space Complexity : O(1)

                    public ListNode mergeKSorted(ListNode [] lists){
                        if(lists == null || lists.length == 0) return null;
                        return mergeKListsHelper(lists, 0, lists.length - 1);
                    }
                        public ListNode mergeKListsHelper(ListNode[] lists,int left, int right){
                            if(left == right) return lists[left];
                            int mid = left + (right -left) / 2;
                            ListNode l1 = mergeKListsHelper(lists, left, mid);
                            ListNode l2 = mergeKListsHelper(lists, mid+1, right);

                            return mergeTwoLists(l1, l2);
                        }
                        public ListNode mergeTwoLists(ListNode l1, ListNode l2){
                            ListNode dummy = new ListNode(-1), tail = dummy;
                            while(l1 != null && l2 != null){
                                if(l1.v1l < l2.val){
                                    tail.next = l1;
                                    l1 = l1.next;
                                }
                                tail = taile.next;
                            }
                            taile.next = (l1 != null) ? l1 : l2;
                            return dummy.next;
                        }

3. Use a MinHeap (Priority Queue) -> Most efficient

- insert the head of each list into a min-heap (priority queue)
- repeatedly extract the smallest element, add its next node to the heap
- build the merged list

Time Complexity : O(n logk)
Space complexity : O(k)

                        public ListNode mergeKlists(ListNode [] lists){
                            PriorityQueue<ListNode> pq = new PriorityQueue<>((a,b) -> a.val - b.val);

                            // Add the head of each list into the heap
                            for(ListNode node : lists){
                                if(node != null)pq.offer(node);
                            }
                            ListNode dummy = new ListNode(-1), tail = dummy;

                            while(!pq.isEmpty()){
                                ListNode min = pq.poll();
                                tail.next = min;
                                tail = tail.next;
                                if(min.next != null) pq.offer(min.next);
                            }
                            return dummy.next;
                        }




