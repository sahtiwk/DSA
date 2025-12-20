# Jump Game II (LeetCode 45)

## 🧩 Problem Statement

You are given a **0-indexed integer array** `nums` of length `n`.

* You start at index `0`
* Each `nums[i]` represents the **maximum jump length** from index `i`
* You can jump to any index `i + j` such that:

  * `0 <= j <= nums[i]`
  * `i + j < n`

🔹 It is guaranteed that you can reach index `n - 1`.

### Goal

Return the **minimum number of jumps** required to reach the last index.

---

## 💡 Greedy Approach (Optimal)

### Key Insight

Instead of deciding **where exactly to jump**, we focus on:

> **How far can we reach using a fixed number of jumps?**

All indices reachable within the same jump count are equivalent in cost, so the best choice is always the one that extends our reach the farthest.

---

## 🚀 Greedy Strategy

We maintain three variables:

| Variable   | Meaning                                               |
| ---------- | ----------------------------------------------------- |
| `jumps`    | Number of jumps taken so far                          |
| `currEnd`  | Farthest index reachable with current number of jumps |
| `farthest` | Farthest index reachable with one more jump           |

### Algorithm

1. Traverse the array from left to right (except the last index)
2. Update `farthest = max(farthest, i + nums[i])`
3. When we reach `currEnd`, we **must take a jump**:

   * Increment `jumps`
   * Update `currEnd = farthest`

---

## ✅ C++ Implementation

```cpp
class Solution {
public:
    int jump(vector<int>& nums) {
        int jumps = 0;
        int currEnd = 0;
        int farthest = 0;

        for (int i = 0; i < nums.size() - 1; i++) {
            farthest = max(farthest, i + nums[i]);

            if (i == currEnd) {
                jumps++;
                currEnd = farthest;
            }
        }
        return jumps;
    }
};
```

---

## 🧪 Example Walkthrough

### Input

```
nums = [2,3,1,1,4]
```

### Steps

* Jump 0 → reach indices `[0…2]`
* From indices `[0…2]`, farthest reach is index `4`
* Jump 1 → reach last index

✅ Output: `2`

---

## ⏱️ Complexity Analysis

* **Time Complexity:** `O(n)`
* **Space Complexity:** `O(1)`

---

## 🧠 Why Greedy Works (One-liner)

> Since all indices reachable within the same jump have equal cost, choosing the one that extends the farthest reach always preserves optimality.

---

## 📌 Notes

* This problem is equivalent to a **level-order BFS traversal** where each jump represents one level.
* The greedy solution efficiently simulates this without using extra space.

---

⭐ If you found this helpful, feel free to star the repository!
