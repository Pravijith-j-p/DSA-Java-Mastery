Leetcode 17

Given a string containing digits from 2-9 inclusive, return all possible letter combinations that the number could represent. Return the answer in any order.

A mapping of digits to letters (just like on the telephone buttons) is given below. Note that 1 does not map to any letters.

Example :
Input : digits = "23"
Output : 
["ad", "ae", "af", "bd", "be", "bf", "cd", "ce", "cf"]

🧭 Mapping of digits to letters

| Digit | Letters    |
| ----- | ---------- |
| 2     | a, b, c    |
| 3     | d, e, f    |
| 4     | g, h, i    |
| 5     | j, k, l    |
| 6     | m, n, o    |
| 7     | p, q, r, s |
| 8     | t, u, v    |
| 9     | w, x, y, z |

🧠 Key Idea

Use backtracking to build combinations:

Each digit can represent several letters.

Recursively build strings by choosing one letter from each digit.

🧩 Approach (Backtracking)

Steps:

- If the input digits is empty, return an empty list.

- Use a hashmap for digit-to-letters mapping.

- Define a recursive function backtrack(index, path):

    - If path length == digits length → add path to the result.

    - Otherwise, iterate through each letter mapped to digits[index], and recursively call backtrack(index+1, path + letter).

                        import java.util.*;

                        public class LetterCombinations {
                            public List<String> letterCombinations(String digits) {
                                List<String> result = new ArrayList<>();
                                if (digits == null || digits.length() == 0) return result;

                                Map<Character, String> map = new HashMap<>();
                                map.put('2', "abc");
                                map.put('3', "def");
                                map.put('4', "ghi");
                                map.put('5', "jkl");
                                map.put('6', "mno");
                                map.put('7', "pqrs");
                                map.put('8', "tuv");
                                map.put('9', "wxyz");

                                backtrack(result, map, digits, 0, new StringBuilder());
                                return result;
                            }

                            private void backtrack(List<String> result, Map<Character, String> map,
                                                String digits, int index, StringBuilder path) {
                                if (path.length() == digits.length()) {
                                    result.add(path.toString());
                                    return;
                                }

                                String letters = map.get(digits.charAt(index));
                                for (char c : letters.toCharArray()) {
                                    path.append(c);
                                    backtrack(result, map, digits, index + 1, path);
                                    path.deleteCharAt(path.length() - 1);
                                }
                            }

                            public static void main(String[] args) {
                                LetterCombinations lc = new LetterCombinations();
                                System.out.println(lc.letterCombinations("23"));
                            }
                        }

🧮 Complexity Analysis

Time Complexity: O(3ⁿ × 4ᵐ)
(where n = number of digits mapping to 3 letters, m = number of digits mapping to 4 letters)

Space Complexity: O(N) — recursion depth and output storage

