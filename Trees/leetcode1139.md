# 🌳 Maximum Product of Splitted Binary Tree

This repository contains a **C++ solution** to the LeetCode problem **"Maximum Product of Splitted Binary Tree"**.

---

## 🧩 Problem Statement

Given the root of a binary tree, remove **exactly one edge** so that the tree is split into two non-empty subtrees.

Let:

* `sum1` = sum of values in the first subtree
* `sum2` = sum of values in the second subtree

Your task is to **maximize the product**:

```
sum1 × sum2
```

Since the product can be very large, return the result **modulo 10⁹ + 7**.

⚠️ **Important:** You must maximize the product **before** applying the modulo.

---

## 🔍 Key Insight

If the **total sum** of the tree is `S`, and a subtree has sum `x`, then removing the edge above that subtree gives:

```
Product = x × (S − x)
```

So the problem reduces to:

1. Computing the total sum of the tree
2. Computing the sum of every subtree
3. Finding the maximum value of `x × (S − x)`

---

## 🚀 Approach

We solve this using **two Depth-First Search (DFS) traversals**:

### 1️⃣ First DFS — Compute Total Sum

Traverse the entire tree to calculate the total sum of all node values.

### 2️⃣ Second DFS — Compute Subtree Sums

For every node:

* Compute the sum of its subtree
* Treat that subtree as one side of the cut
* Compute the product with the remaining tree
* Track the maximum product

Finally, apply modulo `10⁹ + 7` **after** the maximum product is found.

---

## ✅ Correctness Notes

* Uses `long long` to safely store large sums and products
* Modulo is applied **only at the end** (critical to avoid overflow bugs)
* Time Complexity: **O(N)**
* Space Complexity: **O(H)** where `H` is the height of the tree (recursion stack)

---

## 💻 C++ Implementation

```cpp
class Solution {
public:
    long long total = 0;
    long long ans = 0;
    const int MOD = 1e9 + 7;

    long long totalsum(TreeNode* root) {
        if (!root) return 0;
        return root->val + totalsum(root->left) + totalsum(root->right);
    }

    long long dfs(TreeNode* root) {
        if (!root) return 0;

        long long left = dfs(root->left);
        long long right = dfs(root->right);

        long long sub = root->val + left + right;
        ans = max(ans, sub * (total - sub));

        return sub;
    }

    int maxProduct(TreeNode* root) {
        total = totalsum(root);
        dfs(root);
        return (int)(ans % MOD);
    }
};
```

---

## 🧪 Example

**Input:**

```
[1,2,3,4,5,6]
```

**Output:**

```
110
```

**Explanation:**

* Split results in subtree sums `11` and `10`
* Maximum product = `11 × 10 = 110`

---

## 🧠 Common Pitfall (Very Important!)

❌ **Wrong:**

```cpp
return (int)ans % MOD;
```

✔️ **Correct:**

```cpp
return (int)(ans % MOD);
```

Always apply modulo **before** casting to a smaller type.

---

## 📌 Takeaway

This problem is a great example of:

* Tree DP
* Careful handling of large numbers
* Understanding operator precedence in C++

---

⭐ If you found this helpful, feel free to star the repo and use it as a reference in your DSA journey!