```markdown
# Maximum Subarray Sum (Kadane's Algorithm)

## Problem Description
Given an array of integers, find the maximum subarray sum. If multiple subarrays give the same sum, consider the lexicographical smallest indices (the one that starts earlier and ends earlier).

### Constraints
- $1 \le T \le 100$
- $1 \le N \le 10^4$
- $-10^3 \le A[i] \le 10^3$

### Example
**Input:**

```

9 -24 0 28 28 55 -31 -27 -45 -24

```
**Output:**

```

111 1 4

```

---

## Logic Explanation
The solution uses **Kadane's Algorithm**, which runs in $O(N)$ time. 

1. **Current Sum tracking:** We iterate through the array, adding each element to `sum`.
2. **Reset Condition:** If `sum` becomes negative, it's better to start a new subarray from the current element rather than carrying over a negative prefix. 
3. **Maximum Sum tracking:** Every time `sum` exceeds `max_sum`, we update our answer and record the `ansstart` and `ansend` indices.
4. **Lexicographical Requirement:** By updating the `max_sum` only when the new sum is strictly greater (`sum > max_sum`), we naturally preserve the earliest occurring subarray in case of ties.

---

## Solution Code (C++)

```cpp
#include <bits/stdc++.h>
using namespace std;

/**
 * Problem: Maximum Subarray Sum with Indices
 * Technique: Kadane's Algorithm
 * Time Complexity: O(N)
 * Space Complexity: O(N) to store the array
 */

int main() {
    ios_base::sync_with_stdio(false);
    cin.tie(NULL);

    int T; 
    cin >> T; 

    while(T--) {
        int N; 
        cin >> N;
        
        vector<int> ar(N); 
        for(int i = 0; i < N; i++) cin >> ar[i]; 

        int ansstart = 0, ansend = 0;
        long long max_sum = LLONG_MIN;
        long long sum = 0; 
        int start = 0;

        for(int i = 0; i < N; i++) {
            // If the current prefix sum is negative, start fresh at current index
            if(sum < 0) {
                sum = ar[i];
                start = i; 
            } else {
                sum += ar[i];
            }

            // Update global maximum and track indices
            if(sum > max_sum) {
                max_sum = sum; 
                ansstart = start; 
                ansend = i; 
            }
        }

        cout << max_sum << " " << ansstart << " " << ansend << endl;
    } 
    return 0;
}

```

---

## Complexity Analysis

* **Time Complexity:**  per test case, as we traverse the array exactly once.
* **Space Complexity:**  to store the input array.

```

---

Would you like me to explain how to optimize this to **$O(1)$ space** by processing the input numbers as they are read, instead of storing them in a vector?

```