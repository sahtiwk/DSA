# 944. Delete Columns to Make Sorted

## 📌 Problem Statement

You are given an array of **n strings**, all having the **same length**.

Think of these strings as rows in a grid. Each column is formed by characters at the same index across all strings.

Your task is to **delete the columns that are NOT sorted lexicographically (top to bottom)** and return the **number of columns deleted**.

---

## 🔍 Example

**Input:**

```
strs = ["cba", "daf", "ghi"]
```

**Grid Representation:**

```
c b a
d a f
g h i
```

* Column 0 → `c, d, g` ✅ sorted
* Column 1 → `b, a, h` ❌ not sorted
* Column 2 → `a, f, i` ✅ sorted

**Output:**

```
1
```

---

## 💡 Approach

### Key Idea

For each column:

* Compare characters **row by row**.
* If any character is **greater than the one below it**, the column is **not sorted**.
* Mark that column for deletion.

### Step-by-Step

1. Get the number of columns using the length of the first string.
2. Iterate through each column.
3. For each column, compare characters from `strs[j][i]` and `strs[j+1][i]`.
4. If any comparison breaks lexicographical order, increment the delete count.
5. Return the total count.

---

## 🧠 Implementation (C++)

```cpp
class Solution {
public:
    int minDeletionSize(vector<string>& strs) {
        int n = strs[0].size();
        int count = 0;
        
        for (int i = 0; i < n; i++) {
            bool deletion = false;
            for (int j = 0; j < strs.size() - 1; j++) {
                if (strs[j][i] > strs[j + 1][i]) {
                    deletion = true;
                    break;
                }
            }
            if (deletion) count++;
        }
        return count;
    }
};
```

---

## ⏱️ Time Complexity

* Let:

  * `n` = number of strings
  * `m` = length of each string

* We iterate through **all columns** and compare **adjacent rows**:

```
Time Complexity: O(n × m)
```

---

## 🧮 Space Complexity

* No extra data structures used apart from variables.

```
Space Complexity: O(1)
```

---

## ✅ Summary

* Simple brute-force column check
* Efficient for given constraints
* Clean and readable solution

---

⭐ If you found this helpful, consider giving the repo a star!
