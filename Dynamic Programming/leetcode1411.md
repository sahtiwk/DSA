# Paint a Grid With 3 Colors (n x 3)

## Problem Summary

You are given a grid of size **n x 3**. Each cell must be painted using **one of three colors**:

* Red
* Yellow
* Green

### Constraints

* No two **adjacent cells** (horizontal or vertical) can have the same color.
* Return the **total number of valid colorings modulo** `1e9 + 7`.
* `1 ≤ n ≤ 5000`

---

## Key Insight

Instead of tracking all color combinations explicitly (which would be exponential), we observe that **each row can be categorized into two patterns**:

### 1. ABA Pattern

* First and third cells have the **same color**
* Middle cell has a **different color**
* Example: `Red Yellow Red`

Number of such patterns for one row:

* Choose color for A → 3 ways
* Choose different color for B → 2 ways
* **Total = 3 × 2 = 6**

### 2. ABC Pattern

* All three cells have **different colors**
* Example: `Red Yellow Green`

Number of such patterns for one row:

* 3! = **6** ways

So for the **first row**:

```
ABA = 6
ABC = 6
```

---

## Dynamic Programming Approach

Let:

* `aba[i]` = number of ways to paint up to row `i` where row `i` is an **ABA** pattern
* `abc[i]` = number of ways to paint up to row `i` where row `i` is an **ABC** pattern

Instead of arrays, we optimize to **O(1) space** by keeping only the previous row values.

---

## Transition Relations

From the adjacency constraints, the transitions are:

```
new_aba = 3 * prev_aba + 2 * prev_abc
new_abc = 2 * prev_aba + 2 * prev_abc
```

### Why this works

* An **ABA row** can follow:

  * 3 valid ABA configurations
  * 2 valid ABC configurations

* An **ABC row** can follow:

  * 2 valid ABA configurations
  * 2 valid ABC configurations

All calculations are done modulo `1e9 + 7`.

---

## Algorithm Steps

1. Initialize:

   ```cpp
   aba = 6;
   abc = 6;
   ```
2. For rows `2` to `n`, update using transition formulas
3. Final answer:

   ```cpp
   return (aba + abc) % mod;
   ```

---

## Time & Space Complexity

* **Time Complexity:** `O(n)`
* **Space Complexity:** `O(1)`

Efficient enough for `n = 5000`.

---

## Example

### Input

```
n = 1
```

### Output

```
12
```

Explanation: `6 (ABA) + 6 (ABC)`

---

## Final Code

```cpp
class Solution {
public:
    int numOfWays(int n) {
        long long aba = 6;
        long long abc = 6;
        long long mod = 1e9 + 7;
        
        for (int i = 2; i <= n; i++) {
            long long prev_aba = aba;
            long long prev_abc = abc;

            aba = (3 * prev_aba + 2 * prev_abc) % mod;
            abc = (2 * prev_aba + 2 * prev_abc) % mod;
        }
        
        return (aba + abc) % mod;
    }
};
```

---

## Takeaway

By reducing the problem to **row patterns and transitions**, we avoid brute force and achieve an elegant and efficient solution using dynamic programming.

Happy coding 🚀