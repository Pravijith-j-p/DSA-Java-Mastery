Leetcode 981

✅ Problem Summary

You're asked to build a data structure that supports:

1️⃣ set(key, value, timestamp)

Stores value for key with a given timestamp.

2️⃣ get(key, timestamp)

Returns the value for key with the largest timestamp ≤ given timestamp.
If none exists → return "".

✅ Key Insight / Pattern
⏳ 1. Values for each key must be stored in time order

Since timestamps are strictly increasing for the same key, we can store values in a list.

🔍 2. To query, perform binary search

For each key, we binary-search the time list to find:

largest timestamp <= given timestamp


This is classic binary search for floor value.

✅ Data Structure

Use:

HashMap<String, List<Pair<timestamp, value>>>


For Java:

Use Map<String, List<int[], or custom class>>

Or two lists inside a pair.

                                    class TimeMap {

                                        Map<String, List<Pair>> map;

                                        class Pair {
                                            int time;
                                            String value;

                                            Pair(int time, String value) {
                                                this.time = time;
                                                this.value = value;
                                            }
                                        }

                                        public TimeMap() {
                                            map = new HashMap<>();
                                        }

                                        public void set(String key, String value, int timestamp) {
                                            map.putIfAbsent(key, new ArrayList<>());
                                            map.get(key).add(new Pair(timestamp, value));
                                        }

                                        public String get(String key, int timestamp) {
                                            if (!map.containsKey(key)) return "";

                                            List<Pair> list = map.get(key);

                                            int left = 0, right = list.size() - 1;
                                            String result = "";

                                            while (left <= right) {
                                                int mid = left + (right - left) / 2;
                                                if (list.get(mid).time <= timestamp) {
                                                    result = list.get(mid).value;
                                                    left = mid + 1; // try to find a later timestamp
                                                } else {
                                                    right = mid - 1;
                                                }
                                            }

                                            return result;
                                        }
                                    }
Example Walkthrough
set("foo", "bar", 1)

store list:

"foo" → [(1, "bar")]

get("foo", 1) → "bar"
get("foo", 3)

Binary search floor(3) → timestamp 1 → return "bar".

Time Complexity
Operation	Complexity
set	O(1) amortized
get	O(log n) per key
Space	O(N)