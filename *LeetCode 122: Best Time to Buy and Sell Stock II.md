
---

# 📈 Best Time to Buy and Sell Stock II

## 🧠 Problem Statement (with Story)

Imagine you're a stock trader with a simple rule: you can buy and sell a stock as many times as you want — even on the same day — but you can only hold one share at a time.

Each day, you're given the price of a stock. Your mission? Ride every upward wave in the market to maximize your profit.

You're not trying to predict the future. You're just trying to take advantage of every opportunity where today's price is higher than yesterday's. Buy low, sell high — again and again.

---

## 📥 Input

- An integer array `prices` where `prices[i]` is the price of a stock on day `i`.

## 🎯 Output

- Return the maximum profit you can achieve.

---

## 🧪 Example

### Input:
```java
prices = [7, 1, 5, 3, 6, 4]
```

### Walkthrough:
- Day 1: Price = 7 → too high, wait.
- Day 2: Price = 1 → buy.
- Day 3: Price = 5 → sell → profit = 4.
- Day 4: Price = 3 → buy.
- Day 5: Price = 6 → sell → profit = 3.
- Day 6: Price = 4 → no action.

✅ Total Profit = 4 + 3 = **7**

### Output:
```java
7
```

---

## 💡 Approach

Use a **greedy strategy**:
- Loop through the array.
- If today’s price is higher than yesterday’s, simulate a buy yesterday and sell today.
- Accumulate the profit from every such opportunity.

---

## ✅ Java Code

```java
class Solution {
    public int maxProfit(int[] prices) {
        int profit = 0;

        for (int i = 1; i < prices.length; i++) {
            if (prices[i] > prices[i - 1]) {
                int gain = prices[i] - prices[i - 1];
                profit += gain;
            }
        }

        return profit;
    }
}
```

---

## 🔍 Dry Run

Let’s dry-run the input `prices = [7, 1, 5, 3, 6, 4]`:

| i | prices[i - 1] | prices[i] | Condition (>) | gain = prices[i] - prices[i - 1] | profit |
|---|---------------|-----------|----------------|----------------------------------|--------|
| 1 | 7             | 1         | ❌ false        | —                                | 0      |
| 2 | 1             | 5         | ✅ true         | 4                                | 4      |
| 3 | 5             | 3         | ❌ false        | —                                | 4      |
| 4 | 3             | 6         | ✅ true         | 3                                | 7      |
| 5 | 6             | 4         | ❌ false        | —                                | 7      |

### Final Output:
```java
return 7;
```

---

## ⏱️ Time & Space Complexity

| Metric           | Value     |
|------------------|-----------|
| Time Complexity  | O(n)      |
| Space Complexity | O(1)      |

---

