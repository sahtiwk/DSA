# LeetCode 1390 – Four Divisors

This document explains **two optimal approaches** to solve **LeetCode 1390: Four Divisors**:

1. **Divisor Counting Method (√n approach)**
2. **Sieve + Mathematical Observation Method (most optimal)**

---

## 🔹 Problem Recap

Given an integer array `nums`, for each number:

* Check if it has **exactly 4 divisors**
* If yes, add the **sum of those divisors** to the answer
* Return the total sum

---

## 🔹 Key Mathematical Observation

A number has **exactly 4 divisors if and only if** it is of one of the following forms:

1. **p³**, where `p` is a prime number
   Divisors → `{1, p, p², p³}`

2. **p × q**, where `p` and `q` are **distinct primes**
   Divisors → `{1, p, q, p×q}`

No other number can have exactly 4 divisors.

---

## 🟢 Method 1: Divisor Counting (Optimized √n)

### 💡 Idea

Instead of storing divisors in a set:

* Count divisors directly
* Maintain their sum
* Stop early if divisor count exceeds 4

This avoids expensive data structures like `unordered_set`.

### ⏱️ Complexity

* **Time:** `O(N √M)`
* **Space:** `O(1)`

(`M` = max value in `nums`)

### ✅ Implementation

```cpp
class Solution {
public:
    int sumFourDivisors(vector<int>& nums) {
        int ans = 0;

        for (int n : nums) {
            int cnt = 0, divSum = 0;

            for (int i = 1; i * i <= n; i++) {
                if (n % i == 0) {
                    int d1 = i;
                    int d2 = n / i;

                    cnt++;
                    divSum += d1;

                    if (d1 != d2) {
                        cnt++;
                        divSum += d2;
                    }

                    if (cnt > 4) break;
                }
            }

            if (cnt == 4) ans += divSum;
        }

        return ans;
    }
};
```

---

## 🟢 Method 2: Sieve + Math-Based Optimization (Best)

### 💡 Idea

Instead of checking all divisors:

* Precompute primes using **Sieve of Eratosthenes**
* For each number, try to find **one factor `p`**
* Let `q = n / p`
* Validate if:

  * `p` and `q` are primes (p × q case)
  * OR `n = p³` (prime cube case)

Only **one factor check** is enough.

---

## 🧠 Sieve of Eratosthenes

The sieve efficiently precomputes prime numbers up to `10⁵`.

### ⏱️ Complexity

* **Precomputation:** `O(M log log M)`
* **Per number:** almost `O(1)`
* **Space:** `O(M)`

---

### ✅ Sieve-Based Implementation

```cpp
class Solution {
public:
    vector<bool> sieve(int n) {
        vector<bool> prime(n + 1, true);
        prime[0] = prime[1] = false;

        for (int i = 2; i * i <= n; i++) {
            if (prime[i]) {
                for (int j = i * i; j <= n; j += i)
                    prime[j] = false;
            }
        }
        return prime;
    }

    int sumFourDivisors(vector<int>& nums) {
        const int MAX = 100000;
        vector<bool> prime = sieve(MAX);
        int ans = 0;

        for (int n : nums) {
            for (int p = 2; p * p <= n; p++) {
                if (n % p == 0) {
                    int q = n / p;

                    if (p != q && prime[p] && prime[q]) {
                        ans += 1 + p + q + n;
                    }
                    else if ((long long)p * p * p == n && prime[p]) {
                        ans += 1 + p + p*p + n;
                    }
                    break;
                }
            }
        }
        return ans;
    }
};
```

---

## 🔚 Final Comparison

| Method        | Time   | Space | Notes                     |
| ------------- | ------ | ----- | ------------------------- |
| Divisor Count | O(N√M) | O(1)  | Simple & safe             |
| Sieve + Math  | ⭐ O(N) | O(M)  | Fastest & interview-ready |

---

## 🎯 Key Takeaway

> When divisor count is **fixed**, always reduce the problem to **number forms** instead of brute force.

This optimization pattern is extremely common in competitive programming and interviews.