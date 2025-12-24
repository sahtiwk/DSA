# 🍎 LeetCode 3074 – Apple Redistribution into Boxes

## 📘 Problem Statement

You are given two integer arrays:

* `apple` of size `n`, where `apple[i]` represents the number of apples in the *i-th pack*.
* `capacity` of size `m`, where `capacity[j]` represents the capacity of the *j-th box*.

You want to redistribute **all apples from all packs into some of the boxes**.

### Important Rules

* Apples from the **same pack can be split across multiple boxes**.
* Each box has a **maximum capacity**.
* You may choose **any subset of boxes**.

### Goal

Return the **minimum number of boxes** required to store all the apples.

The problem guarantees that a solution always exists.

---

## 🧠 Key Observations

1. Since apples from the same pack **can be split**, we do **not** need to care about individual packs.
2. What really matters is:

   > **Total apples ≤ total selected box capacity**
3. To minimize the number of boxes used, we should:

   * Always pick boxes with **largest capacity first**.

This naturally leads to a **greedy strategy**.

---

## 💡 Strategy (Greedy Approach)

1. **Compute the total number of apples**.
2. **Sort the box capacities in descending order**.
3. Start picking boxes from the largest capacity:

   * Subtract the box capacity from the remaining apples.
   * Count how many boxes are used.
4. Stop once all apples are placed.

This guarantees the **minimum number of boxes**, because using smaller boxes first would only increase the count.

---

## ✍️ Example Walkthrough

### Example 1

```
apple    = [1, 3, 2]   → total apples = 6
capacity = [4, 3, 1, 5, 2]
```

Sorted capacities (descending):

```
[5, 4, 3, 2, 1]
```

Pick boxes:

* Use 5 → remaining apples = 1
* Use 4 → remaining apples = -3 (done)

✅ **Answer = 2 boxes**

---

### Example 2

```
apple    = [5, 5, 5] → total apples = 15
capacity = [2, 4, 2, 7]
```

Sorted capacities:

```
[7, 4, 2, 2]
```

Pick boxes:

* 7 → remaining = 8
* 4 → remaining = 4
* 2 → remaining = 2
* 2 → remaining = 0

✅ **Answer = 4 boxes**

---

## ✅ Final C++ Solution

```cpp
class Solution {
public:
    int minimumBoxes(vector<int>& apple, vector<int>& capacity) {
        int sum = 0;
        
        // Step 1: Sum all apples
        for (int a : apple) {
            sum += a;
        }

        // Step 2: Sort capacities in descending order
        sort(capacity.rbegin(), capacity.rend());

        // Step 3: Greedily pick boxes
        int count = 0;
        for (int c : capacity) {
            if (sum <= 0) break;
            sum -= c;
            count++;
        }

        return count;
    }
};
```

---

## ⏱️ Complexity Analysis

* **Time Complexity:** `O(m log m)` due to sorting the box capacities
* **Space Complexity:** `O(1)` (in-place sort)

Where `m` is the number of boxes.

---

## 🏁 Conclusion

* The problem reduces to a **capacity coverage problem**.
* Since splitting apples is allowed, we only care about totals.
* A **greedy approach** using the largest boxes first guarantees the minimum number of boxes.

This solution is efficient, clean, and passes all constraints.

---

⭐ Feel free to fork, copy, or adapt this explanation for your GitHub repository!