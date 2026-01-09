# Subtree With All Deepest Nodes

This repository contains a clean and efficient C++ solution to the LeetCode problem **Subtree With All Deepest Nodes** (also known as **Lowest Common Ancestor of Deepest Leaves**, Problem 1123).

---

## 🧠 Problem Summary

Given the root of a binary tree:

* Each node has a depth defined as its distance from the root.
* A **deepest node** is one with the maximum depth in the tree.

### Objective

Return the **smallest subtree** that contains **all deepest nodes**.

---

## 💡 Key Insight

* If the deepest nodes exist in **both left and right subtrees** of a node, that node is the answer.
* If the deepest nodes exist **only on one side**, recursively search that subtree.

This naturally leads to a **depth-based recursive approach**.

---

## 🚀 Approach

1. Compute the depth of left and right subtrees.
2. Compare depths:

   * If equal → current node is the LCA of deepest leaves.
   * If left is deeper → recurse left.
   * If right is deeper → recurse right.
3. Repeat until the smallest valid subtree is found.

---

## 🧾 C++ Implementation

```cpp
/**
 * Definition for a binary tree node.
 * struct TreeNode {
 *     int val;
 *     TreeNode *left;
 *     TreeNode *right;
 *     TreeNode() : val(0), left(nullptr), right(nullptr) {}
 *     TreeNode(int x) : val(x), left(nullptr), right(nullptr) {}
 *     TreeNode(int x, TreeNode *left, TreeNode *right) : val(x), left(left), right(right) {}
 * };
 */
class Solution {
public:

    int depth(TreeNode* node) {
        if (node == nullptr) return 0;
        return 1 + max(depth(node->left), depth(node->right));
    }

    TreeNode* lcaDeepestLeaves(TreeNode* root) {
        if (!root) return nullptr;

        int leftDepth = depth(root->left);
        int rightDepth = depth(root->right);

        if (leftDepth == rightDepth) return root;
        if (leftDepth > rightDepth) return lcaDeepestLeaves(root->left);
        return lcaDeepestLeaves(root->right);
    }

    TreeNode* subtreeWithAllDeepest(TreeNode* root) {
        return lcaDeepestLeaves(root);
    }
};
```

---

## ⏱️ Complexity Analysis

* **Time Complexity:** `O(N^2)` (due to repeated depth calculations)
* **Space Complexity:** `O(H)` where `H` is the height of the tree (recursion stack)

> 💡 Note: This can be optimized to `O(N)` using a single DFS pass.

---

## 🧪 Examples

| Input                           | Output    |
| ------------------------------- | --------- |
| `[3,5,1,6,2,0,8,null,null,7,4]` | `[2,7,4]` |
| `[1]`                           | `[1]`     |
| `[0,1,3,null,2]`                | `[2]`     |

---

## 🔗 Related Problem

* LeetCode 1123: Lowest Common Ancestor of Deepest Leaves

---

## ✨ Author

Built for learning, clarity, and GitHub-ready presentation.

Happy Coding 🚀
