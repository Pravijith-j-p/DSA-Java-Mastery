Leetcode 271

Problem : Design an algorithm to encode a list of strings to a single string, and decode it back to the original list of strings

⚠️ The challenge is handling strings that might contain spaces, commas, or special characters (so we can’t just join by a delimiter).

Example 1:
Input : ["lint", "code", "love", "you"]
Output : 
- Encoded : 4#lint4#code4#love3#you
- Decoded : ["lint", "code", "love", "you"]

🔹 Approach

👉 We need a lossless encoding scheme.

Prefix each string with its length + special delimiter (#).

While decoding, read length first, then extract the substring of that length.

🔹 Brute Force Idea
- try using a simple delimeter like "|" and split
- Problem : what if a string itself contains "|" ?(fails)

🔹 Optimized Approach ✅ (Length Prefixing)

Encode :
"lint" -> "4#lint"
"code" -> "4#code"

Final Encoding string
"4#lint4#code4#love3#you"

Decode 
- Read number until # -> gives length
- Extract next length characters
- Repeat

                    public String encode(List<String> strs){
                        StringBuilder sb = new StringBuilder ();
                        for(Strings s : strs){
                            sb.append(s.length().append('#').append(s));
                        }
                        return sb.toString();
                    }

                    public List<String> decode(String strs){
                        List<String> result = new ArrayList <>();

                        int i = 0;
                        while(i< s.length()){
                            int j = i;
                            while(s.charAt(j)!='#'){
                                j++;
                            }
                            int length = Integer.parseInt(s.substring(i, j));
                            i = j +1; //skip '#'
                            result.add(s.substring(i, i+length));
                            i += length;
                        }
                        return result;
                    }

🔹 Complexity

Time Complexity: O(n) for both encode and decode (N = total length of strings).

Space Complexity: O(n).                 