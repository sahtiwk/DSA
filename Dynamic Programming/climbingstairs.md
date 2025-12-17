# 70. Climbing Stairs

## Problem Statement
You are climbing a staircase. It takes `n` steps to reach the top. Each time you can either climb 1 or 2 steps. In how many distinct ways can you climb to the top?

## Examples

### Example 1
```
Input: n = 2
Output: 2
Explanation: 
1. 1 step + 1 step
2. 2 steps
```

### Example 2
```
Input: n = 3
Output: 3
Explanation:
1. 1 step + 1 step + 1 step
2. 1 step + 2 steps
3. 2 steps + 1 step
```

## Constraints
- `1 <= n <= 45`

## Solution Approach
This is a dynamic programming problem. The key insight is that to reach step `n`, you can come from step `n-1` (by taking 1 step) or from step `n-2` (by taking 2 steps). Therefore:
```
ways(n) = ways(n-1) + ways(n-2)
```

This follows the Fibonacci sequence pattern.

## Code
```java
class Solution {
    public int climbStairs(int n) {
        if(n <= 3) return n;
        int prev = 3;      // ways to reach step 2
        int prev1 = 2;     // ways to reach step 1
        int curr = 0;
        for(int i = 3; i < n; i++) {
            curr = prev + prev1;
            prev1 = prev;
            prev = curr;
        }
        return curr;
    }
}
```

## Complexity Analysis
- **Time Complexity:** O(n) - single loop iteration
- **Space Complexity:** O(1) - only three variables used
