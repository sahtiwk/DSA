```markdown
# Longest Increasing Subsequence (LIS)

## Problem Description
Given an array of size $N$, find the length of the Longest Increasing Subsequence (LIS). A subsequence is a sequence that can be derived from another sequence by deleting zero or more elements without changing the order of the remaining elements.

### Constraints
- $1 \le T \le 10^3$
- $1 \le N \le 10^4$
- $-10^4 \le arr[i] \le 10^4$
- **Time Limit:** Optimized solution ($O(N \log N)$) required to pass all test cases.

### Example
**Input:**

```

6
94 19 58 80 14 48

```
**Output:**

```

3

```
**Explanation:** One possible LIS is `{19, 58, 80}`.

---

## Logic & Algorithm
To achieve $O(N \log N)$ time complexity, we use a tail-replacement strategy often compared to **Patience Sorting**:

1. **Maintain a Dynamic List (`ans`):** We maintain a list that stores the smallest possible tail for all increasing subsequences of various lengths.
2. **Iteration:**
   - If the current element `ar[i]` is greater than the last element of `ans`, it extends the longest subsequence found so far. We append it.
   - If `ar[i]` is smaller or equal, it cannot extend the current longest subsequence. However, it might be a "better" (smaller) tail for an existing subsequence of some length. 
3. **Binary Search (Ceil Function):** We use binary search to find the first element in `ans` that is greater than or equal to `ar[i]` and replace it. This doesn't change the length of the LIS but makes it easier to extend the subsequence later.



---

## Solution Code (C++)

```cpp
#include <bits/stdc++.h>
using namespace std;

/**
 * Problem: Longest Increasing Subsequence
 * Technique: Binary Search + Greedy (Tail Replacement)
 * Time Complexity: O(T * N log N)
 * Space Complexity: O(N)
 */

// Function to find the index of the first element >= key (Lower Bound/Ceil)
int ceilbs(vector<int> &ar, int key) {
    int lo = 0, hi = ar.size() - 1; 
    int ans = -1; 
    while(lo <= hi) {
        int mid = lo + (hi - lo) / 2; 
        if(ar[mid] >= key) {
            ans = mid;
            hi = mid - 1;
        } else {
            lo = mid + 1;
        }
    }
    return ans;
}

int main() {
    // Fast I/O
    ios::sync_with_stdio(false); 
    cin.tie(nullptr); 

    int T; 
    cin >> T; 

    while(T--) {
        int N; 
        cin >> N; 
        vector<int> ar(N); 
        for(int i = 0; i < N; i++) cin >> ar[i]; 

        if (N == 0) {
            cout << 0 << endl;
            continue;
        }

        vector<int> tails; 
        tails.push_back(ar[0]); 

        for(int i = 1; i < N; i++) {
            if(ar[i] > tails.back()) {
                // Extend the longest subsequence
                tails.push_back(ar[i]);
            } else {
                // Replace the ceiling element to maintain potential for longer sequences
                int idx = ceilbs(tails, ar[i]); 
                tails[idx] = ar[i]; 
            }
        }

        cout << tails.size() << endl;
    } 
    return 0;
}

```

---

## Complexity Analysis

* **Time Complexity:**  per test case. We iterate through  elements and perform a binary search () for each.
* **Space Complexity:**  to store the `tails` vector.

```