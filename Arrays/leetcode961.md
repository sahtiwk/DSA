# Repeated N Times in Array

## Problem Summary

You are given an integer array `nums` with the following guarantees:

* `nums.length = 2 * n`
* There are exactly `n + 1` **unique** elements
* **One element appears exactly `n` times**
* All other elements appear **once**

Your task is to **return the element that is repeated `n` times**.

---

## Key Insight

Since only **one number is repeated many times**, the **first number you encounter twice** while scanning the array must be the answer.

This allows us to solve the problem in **one pass** using a hash-based data structure.

---

## Approach (Using Hash Set)

1. Create an empty hash set `seen`
2. Traverse the array from left to right
3. For each number:

   * If it already exists in `seen`, return it immediately
   * Otherwise, insert it into `seen`

Because the repeated element appears many times, it is guaranteed to be detected early.

---

## Algorithm

* Initialize an empty `unordered_set`
* Iterate through `nums`
* Check if the current element already exists in the set
* If yes → return it
* Else → insert it into the set

---

## C++ Implementation

```cpp
class Solution {
public:
    int repeatedNTimes(vector<int>& nums) {
        unordered_set<int> seen;
        for (int n : nums) {
            if (seen.count(n))
                return n;
            seen.insert(n);
        }
        return -1; // guaranteed not to happen by constraints
    }
};
```

---

## Example Walkthrough

### Input

```
nums = [2, 1, 2, 5, 3, 2]
```

### Steps

| Element | Seen Set | Action                     |
| ------- | -------- | -------------------------- |
| 2       | {}       | insert 2                   |
| 1       | {2}      | insert 1                   |
| 2       | {2,1}    | duplicate found → return 2 |

---

## Complexity Analysis

* **Time Complexity:** `O(n)`

  * Each element is processed once

* **Space Complexity:** `O(n)`

  * Hash set stores at most `n + 1` elements

---

## Why This Works

* Only **one element** repeats
* The moment a duplicate appears, it **must be the answer**
* No sorting or nested loops required

---

## Takeaway

This problem is a classic example where **constraints simplify the solution**.
Recognizing that only one number repeats allows us to stop early and write clean, efficient code.

Happy coding 🚀
