# 🧮 Maximize Matrix Sum Using Adjacent Sign Flips

## 📌 Problem Statement

You are given an **n × n integer matrix**. You may perform the following operation **any number of times**:

* Choose **any two adjacent elements** (sharing a border)
* Multiply **both elements by -1**

Your goal is to **maximize the sum of all elements** in the matrix after performing any number of such operations.

---

## 🧠 Key Observations

### 1️⃣ Operation preserves parity of negative numbers

* Each operation flips **exactly two elements**
* Number of negative elements changes by **0 or ±2**
* Therefore, the **parity (odd/even)** of negative numbers **never changes**

➡️ This is the core invariant of the problem.

---

### 2️⃣ What is the best possible matrix?

* Ideally, we want **all elements to be positive**
* This gives the **maximum possible sum**

But…

* If the number of negative elements is **odd**, at least **one element must remain negative** (parity cannot change)

---

## 🎯 Strategy

We reduce the entire problem to **counting negatives** and **tracking the smallest absolute value**.

### While iterating through the matrix, compute:

* `sum` → sum of absolute values of all elements
* `negCount` → number of negative elements
* `minAbs` → smallest absolute value in the matrix

---

## ✅ Final Decision Logic

### Case 1: `negCount` is **even**

* All elements can be made positive
* ✅ **Maximum sum = sum of absolute values**

### Case 2: `negCount` is **odd**

* One element must remain negative
* To minimize loss, keep the element with **smallest absolute value** negative

---

## ❓ Why do we subtract `2 × minAbs`?

Let:

* Total absolute sum = `S`
* Smallest absolute value = `x`

If one value `x` must stay negative instead of positive:

* Contribution if positive: `+x`
* Contribution if negative: `-x`

🔻 Net loss = `(+x) - (-x) = 2x`

➡️ Therefore:

```
Maximum sum = S - 2 × minAbs
```

This guarantees the **least possible reduction** while respecting the parity constraint.

---

## 🧾 C++ Implementation

```cpp
class Solution {
public:
    long long maxMatrixSum(vector<vector<int>>& matrix) {
        int n = matrix.size();
        int negcount = 0;
        long long sum = 0;
        int minAbs = INT_MAX;

        for (int i = 0; i < n; i++) {
            for (int j = 0; j < n; j++) {
                sum += abs(matrix[i][j]);
                if (matrix[i][j] < 0) negcount++;
                minAbs = min(minAbs, abs(matrix[i][j]));
            }
        }

        if (negcount % 2 == 0) return sum;
        return sum - 2LL * minAbs;
    }
};
```

---

## 🧪 Example

### Input

```
[[1, 2, 3],
 [-1, -2, -3],
 [1, 2, 3]]
```

### Computation

* Absolute sum = `18`
* Negatives = `3` (odd)
* Minimum absolute value = `1`

### Result

```
18 - 2 × 1 = 16
```

---

## ⏱ Complexity Analysis

* **Time:** `O(n²)`
* **Space:** `O(1)`

Efficient for `n ≤ 250`.

---

## 🏁 Final Takeaway

> The entire problem boils down to **negative count parity**.
>
> * Even negatives → make everything positive
> * Odd negatives → sacrifice the smallest element

This invariant-based approach is both **optimal** and **interview-friendly**.

---

✨ Happy Coding & GitHub documenting!