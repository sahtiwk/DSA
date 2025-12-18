# 3573. Best Time to Buy and Sell Stock V

## 📝 Problem Description
You are given an integer array `prices` where `prices[i]` is the price of a stock on the $i^{th}$ day, and an integer `k`.

You are allowed to make at most **k transactions**. A transaction can be:
1.  **Normal transaction:** Buy on day $i$, then sell on a later day $j$ ($i < j$).
2.  **Short selling transaction:** Sell on day $i$, then buy back on a later day $j$ ($i < j$).

**Key Constraints:**
* You must complete each transaction before starting another.
* **No Same-Day Trading:** You cannot buy or sell on the same day you are closing a previous transaction.
* Maximize the total profit.

---

## 💡 Logic & Approach
This problem is a variation of the classic "Buy and Sell Stock" series. The introduction of **Short Selling** means we can profit from both price increases and price decreases. Essentially, for any transaction, the profit is $|prices[j] - prices[i]|$.

### Dynamic Programming Strategy
We use a DP approach where we track the maximum profit at each day for up to `k` transactions.

1.  **State Representation:**
    * `dp[j]` represents the maximum profit using $t-1$ transactions up to day $j$.
    * `next_dp[j]` represents the maximum profit using $t$ transactions up to day $j$.

2.  **Maintaining Entry Points:**
    To calculate the current transaction $t$ ending on day $j$, we maintain two states:
    * `max_val_normal`: The best "Buy" price we've seen so far, considering the profit from the previous transaction.
    * `max_val_short`: The best "Sell" price we've seen so far for a short position.

3.  **Handling Disjoint Days:**
    The rule "can't buy or sell on the same day as a previous transaction" is handled by using `dp[j-2]` as the base profit when starting a new trade on day `j-1`. This ensures a minimum 1-day gap between transactions.

---

## 🚀 Complexity Analysis
* **Time Complexity:** $O(k \cdot n)$, where $n$ is the number of days. We iterate through $k$ transactions and for each, we traverse the prices once.
* **Space Complexity:** $O(n)$. We optimize space by only keeping the results of the current and previous transaction count.

---

## 💻 Implementation

```cpp
#include <vector>
#include <algorithm>

using namespace std;

class Solution {
public:
    long long maximumProfit(vector<int>& prices, int k) {
        int n = prices.size();
        if (n < 2 || k == 0) return 0;

        // dp[j] stores max profit for (t-1) transactions up to day j
        vector<long long> dp(n, 0);

        for (int t = 1; t <= k; t++) {
            vector<long long> next_dp(n, 0);
            
            // Initializing with a very small value to handle long long range
            long long max_val_normal = -2e18; 
            long long max_val_short = -2e18;

            for (int j = 1; j < n; j++) {
                // Ensure disjoint days: if starting a trade on day j-1, 
                // the previous trade must have ended by day j-2.
                long long prev_profit = (j >= 2) ? dp[j - 2] : 0;
                
                // Track best entry points for a normal buy or a short sell
                max_val_normal = max(max_val_normal, prev_profit - prices[j - 1]);
                max_val_short = max(max_val_short, prev_profit + prices[j - 1]);

                // Option 1: Don't complete any transaction today (carry forward profit)
                next_dp[j] = next_dp[j - 1];

                // Option 2: Complete a Normal transaction today (Sell)
                next_dp[j] = max(next_dp[j], (long long)prices[j] + max_val_normal);

                // Option 3: Complete a Short transaction today (Buy back)
                next_dp[j] = max(next_dp[j], (long long)max_val_short - prices[j]);
            }
            // Move current transaction results to previous for the next iteration
            dp = next_dp;
        }

        return dp[n - 1];
    }
};