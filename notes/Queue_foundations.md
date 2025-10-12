A Queue is a linear data structure that follows the FIFO principle - meaning the first element inserted into the queue is the first one to be removed

🧠 Key Characterstics
-  order : elements are processed in the order they arrive (FIFO)
- Access : insertion happens at one end(rear) and deletion happens at the other(front)

Basic Operations

| Operation            | Description                                    | Time Complexity |
| -------------------- | ---------------------------------------------- | --------------- |
| `enqueue(x)`         | Add element `x` to the **rear** of the queue   | O(1)            |
| `dequeue()`          | Remove element from the **front** of the queue | O(1)            |
| `front()` / `peek()` | Get the front element without removing it      | O(1)            |
| `isEmpty()`          | Check if the queue is empty                    | O(1)            |
| `isFull()`           | (For fixed-size queues) Check if it’s full     | O(1)            |

🧩 Implemetation

1. Using Arrays

                            class Queue{
                                int front, rear, size;
                                int capacity;
                                int []arr;

                                Queue(int capacity){
                                    this.capacity = capacity;
                                    front = 0;
                                    rear = -1;
                                    size = 0;
                                    arr = new int [capacity];
                                }

                                void enqueue(int x){
                                    if( size == capacity) return;
                                    rear = (rear + 1) % capacity;
                                    arr[rear] = x;
                                    size++;
                                }

                                int dequeue(){
                                    if(size == 0) return -1;
                                    int item = arr[front];
                                    front = (front + 1) % capacity;
                                    size --;
                                    return item;
                                } 
                            }

2. Using LinkedList

                            class Node{
                                int data;
                                Node next;
                                Node(int data) {this.data = data;}
                            }

                            class Queue{
                                Node front, rear;

                                void enqueue(int x){
                                    Node temp = new Node(x);
                                    if(rear == null){
                                        front = rear = temp;
                                        return;
                                    }
                                    rear.next = temp;
                                    rear = temp;
                                }
                                int dequeue(){
                                    if(front == null) return -1;
                                    int val = front.data;
                                    front = front.next;
                                    if(front == null) rear = null;
                                    return val;
                                }
                            }

🧮 Types of Queues

Simple Queue → FIFO (normal queue)

Circular Queue → Last position connects to the first, forming a circle

Priority Queue → Elements served based on priority, not arrival time

Deque (Double-Ended Queue) → Insert/delete allowed at both ends                        

⚙️ Real-World Applications

Task scheduling (CPU scheduling, print queues)

Breadth-First Search (BFS) in graphs

Buffer management (network packets, IO)

Asynchronous data transfer (e.g., producer-consumer model)