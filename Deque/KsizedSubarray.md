# K Sized Subarray Maximum (GFG – POTD)

## 📌 Problem Statement

Given an array `arr[]` of positive integers and an integer `k`, find the **maximum value for each contiguous subarray of size `k`**.

## 📍 Problem Reference

Read the full problem on GeeksforGeeks Practice:  
https://www.geeksforgeeks.org/problems/maximum-of-all-subarrays-of-size-k3101/1 :contentReference[oaicite:0]{index=0}

---

## 🧠 Key Idea

The brute-force approach (checking max for every subarray) takes **O(n·k)** time, which is too slow for large inputs.

An **optimized approach** uses a **Deque (Double Ended Queue)** to keep track of indices of useful elements in the current window.

---

## 🚀 Optimized Approach (Deque / Sliding Window)

### Why Deque?

* Stores **indices**, not values
* Maintains elements in **decreasing order of values**
* Front of deque always contains the **maximum** of the current window

### Algorithm Steps

1. Traverse the array from left to right
2. Remove indices from the front if they are **out of the current window**
3. Remove indices from the back if their values are **smaller than the current element**
4. Add the current index to the deque
5. Once the window size reaches `k`, record the maximum

---

## ⏱️ Complexity Analysis

* **Time Complexity:** `O(n)`
* **Space Complexity:** `O(k)`

---

## ✅ C++ Implementation

```cpp
class Solution {
  public:
    vector<int> maxOfSubarrays(vector<int>& arr, int k) {
        int n = arr.size();
        deque<int> dq;
        vector<int> res;
        
        for (int i = 0; i < n; i++) {
            // Remove elements out of this window
            if (!dq.empty() && dq.front() == i - k)
                dq.pop_front();
            
            // Remove smaller elements from back
            while (!dq.empty() && arr[dq.back()] <= arr[i])
                dq.pop_back();
            
            dq.push_back(i);
            
            // Window size reached
            if (i >= k - 1)
                res.push_back(arr[dq.front()]);
        }
        return res;
    }
};
```

---

## 🧪 Example

**Input:**

```
arr = [1, 2, 3, 1, 4, 5, 2, 3, 6]
k = 3
```

**Output:**

```
[3, 3, 4, 5, 5, 5, 6]
```

---

## 📝 Notes

* Works efficiently even for large inputs (`n` up to `10^6`)
* Classic **Sliding Window + Deque** problem
* Frequently asked in interviews

---

✨ **GeeksforGeeks – Problem of the Day**