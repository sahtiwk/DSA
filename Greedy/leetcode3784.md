# 🧹 Minimum Deletion Cost to Make String Consist of Equal Characters

## 📌 Problem Overview

You are given:

* A string **`s`** of length `n`
* An integer array **`cost`** of the same length, where `cost[i]` represents the cost of deleting the `i`-th character of `s`

You may delete **any number of characters (possibly none)** such that:

* The resulting string is **non-empty**
* All remaining characters in the string are **equal**

Your task is to return the **minimum total deletion cost** required to achieve this.

---

## ✨ Examples

### Example 1

**Input:**
`s = "aabaac"`
`cost = [1,2,3,4,1,10]`

**Explanation:**
If we keep only `'c'`, we must delete all other characters.

Total deletion cost:

```
1 + 2 + 3 + 4 + 1 = 11
```

**Output:** `11`

---

### Example 2

**Input:**
`s = "abc"`
`cost = [10,5,8]`

**Explanation:**
Keeping `'a'` and deleting `'b'` and `'c'` gives:

```
5 + 8 = 13
```

**Output:** `13`

---

### Example 3

**Input:**
`s = "zzzzz"`
`cost = [67,67,67,67,67]`

**Explanation:**
All characters are already equal, so no deletions are required.

**Output:** `0`

---

## 🧠 Thought Process & Ideology

This problem is best solved by **reframing the goal**:

> Instead of deciding *which characters to delete*, decide **which character to keep**.

Once we choose a character to keep, **all other characters must be deleted**.

---

### 1️⃣ Key Observation

If we decide to keep only a specific character (say `'a'`):

* All characters that are **not `'a'`** must be deleted
* The cost is the **sum of deletion costs of all other characters**

So the problem reduces to:

> For each character from `'a'` to `'z'`, compute the cost of deleting everything **except** that character, and take the minimum.

---

### 2️⃣ Total Cost Strategy

Let:

* `total` = sum of all deletion costs
* `cs[i]` = total cost of all occurrences of character `(char)(i + 'a')`

If we keep character `i`, then:

```
Deletion cost = total - cs[i]
```

This turns a complex deletion problem into a **simple minimization problem**.

---

### 3️⃣ Efficient Use of Constraints

* Only **26 lowercase English letters** exist
* We can safely store cumulative costs in a fixed-size array
* This ensures excellent performance even for `n = 10^5`

---

### 4️⃣ Why This Approach Is Optimal

* Avoids brute-force deletion simulations
* No nested loops over the string
* Uses a **single pass** to compute totals
* Clean, readable, and interview-friendly logic

---

## 🧩 Algorithm Explanation

1. Initialize `total` as the sum of all deletion costs
2. Create an array `cs[26]` to store total cost per character
3. Traverse the string:

   * Add each cost to `total`
   * Add cost to corresponding character bucket in `cs`
4. For each character:

   * If it exists, compute `total - cs[i]`
   * Track the minimum value
5. Return the minimum deletion cost

---

## 💻 Code Implementation (C++)

```cpp
class Solution {
public:
    long long minCost(string s, vector<int>& cost) {
        int n = s.size();
        long long total = 0;
        vector<long long> cs(26, 0);
        
        for (int i = 0; i < n; i++) {
            total += cost[i];
            cs[s[i] - 'a'] += cost[i];
        }

        long long ans = LLONG_MAX;
        for (int i = 0; i < 26; i++) {
            if (cs[i] > 0) {
                ans = min(ans, total - cs[i]);
            }
        }

        return ans;
    }
};
```

---

## ⏱️ Time and Space Complexity

* **Time Complexity:** `O(n + 26)` → `O(n)`
* **Space Complexity:** `O(26)` → `O(1)`

This makes the solution highly efficient and scalable.

---

## 🏷️ Topic Classification

This problem falls under:

* **Greedy Algorithms**
* **Frequency Counting**
* **Optimization Problems**
* **String Manipulation**

Common tags:

```
#Greedy
#Strings
#Optimization
#PrefixSumIdea
#Implementation
```

---

## ✅ Key Takeaways

* Reframing the problem simplifies the solution
* Choosing what to **keep** is often easier than choosing what to **delete**
* Fixed-size frequency arrays can greatly improve efficiency

---

## 🚀 Final Notes

This solution is clean, optimal, and demonstrates strong problem-solving skills. It is well-suited for:

* Coding interviews
* Competitive programming
* Algorithmic portfolio projects

Happy Coding! 🎯
