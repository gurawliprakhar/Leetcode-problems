

---

### 📄 README.md Content

````markdown
# 🏆 Leetcode 1900 - The Earliest and Latest Rounds Where Players Compete

## 📖 Problem Statement (Story Mode)

Once upon a time in a grand tournament, **n brave players** lined up in order from `1` to `n`. Every round, the matchups were unusual but fair:

- The **first player** fights the **last player**.
- The **second player** fights the **second last**, and so on...
- If there's an odd number of players, the one in the middle gets a free pass to the next round.

⚔️ Two players are special: `firstPlayer` and `secondPlayer`. They are **undefeated** and will win every match **unless** they face each other.

Your task is to find out:

> **What is the earliest and latest round in which these two champions can face each other?**

---

## 🧪 Example Test Case

```java
n = 11;
firstPlayer = 2;
secondPlayer = 4;
````

### ✅ Output:

```java
[3, 4]
```

### 💬 What does this mean?

* 🕐 The **earliest** round they can meet is **Round 3**.
* 🐢 The **latest** round they could meet is **Round 4**.
* It all depends on **how other players win or lose** — which you get to control!

---

## 🔍 How It Works – Step by Step

Imagine players standing in a line:

```
[1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11]
```

### 🎮 Round 1 Matchups:

* 1 vs 11
* 2 vs 10 ✅
* 3 vs 9
* 4 vs 8 ✅
* 5 vs 7
* ➕ Player 6 skips (odd number of players)

We control who wins — but **2 and 4 always win**.

Depending on who wins other matches:

* They can meet **sooner** if you eliminate other players early.
* Or they can meet **later** if you spread out the competition.

---

## 🧠 Approach

We use **DFS + memoization** to:

* Try **all possible winner combinations** (except 2 and 4 who always win unless they face each other).
* At each round, we simulate who moves to the next round.
* When 2 and 4 finally meet, we record the round number.
* We track the **minimum and maximum** rounds where this happens.

---

## 💻 Code – Java

```java
// File: 1900_EarliestAndLatestRounds.java

import java.util.*;

class Solution {
    public int[] earliestAndLatest(int n, int firstPlayer, int secondPlayer) {
        List<Integer> list = new ArrayList<>();
        for (int i = 1; i <= n; i++) list.add(i);

        Map<String, int[]> map = new HashMap<>();
        return dfs(list, firstPlayer, secondPlayer, 1, map);
    }

    private int[] dfs(List<Integer> players, int firstPlayer, int secondPlayer, int round, Map<String, int[]> map) {
        String key = players.toString();
        if (map.containsKey(key)) return map.get(key);

        int size = players.size();

        // Check if 2 champions are fighting each other this round
        for (int i = 0; i < size / 2; i++) {
            int a = players.get(i), b = players.get(size - 1 - i);
            if ((a == firstPlayer && b == secondPlayer) || (a == secondPlayer && b == firstPlayer))
                return new int[]{round, round};
        }

        int min = Integer.MAX_VALUE, max = Integer.MIN_VALUE;
        int mid = (size % 2 == 1) ? players.get(size / 2) : -1;
        int count = size / 2;

        for (int mask = 0; mask < (1 << count); mask++) {
            List<Integer> next = new ArrayList<>();
            for (int i = 0; i < count; i++) {
                int a = players.get(i), b = players.get(size - 1 - i);

                if (a == firstPlayer || a == secondPlayer) next.add(a);
                else if (b == firstPlayer || b == secondPlayer) next.add(b);
                else next.add(((mask & (1 << i)) == 0) ? b : a);
            }

            if (mid != -1) next.add(mid);

            Collections.sort(next);
            int[] res = dfs(next, firstPlayer, secondPlayer, round + 1, map);
            min = Math.min(min, res[0]);
            max = Math.max(max, res[1]);
        }

        int[] result = new int[]{min, max};
        map.put(key, result);
        return result;
    }
}
```

---

## 🧪 Dry Run (For n = 11, firstPlayer = 2, secondPlayer = 4)

**Round 1:**
Lineup: \[1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11]
Matchups:

* 1 vs 11
* 2 vs 10 ✅
* 3 vs 9
* 4 vs 8 ✅
* 5 vs 7
* ➕ 6 skips

After Round 1 → possible winners like: `[2, 3, 4, 5, 6, 11]`

**Round 2:**

* 2 vs 11
* 3 vs 6
* ➕ 4 skips
  → Winners: `[2, 3, 4]`

**Round 3:**

* 2 vs 4 👑 The clash!

✅ **Earliest Round = 3**

Now if you delay by allowing others to win:

**Round 1 winners:** `[1, 2, 3, 4, 5, 6]`
**Round 2 winners:** `[1, 2, 4]`
**Round 3:** `[2, 4]`
**Round 4:** 2 vs 4

✅ **Latest Round = 4**

---

## 📘 Summary

* Problem involves simulating a unique tournament structure.
* DFS + memoization helps explore all match outcomes.
* We must handle middle players, sort winners, and control flow.
* Great practice for **state simulation**, **backtracking**, and **recursion**!

---


```

---

## ⭐ Like This?

Follow me for more readable, intuitive explanations of complex Java and algorithm problems.
Got a question or idea? Drop it in the issues or discussions section!

```

---

```
