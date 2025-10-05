Leetcode 150

Problem : You are given an array of strings tokens, representing an arithmetic expression in Reverse Polish Notation(RPN)
Return the integer result of the expression

Valid Operators are +,-,*, and /
Each operand may be an integer or another expression

Example 1 :
Input : tokens = ["2", "1", "+", "3", "*"]
Output : 9
Explanation : ((2+1)*3) = 9

Explanation 2:
Input : tokens = ["4", "13", "5", "/", "+"]
Output : 6
Explanation : (4+(13/5)) = 6

Input : tokens = ["10","6","9","3","+","-11","*","/","*","17","+","5","+"]
Output : 22

🧠 Understanding Reverse Polish Notation

In Reverse Polish Notation(PostFix Expression)

- Operators come after thier operands
- example:
    - infix(2+1)*3
    - postfix(2 1 + 3 *)
- to evaluate it, we need to process operations in the order they appear

💡 Brute Force Approach (Recursive Reduction)

🔸 Idea :
We can simulate the evaluation by finding an operator, replacing it with its evaluated result, and continuing until only one number remains.

🪜 Steps:
1. Traverse the tokens array to find the first operator (+,-,*,/)
2. When found, take the two numbers before it , perform the operation , and replace those three tokens with the result
3. Repeat this until array length becomes one

                    class BruteForceRPN{
                        public int evalRPN(String []tokens){
                            List<String> list = new ArrayList<>(Arrays.asList(tokens));

                            while(list.size()>1){
                                for(int i =0;i<list.size();i++){
                                    String token = list.get(i);

                                    if(isOperator(token)){
                                        int a = Integer.parseInt(list.get(i-2));
                                        int b = Integer.parseInt(list.get(i-2));
                                        int res = 0;

                                        switch(token){
                                            case "+": res = a+b; break;
                                            case "-": res = a-b; break;
                                            case "*": res = a*b; break;
                                            case "/": res = a/b; break;
                                        }

                                        list.set(i-2, String.valueOf(res));
                                        list.remove(i);     //remove operator
                                        list.remove(i-1);   //remove b
                                        break;      //restart scanning from begining
                                    }
                                }
                            }
                            return Integer.parseInt(list.get(0);)
                        }
                        private boolean isOperator(String token){
                            return token.equals("+") || token.equals("-") || token.equals("*") || token.equals("/");
                        }
                    }
Time complexity : O(n^2)
Space complexity : O(n)

✅ Optimized approach - Using stack

Key Idea: 
- Use a stack to keep operands
- When we see a number , push it
- When see an operator -> pop top two, apply operation and push result

import java.utils.Stack;

                        class Solution{
                            public int evalRPN(String []tokens){
                                Stack<Integer> stack = new Stack<>();

                                for(String token: tokens){
                                    if(isOperator(token)){
                                        int b = stack.pop();
                                        int a = stack.pop();
                                        int res = 0;

                                        switch(token){
                                            case "+": res = a+b; break;
                                            case "-": res = a-b; break;
                                            case "*": res = a*b; break;
                                            case "/": res = a/b; break;
                                        }
                                        stack.push(res);
                                    }else{
                                        stack.push(Integer.parseInt(token));
                                    }
                                }
                                return stack.pop();
                            }
                            private boolean isOperator(String token) {
                                return token.equals("+") || token.equals("-")|| token.equals("*") || token.equals("/");
                            }
                        }
Time complexity: O(n)
Space : O(n)


