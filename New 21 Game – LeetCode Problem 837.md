
---

```markdown
# 🎰 New 21 Game – LeetCode Problem 837

## 🧩 Problem Statement

Alice plays a game loosely based on "21":

- She starts with 0 points.
- While her score is **less than `k`**, she draws numbers.
- Each draw gives her a random integer between **1 and `maxPts`** (inclusive).
- Once her score reaches **`k` or more**, she **stops drawing**.
- Compute the probability that **her final score is ≤ `n`**.

Answers within `10^-5` precision are accepted.

---

## 🚀 Example

### Input:
```
n = 21, k = 17, maxPts = 10
```

### Output:
```
0.73278
```

### Explanation:
Alice draws until score ≥ 17.  
From scores `17 to 21`, she stops and is considered successful.  
DP helps us count all such outcomes and sum their probabilities.

---

## 📚 Approach

### Core Idea:
Use **Dynamic Programming with Sliding Window** to track probabilities for each score.

### DP State:
Let `dp[i]` represent the probability of reaching **exactly score `i`**.

### Transitions:
- If `i < k`: Alice can still draw → `dp[i] = windowSum / maxPts`
- If `i ≥ k`: She stops drawing → add `dp[i]` to result

---

## 🧠 Code (with Hinglish Comments)

```java
class Solution {
    public double new21Game(int n, int k, int maxPts) {
        if (k == 0 || n >= k + maxPts) return 1.0; // edge cases

        double[] dp = new double[n + 1];
        dp[0] = 1.0; // Game starts with 0 points

        double windowSum = 1.0; // sum of last maxPts dp values
        double result = 0.0;

        for (int i = 1; i <= n; i++) {
            dp[i] = windowSum / maxPts; // average of reachable probabilities

            if (i < k) {
                windowSum += dp[i]; // still drawing
            } else {
                result += dp[i]; // stop drawing → accumulate result
            }

            if (i - maxPts >= 0) {
                windowSum -= dp[i - maxPts]; // slide window
            }
        }

        return result;
    }
}
```

---

## 🔍 Dry Run (n=10, k=1, maxPts=10)

- Alice draws **once**.
- Possible outcomes: `1, 2, ..., 10`
- Since all ≤ `n=10`, final probability = **1.00000**

---

## ⏱ Complexity

| Metric      | Value     |
|-------------|-----------|
| Time        | O(n)      |
| Space       | O(n)      |
| Optimization| Sliding Window keeps it fast ✅ |

---

## ✅ Test Coverage

- `new21Game(10, 1, 10)` → `1.00000`
- `new21Game(6, 1, 10)` → `0.60000`
- `new21Game(21, 17, 10)` → `0.73278`

---

## 📦 Tags

`Dynamic Programming`, `Sliding Window`, `Probability`, `LeetCode Medium`

---

```
