LeetCode 20

Problem : Given a string s containing just the characters '(', ')', '{', '}', '[', ']', determine if the input string is valid.

A string is valid if :
- Open brackets are closed by the same type of brackets
- Open brackets are closed in the correct order

Example : 
Input : s = "() [] {}"
Output : true

Example:
Input : s = "(]"
Output : false

🔹 Brute Force Approach (Replace pairs until empty)

                    public boolean isValid(String s){
                        while (s.contains("()") || s.contains("{}") || s.contains("[]")){
                            s = s.replace("()", "")
                                s.replace("{}", "")
                                s.replace("[]", "");
                        }
                        return s.isEmpty();
                    }

- keep moving valid pairs until no more exist
- if string becomes empty -> valid
Time complexity : O(n^2)

.

🔹 Optimized Approach (Using Stack)

                        public boolean(String s){
                            Stack<Charcter> stack = new Stack<>();
                            for(char c : s.tocharArray()){
                                if(c == '(') stack.push(')');
                                else if(c == '{') stack.push('}');
                                else if(c == '[') stack.push(']');
                                else{
                                    if(stack.isEmpty() || stack.pop != c) return false;
                                }
                            }
                            return stack.isEmpty();
                        }

Key Idea / Pattern:

Use a stack to push expected closing brackets.

When a closing bracket appears, check if it matches top of stack.

At end, stack must be empty.
Time Complexity: O(n)
Space Complexity: O(n)