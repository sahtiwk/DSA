# ➕ Plus One (Array Representation of Integer)

## 📌 Problem Statement

You are given a **large integer** represented as an array of digits, where:

* Each `digits[i]` is the **i-th digit** of the number
* Digits are ordered from **most significant to least significant**
* There are **no leading zeros**

Your task is to **increment the integer by one** and return the resulting array of digits.

---

## 🧠 Key Idea

We simulate the process of adding `1` the same way we do on paper:

* Start from the **last digit**
* If the digit is less than `9`, increment it and stop
* If the digit is `9`, convert it to `0` and continue carrying
* If all digits are `9`, the result will have **one extra digit** at the front

---

## ✅ Examples

### Example 1

**Input:** `[1, 2, 3]`
**Output:** `[1, 2, 4]`

### Example 2

**Input:** `[4, 3, 2, 1]`
**Output:** `[4, 3, 2, 2]`

### Example 3

**Input:** `[9]`
**Output:** `[1, 0]`

---

## 🧩 Constraints

* `1 <= digits.length <= 100`
* `0 <= digits[i] <= 9`
* No leading zeros in the input

---

## 🧪 Approach (Step-by-Step)

1. Traverse the array from the **last index to the first**
2. If the current digit is `< 9`:

   * Increment it
   * Return the array immediately
3. If the digit is `9`:

   * Set it to `0` and continue
4. If the loop finishes (all digits were `9`):

   * Create a new array of size `n + 1`
   * Set the first digit to `1`

---

## 💻 C++ Implementation

```cpp
class Solution {
public:
    vector<int> plusOne(vector<int>& digits) {
        int n = digits.size();

        for (int i = n - 1; i >= 0; i--) {
            if (digits[i] < 9) {
                digits[i]++;
                return digits;
            }
            digits[i] = 0;
        }

        vector<int> result(n + 1);
        result[0] = 1;
        return result;
    }
};
```

---

## ⏱️ Complexity Analysis

* **Time Complexity:** `O(n)`
* **Space Complexity:** `O(n)` (only when all digits are `9`)

---

## 🏁 Summary

This is a classic **array manipulation + carry propagation** problem. The solution efficiently mimics integer addition without converting the array into a number, making it safe for very large integers.

Happy coding 🚀
And a Happy New Year!