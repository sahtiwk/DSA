# Divide an Array Into Subarrays With Minimum Cost

This repository contains an **optimized C++ solution** for the problem:

> **Divide an Array Into Subarrays With Minimum Cost**

The solution is designed to handle large inputs efficiently (up to `n = 10^5`) and is suitable for competitive programming and interview preparation.

---

## 🧩 Problem Summary

You are given:

* A 0-indexed array `nums` of length `n`
* Two integers `k` and `dist`

### Rules

* Divide `nums` into `k` **disjoint contiguous subarrays**
* The **cost** of each subarray is its **first element**
* Let the starting indices of subarrays be:

  ```
  0 = i0 < i1 < i2 < ... < i(k-1)
  ```
* The following constraint must hold:

  ```
  i(k-1) - i1 <= dist
  ```

### Goal

Return the **minimum possible sum of costs** of the `k` subarrays.

---

## 💡 Key Insight

* The first subarray **always starts at index 0**, so `nums[0]` is always included in the answer
* We only need to choose **`k-1` more starting indices**
* Those indices must lie inside a window of size `dist + 1`
* For every valid window, we want the **smallest `k-1` values**

This leads to a **sliding window + balanced data structure** approach.

---

## 🚀 Optimized Approach

We use a custom structure called **SmartWindow**:

* Maintains two multisets:

  * `low`  → contains the smallest `k-1` elements
  * `high` → contains the remaining elements
* Keeps track of the sum of elements in `low`
* Supports:

  * Insertion
  * Deletion
  * Rebalancing to maintain exactly `k-1` smallest values

Each window update takes **O(log k)** time.

---

## ⏱️ Complexity Analysis

| Metric           | Value          |
| ---------------- | -------------- |
| Time Complexity  | **O(n log k)** |
| Space Complexity | **O(k)**       |

Efficient enough for the maximum constraints.

---

## ✅ Correctness

* Handles **duplicate values** safely
* Avoids incorrect assumptions about element ownership
* Passes all edge cases including:

  * Large `dist`
  * Repeated patterns
  * Worst-case inputs

---

## 🧪 Example

```text
Input:
nums = [10,1,2,2,2,1]
k = 4
dist = 3

Output:
15
```

---

## 🧠 C++ Implementation

```cpp
class Solution {
public:
    struct SmartWindow{
        int K;
        multiset<int> low, high;
        long long sumLow = 0;

        SmartWindow(int k) : K(k) {}

        int windowSize() const{
            return (int)low.size() + (int)high.size();
        }
        void rebalance() {
            int need = min(K, windowSize());

            while((int)low.size() > need){
                auto it = prev(low.end());
                int x = *it;
                low.erase(it);
                sumLow -= x;
                high.insert(x);
            }
            while((int)low.size() < need && !high.empty()){
                auto it = high.begin();
                int x = *it;
                high.erase(it);
                low.insert(x);
                sumLow += x;
            }
        }
        void add(int x){
            if(low.empty() || x <= *prev(low.end())){
                low.insert(x);
                sumLow += x;
            }
            else{
                high.insert(x);
            }
            rebalance();
        }
        void remove(int x){
            auto itLow = low.find(x);
            if(itLow != low.end()){
                low.erase(itLow);
                sumLow -= x;
            }
            else{
                auto itHigh = high.find(x);
                if(itHigh != high.end()){
                    high.erase(itHigh);
                }
            }
            rebalance();
        }
        long long query() const{
            return sumLow;
        }
    };

    long long minimumCost(vector<int>& nums, int k, int dist) {
        int n = nums.size();
        k -= 1;
        SmartWindow window(k);

        for(int i = 1; i <= 1 + dist; i++){
            window.add(nums[i]);
        }

        long long ans = window.query();

        for(int i = 2; i + dist < n; i++){
            window.remove(nums[i - 1]);
            window.add(nums[i + dist]);
            ans = min(ans, window.query());
        }

        return ans + nums[0];
    }
};
```

---

## 📌 Notes

* This solution avoids brute force and incorrect heap assumptions
* Safe for duplicates and large windows
* Suitable for **LeetCode / Codeforces / interviews**

---

Happy coding 🚀
