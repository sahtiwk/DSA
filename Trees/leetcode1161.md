# Maximum Level Sum of a Binary Tree

## 📌 Problem Statement

Given the root of a binary tree:

* The root is at **level 1**
* Its children are at **level 2**, and so on

Return the **smallest level number** such that the **sum of all node values at that level is maximum**.

---

## 🧠 Approach: Breadth-First Search (Level Order Traversal)

To solve this problem efficiently, we use **Breadth-First Search (BFS)** because it naturally processes the tree **level by level**.

### Why BFS?

* Each level is handled separately
* Easy to compute sum per level
* Guarantees smallest level is chosen if sums tie

---

## 🚀 Algorithm Steps

1. Initialize a queue and push the root node.
2. Keep track of:

   * `curr` → current level number
   * `maxSum` → maximum level sum seen so far
   * `ans` → level corresponding to `maxSum`
3. While the queue is not empty:

   * Process all nodes at the current level
   * Calculate the sum of node values
   * Push child nodes into the queue
4. Update `maxSum` and `ans` when a higher sum is found
5. Return `ans`

---

## ⏱️ Complexity Analysis

* **Time Complexity:** `O(N)` — each node is visited once
* **Space Complexity:** `O(N)` — queue storage in the worst case

---

## 💻 C++ Implementation

```cpp
/**
 * Definition for a binary tree node.
 * struct TreeNode {
 *     int val;
 *     TreeNode *left;
 *     TreeNode *right;
 *     TreeNode() : val(0), left(nullptr), right(nullptr) {}
 *     TreeNode(int x) : val(x), left(nullptr), right(nullptr) {}
 *     TreeNode(int x, TreeNode *left, TreeNode *right)
 *         : val(x), left(left), right(right) {}
 * };
 */
class Solution {
public:
    int maxLevelSum(TreeNode* root) {
        queue<TreeNode*> q;
        q.push(root);

        int curr = 1;
        int ans = 1;
        long long maxSum = LLONG_MIN;

        while (!q.empty()) {
            int sz = q.size();
            long long currSum = 0;

            for (int i = 0; i < sz; i++) {
                TreeNode* node = q.front();
                q.pop();

                currSum += node->val;

                if (node->left) q.push(node->left);
                if (node->right) q.push(node->right);
            }

            if (currSum > maxSum) {
                maxSum = currSum;
                ans = curr;
            }

            curr++;
        }

        return ans;
    }
};
```

---

## ✅ Example

**Input:**

```
[1,7,0,7,-8,null,null]
```

**Level Sums:**

* Level 1 → 1
* Level 2 → 7
* Level 3 → -1

**Output:**

```
2
```

---

## 🏁 Conclusion

This solution efficiently finds the level with the maximum sum using BFS. It is optimal, clean, and handles negative values correctly.

Feel free to fork or star ⭐ if you found this useful!