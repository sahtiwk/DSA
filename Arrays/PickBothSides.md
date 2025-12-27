# Pick From Both Sides – Maximum Sum

## 🧩 Problem Description

Given an integer array `A` of size `N`, you are required to pick **exactly `B` elements** from either **the left end or the right end** of the array.

Your goal is to **maximize the sum** of the picked elements.

You can pick:

* All `B` elements from the left
* All `B` elements from the right
* Or any combination such as `k` from the left and `B - k` from the right

---

## 📌 Constraints

* `1 ≤ N ≤ 10^5`
* `1 ≤ B ≤ N`
* `-10^3 ≤ A[i] ≤ 10^3`

---

## 🧠 Approach

This problem can be solved efficiently using a **sliding window technique**:

1. Start by calculating the sum of the **first `B` elements**.
2. This represents the case where all elements are taken from the left.
3. Then, iteratively:

   * Remove one element from the left side of the chosen window
   * Add one element from the right end of the array
4. Track the maximum sum encountered during this process.

This ensures we explore **all valid combinations** of picks from both ends.

---

## ⚙️ Algorithm Steps

1. Compute the sum of the first `B` elements.
2. Initialize `maxSum` with this value.
3. Use two pointers:

   * `left = B - 1`
   * `right = N - 1`
4. Loop `B` times:

   * Subtract `A[left]`
   * Add `A[right]`
   * Update `maxSum`
   * Move both pointers inward

---

## 💻 C++ Implementation

```cpp
int Solution::solve(vector<int> &A, int B) {
    int n = A.size();
    
    int currentSum = 0;
    
    // Sum of first B elements
    for (int i = 0; i < B; i++) {
        currentSum += A[i];
    }
    
    int maxSum = currentSum;
    
    int left = B - 1;
    int right = n - 1;
    
    // Slide the window
    for (int i = 0; i < B; i++) {
        currentSum = currentSum - A[left] + A[right];
        maxSum = max(maxSum, currentSum);
        left--;
        right--;
    }
    
    return maxSum;
}
```

---

## ⏱️ Complexity Analysis

* **Time Complexity:** `O(B)`
* **Space Complexity:** `O(1)`

This solution is optimal and works efficiently even for large inputs.

---

## ✅ Example

**Input:**

```
A = [5, -2, 3, 1, 2]
B = 3
```

**Output:**

```
8
```

**Explanation:**
Pick `5` from the front and `1, 2` from the back → `5 + 1 + 2 = 8`

---

Happy Coding 🚀