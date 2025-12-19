# Longest Increasing Subsequence (LIS)

## Problem Statement

Given an integer array `nums`, return the **length of the longest strictly increasing subsequence**.

A subsequence is derived from the array by deleting some or no elements without changing the order of the remaining elements.

---

## Examples

```
Input:  [10,9,2,5,3,7,101,18]
Output: 4
Explanation: LIS is [2,3,7,101]
```

```
Input:  [0,1,0,3,2,3]
Output: 4
```

```
Input:  [7,7,7,7,7,7,7]
Output: 1
```

---

## Constraints

* `1 <= nums.length <= 2500`
* `-10^4 <= nums[i] <= 10^4`

---

## Approach Used

### Greedy + Binary Search (O(n log n))

This solution uses an **optimized approach** to compute the LIS in `O(n log n)` time.

### Key Idea

We maintain a helper array `ans` where:

* `ans[i]` represents the **smallest possible ending value** of an increasing subsequence of length `i + 1`.
* The array `ans` is always **sorted**.

Important:

> The `ans` array does **not** necessarily represent the actual subsequence, but its length always equals the length of the LIS.

---

## Algorithm Steps

1. Initialize an empty array `ans`.
2. Insert the first element of `nums` into `ans`.
3. For each subsequent element in `nums`:

   * If the current number is **greater than the last element** of `ans`, append it.
   * Otherwise, use **binary search** to find the first element in `ans` that is `>= current number` and replace it.
4. The final size of `ans` is the length of the LIS.

---

## Why This Works

* Replacing elements keeps `ans` optimal and sorted.
* Smaller ending values give more chances to build longer increasing subsequences.
* Binary search ensures efficient updates.

---

## Time and Space Complexity

* **Time Complexity:** `O(n log n)`
* **Space Complexity:** `O(n)`

---

## Implementation (C++)

```cpp
class Solution {
public:
    int ceilbs(vector<int> &ar, int key){
        int lo = 0, hi = ar.size() - 1;
        int ans = -1;
        while(lo <= hi){
            int mid = lo + (hi - lo) / 2;
            if(ar[mid] >= key){
                ans = mid;
                hi = mid - 1;
            } else {
                lo = mid + 1;
            }
        }
        return ans;
    }

    int lengthOfLIS(vector<int>& nums) {
        vector<int> ans;
        ans.push_back(nums[0]);

        for(int i = 1; i < nums.size(); i++){
            if(ans.back() < nums[i]){
                ans.push_back(nums[i]);
            } else {
                int idx = ceilbs(ans, nums[i]);
                ans[idx] = nums[i];
            }
        }
        return ans.size();
    }
};
```

---

## Summary

* Used **Greedy strategy** to maintain optimal subsequence endings
* Applied **Binary Search** to ensure efficiency
* Achieved optimal `O(n log n)` runtime

This approach is commonly known as the **Patience Sorting technique** for LIS.

---

⭐ If you found this helpful, feel free to star the repository!
