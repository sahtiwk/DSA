# 🪞 Mirror Distance of an Integer

## 📌 Problem Overview

You are given an integer **n**. The task is to compute its **mirror distance**, which is defined as:

```
abs(n - reverse(n))
```

Where:

* `reverse(n)` is the integer formed by reversing the digits of `n`
* `abs(x)` denotes the absolute value of `x`

The goal is to return the mirror distance as an integer.

---

## ✨ Examples

### Example 1

**Input:** `n = 25`
**Reverse:** `52`
**Mirror Distance:** `abs(25 - 52) = 27`

### Example 2

**Input:** `n = 10`
**Reverse:** `01 → 1`
**Mirror Distance:** `abs(10 - 1) = 9`

### Example 3

**Input:** `n = 7`
**Reverse:** `7`
**Mirror Distance:** `abs(7 - 7) = 0`

---

## 🧠 Thought Process & Ideology

To solve this problem efficiently and cleanly, I followed these guiding principles:

### 1️⃣ Break the Problem into Simple Steps

Instead of thinking about the problem as a whole, I divided it into smaller, manageable parts:

* Extract digits of the number
* Reverse the digits mathematically
* Compute the absolute difference

This approach reduces complexity and avoids unnecessary conversions (like strings).

---

### 2️⃣ Avoid String Conversion

Although reversing a number using strings is possible, I intentionally chose a **pure mathematical approach** because:

* It improves understanding of number manipulation
* It avoids extra memory overhead
* It performs consistently even for large numbers

This reflects a **low-level, algorithmic mindset**, which is often preferred in interviews and competitive programming.

---

### 3️⃣ Use a Loop to Reverse the Number

The reversal logic is based on a standard digit-extraction technique:

* Use `% 10` to extract the last digit
* Multiply the reversed number by `10` and add the digit
* Divide the original number by `10` to move to the next digit

This continues until all digits are processed.

---

### 4️⃣ Preserve the Original Number

A temporary variable is used so that:

* The original value of `n` remains unchanged
* We can safely compute the difference at the end

This reflects **defensive programming**, ensuring data integrity.

---

### 5️⃣ Absolute Difference for Correctness

The mirror distance must always be non-negative. Using `abs()` guarantees correctness regardless of whether the reversed number is greater or smaller than the original.

---

## 🧩 Algorithm Explanation

1. Initialize `rev = 0`
2. Store `n` in a temporary variable `temp`
3. While `temp` is not zero:

   * Extract the last digit using `% 10`
   * Append it to `rev`
   * Remove the last digit using `/ 10`
4. Compute and return `abs(n - rev)`

---

## 💻 Code Implementation (C++)

```cpp
class Solution {
public:
    int mirrorDistance(int n) {
        int rev = 0;
        int temp = n;
        
        while (temp != 0) {
            int rem = temp % 10;
            rev = (rev * 10) + rem;
            temp /= 10;
        }
        
        return abs(n - rev);
    }
};
```

---

## ⏱️ Time and Space Complexity

* **Time Complexity:** `O(d)` where `d` is the number of digits in `n`
* **Space Complexity:** `O(1)` (constant extra space)

This makes the solution optimal and scalable for values up to `10^9`.

---

## ✅ Key Takeaways

* Mathematical digit manipulation is efficient and elegant
* Avoiding unnecessary string conversions leads to better performance
* Clear step-by-step logic improves readability and maintainability

---

## 🚀 Final Note

This solution emphasizes **clarity, efficiency, and strong algorithmic fundamentals**, making it suitable for coding interviews, competitive programming, and real-world applications.

Happy Coding! 🎯
