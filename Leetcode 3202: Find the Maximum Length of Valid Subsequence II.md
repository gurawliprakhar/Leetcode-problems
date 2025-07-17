# Leetcode 3202: Find the Maximum Length of Valid Subsequence II

## 🔢 Problem Statement:

We are given:

* An array of integers `nums`
* A positive integer `k`

### Goal:

Find the **maximum length** of a valid **subsequence** such that:
For every two **consecutive elements** in the subsequence,

> `(a + b) % k` is the **same value**.

### Example 1:

```java
nums = [1, 2, 3, 4, 5], k = 2
```

* (1 + 2) % 2 = 1
* (2 + 3) % 2 = 1
* (3 + 4) % 2 = 1
* (4 + 5) % 2 = 1
  ✅ All pairs give 1 ➔ Valid sequence of length 5

### Example 2:

```java
nums = [1, 4, 2, 3, 1, 4], k = 3
```

Try: \[1, 4, 1, 4]

* All (a + b) % 3 = 2
  ✅ Valid sequence of length 4

---

## 💡 Key Insight:

We want the longest subsequence such that all consecutive pairs:

```java
(a + b) % k == (b + c) % k == ...
```

Let this common modulo value be `val` ➔ it ranges from 0 to k - 1

### Rearranging:

To maintain (a + b) % k == val, we need:

```java
b % k == (val - (a % k) + k) % k
```

This gives us a **transition condition**: what kind of number we can add after another

---

## 📊 Dynamic Programming Design:

We use a 2D DP array:

```java
int[][] dp = new int[k][k];
```

Where:

* `dp[prev][curr]` = longest subsequence where:

  * previous number has mod = prev
  * current number has mod = curr

---

## ⚖️ Code:

```java
class Solution {
    public int maximumLength(int[] nums, int k) {
        int[][] dp = new int[k][k];
        int res = 0;

        for (int num : nums) {
            num %= k;
            for (int prev = 0; prev < k; prev++) {
                dp[prev][num] = dp[num][prev] + 1;
                res = Math.max(res, dp[prev][num]);
            }
        }

        return res;
    }
}
```

---

## 📉 Dry Run:

### Input:

```java
nums = [1, 4, 1, 4], k = 3
```

### Step 1: Initialization

```java
dp[3][3] = all zeros
res = 0
```

### Step 2: Iterate nums

#### num = 1 ➔ mod = 1

```java
dp[0][1] = dp[1][0] + 1 = 1
res = 1
```

#### num = 4 ➔ mod = 1

```java
dp[1][1] = dp[1][1] + 1 = 2
res = 2
```

#### num = 1 ➔ mod = 1

```java
dp[1][1] = 2 + 1 = 3
res = 3
```

#### num = 4 ➔ mod = 1

```java
dp[1][1] = 3 + 1 = 4
res = 4
```

---

## 🔢 Final Answer:

```java
res = 4
```

Valid subsequence: \[1, 4, 1, 4] ➔ All (a + b) % 3 = 2

---

## 📊 Time & Space Complexity:

* Time: O(n \* k)
* Space: O(k^2)

---

## ✅ Summary:

* Track longest sequences where (a + b) % k stays constant
* Use 2D DP to remember best paths
* Try all (prev, curr) mod combinations
* Efficient for n, k ≤ 1000

---

👋 That's how you solve **"Find the Maximum Length of Valid Subsequence II"** using dynamic programming and modular arithmetic!
