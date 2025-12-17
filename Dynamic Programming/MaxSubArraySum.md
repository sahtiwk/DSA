
# Maximum Subarray

## Problem Statement

Given an integer array `nums`, find the subarray with the largest sum and return its sum.

### Constraints
- `1 <= nums.length <= 10^5`
- `-10^4 <= nums[i] <= 10^4`

## Examples

### Example 1
**Input:** `nums = [-2,1,-3,4,-1,2,1,-5,4]`  
**Output:** `6`  
**Explanation:** The subarray `[4,-1,2,1]` has the largest sum 6.

### Example 2
**Input:** `nums = [1]`  
**Output:** `1`  
**Explanation:** The subarray `[1]` has the largest sum 1.

### Example 3
**Input:** `nums = [5,4,-1,7,8]`  
**Output:** `23`  
**Explanation:** The subarray `[5,4,-1,7,8]` has the largest sum 23.

## Solution

**Approach:** Kadane's Algorithm (Dynamic Programming)

```cpp
class Solution {
public:
    int maxSubArray(vector<int>& nums) {
        int curr = 0, maxtilNow = INT_MIN; 
        for(int num : nums) {
            curr = max(num, curr + num); 
            maxtilNow = max(maxtilNow, curr); 
        }
        return maxtilNow;
    }
};
```

### Explanation
- **`curr`**: Tracks the maximum sum ending at the current position
- **`maxtilNow`**: Stores the overall maximum sum found so far
- At each element, we decide whether to start a new subarray or extend the existing one
- Time Complexity: **O(n)**
- Space Complexity: **O(1)**
