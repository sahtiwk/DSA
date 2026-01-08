# Maximum Dot Product of Two Subsequences

## 📌 Problem Overview

Given two integer arrays `nums1` and `nums2`, the task is to compute the **maximum dot product** between **non-empty subsequences** of both arrays such that:

* Both subsequences have the **same length**
* The **relative order** of elements is preserved
* The subsequences are **non-empty**

The dot product of two arrays of equal length is defined as:

```
(a1 * b1) + (a2 * b2) + ... + (ak * bk)
```

This project implements an **efficient dynamic programming solution** that correctly handles **negative values**, which is the main challenge of the problem.

---

## 🧠 Key Insight

* Standard DP approaches fail when all products are negative.
* To fix this, we explicitly allow **starting a new subsequence at any position** instead of defaulting to `0`.
* This guarantees correctness even in worst-case scenarios.

---

## 🛠️ Approach

We use a 2D Dynamic Programming table where:

```
dp[i][j] = maximum dot product using non-empty subsequences
           from nums1[0..i-1] and nums2[0..j-1]
```

### Transition Formula

```
product = nums1[i-1] * nums2[j-1]

dp[i][j] = max(
    product,
    product + dp[i-1][j-1],
    dp[i-1][j],
    dp[i][j-1]
)
```

---

## ✅ Example

**Input**

```
nums1 = [2, 1, -2, 5]
nums2 = [3, 0, -6]
```

**Output**

```
18
```

**Explanation**

Subsequences chosen:

```
nums1 → [2, -2]
nums2 → [3, -6]
```

Dot Product:

```
(2 × 3) + (-2 × -6) = 18
```

---

## 💻 C++ Implementation

```cpp
class Solution {
public:
    int maxDotProduct(vector<int>& nums1, vector<int>& nums2) {
        int n = nums1.size(), m = nums2.size();
        const int NEG_INF = -1e9;

        vector<vector<int>> dp(n + 1, vector<int>(m + 1, NEG_INF));

        for (int i = 1; i <= n; i++) {
            for (int j = 1; j <= m; j++) {
                int product = nums1[i - 1] * nums2[j - 1];
                dp[i][j] = max({
                    product,
                    product + dp[i - 1][j - 1],
                    dp[i - 1][j],
                    dp[i][j - 1]
                });
            }
        }
        return dp[n][m];
    }
};
```

---

## ⏱️ Complexity Analysis

* **Time Complexity:** `O(n × m)`
* **Space Complexity:** `O(n × m)`

> Can be optimized to `O(m)` space if required.

---

## 🚀 How to Run

1. Copy the C++ code into a `.cpp` file
2. Compile using a C++17 compatible compiler
3. Run with your test cases

---

## 📚 References

* LeetCode Problem 1458: *Maximum Dot Product of Two Subsequences*
* Dynamic Programming (DP) Optimization Techniques

---

## ✨ Author

Developed as part of algorithmic problem-solving practice and competitive programming preparation.

---

⭐ If you found this helpful, consider giving the repository a star!