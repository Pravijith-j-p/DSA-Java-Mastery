Leetcode 155

Problem : Design a stack that supports the following operations

- push()
- pop()
- top()
- getMin()

All must run on O(1) time

🔹 Brute Force MinStack

Example : Stack = [5, 3, 7, 2]

top() -> 2
pop() -> removes 2
getMin() -> scan [5, 3, 7] ->3

                        class Minstack {
                            private Stack<Integer> stack;

                            public MinStack(){
                                stack = new Stack<>();
                            }

                            public void push(int val){
                                stack.push(val);
                            }

                            public void pop(){
                                stack.pop();
                            }

                            public int top(){
                                return stack.peek();
                            }

                            //Brute force: scan the stack to find min
                            public int getMin(){
                                int min = Integer.MAX_VALUE;
                                for(int num :stack) {
                                    min = Math.min(min, num);
                                }
                                return min;
                            }
                        }

✅ Optimal Solution:

We maintain to stacks:
1. main stack -> stores all the elements
2. min stack -> stores the minimum values at each step

Example : 
push(5) -> main: [5], min:[5]
push(3) -> main: [5, 3], min :[5, 3]
push(7) -> main: [5, 3, 7], min : [5, 3]        //7 greater , so again push 3 to stack
push(2) -> main: [5, 3, 7, 2], min :[5, 3, 3, 2]
pop() -> main: [5, 3, 7], min: [5, 3, 3]
getMin() -> 3

                            class MinStack{
                                private Stack<Integer> mainStack;
                                private Stack<Integer> minStack;

                                public MinStack(){
                                    mainStack = new Stack<>();
                                    minStack = new Stack<>();
                                }

                                public void push(int val){
                                    mainStack.push(val);

                                    if(minStack.isEmpty()){
                                        minStack.push(val);
                                    }else{
                                        minStack.push(Math.min(val, minStack.peek()));
                                    }
                                }

                                public void pop(){
                                    mainStack.pop();
                                    minStack.pop();
                                }
                                public int top(){
                                    return mainStack.peek();
                                }
                                public int getMin(){
                                    return minStack.peek();
                                }
                            }

