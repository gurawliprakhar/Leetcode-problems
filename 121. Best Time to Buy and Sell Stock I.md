

---

# LeetCode 121 — Best Time to Buy and Sell Stock I

**Difficulty:** Easy  
**Tags:** Array, Greedy  


## 🧩 Problem Statement

You are given an array `prices` where `prices[i]` is the price of a given stock on the `i`-th day.

Your goal is to maximize your profit by choosing a single day to **buy** one stock and a different day in the future to **sell** that stock.

Return the maximum profit you can achieve from this transaction. If no profit is possible, return `0`.

### 🔒 Constraints
- `1 <= prices.length <= 10⁵`
- `0 <= prices[i] <= 10⁴`

---

## 💡 Example

### Example 1:
```
Input:  prices = [7,1,5,3,6,4]
Output: 5
Explanation: Buy on day 2 (price = 1) and sell on day 5 (price = 6), profit = 6 - 1 = 5.
```

### Example 2:
```
Input:  prices = [7,6,4,3,1]
Output: 0
Explanation: No transaction is done since prices are in decreasing order.
```

---

## 🚀 Approach

We use a **single pass greedy approach**:

- Track the **minimum price** seen so far.
- At each step, calculate the **profit** if we sold at the current price.
- Update the **maximum profit** if the current profit is higher.

This ensures **O(n)** time complexity and **O(1)** space.

---

## 🧪 Dry Run

For `prices = [7,1,5,3,6,4]`:

| Day | Price | Min Price So Far | Profit (Price - Min) | Max Profit |
|-----|-------|------------------|-----------------------|-------------|
| 0   | 7     | 7                | 0                     | 0           |
| 1   | 1     | 1                | 0                     | 0           |
| 2   | 5     | 1                | 4                     | 4           |
| 3   | 3     | 1                | 2                     | 4           |
| 4   | 6     | 1                | 5                     | 5           |
| 5   | 4     | 1                | 3                     | 5           |

✅ Final Answer: `5`

---

## 🧾 Code

```java
class Solution {
    public int maxProfit(int[] prices) {
        int min = Integer.MAX_VALUE;
        int max = 0;

        for (int i = 0; i < prices.length; i++) {
            if (prices[i] < min) {
                min = prices[i]; // update minimum price
            } else {
                int profit = prices[i] - min; // calculate profit
                if (profit > max) {
                    max = profit; // update max profit
                }
            }
        }

        return max;
    }
}
```

---

## 🧠 Complexity Analysis

| Metric         | Value     |
|----------------|-----------|
| Time Complexity| O(n)      |
| Space Complexity| O(1)     |

---

## 🏁 Conclusion

This solution is optimal for large inputs and leverages a greedy strategy to track the best opportunity to buy low and sell high. It’s a classic example of how a simple linear scan can outperform more complex approaches when applied thoughtfully.

---
