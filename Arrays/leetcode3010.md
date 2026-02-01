# LeetCode 3010 — Divide an Array Into Subarrays With Minimum Cost I

## 🧩 Problem Summary

You are given an integer array `nums` of length `n` (`n ≥ 3`).

* The **cost** of a subarray is defined as its **first element**.
* You must divide the array into **exactly 3 disjoint contiguous subarrays**.
* Your goal is to **minimize the sum of the costs** of these 3 subarrays.

---

## 💡 Key Insight

Since the array must be divided into **3 contiguous subarrays**, their costs will be:

1. The first element of the original array → `nums[0]`
2. The first element of the second subarray
3. The first element of the third subarray

To minimize the total cost:

* The first subarray **must start at index 0**, so its cost is fixed: `nums[0]`
* We should choose the **two smallest possible values** from the remaining elements to act as the starting points of the other two subarrays

Thus, the solution is:

> **nums[0] + the two smallest values from nums[1..n-1]**

---

## ✅ Approach

1. Store the first element separately (it must be included).
2. Sort the remaining elements.
3. Add the two smallest values from the sorted remainder.

---

## 🧪 Examples

### Example 1

```
Input:  nums = [1,2,3,12]
Output: 6
Explanation: [1], [2], [3,12] → 1 + 2 + 3 = 6
```

### Example 2

```
Input:  nums = [5,4,3]
Output: 12
Explanation: [5], [4], [3] → 5 + 4 + 3 = 12
```

### Example 3

```
Input:  nums = [10,3,1,1]
Output: 12
Explanation: [10,3], [1], [1] → 10 + 1 + 1 = 12
```

---

## 🧠 C++ Solution

```cpp
class Solution {
public:
    int minimumCost(vector<int>& nums) {
        int first = nums[0];
        sort(nums.begin() + 1, nums.end());
        return first + nums[1] + nums[2];
    }
};
```

---

## ⏱️ Complexity Analysis

* **Time Complexity:** `O(n log n)` (due to sorting)
* **Space Complexity:** `O(1)` (in-place sort)

---

## 🚀 Notes

* Constraints are small (`n ≤ 50`), so sorting is efficient.
* This greedy strategy works because only the **first elements of subarrays matter**, not their lengths.

Happy coding! 🎯